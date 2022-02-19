---
title: "PTLCs : de l'art d'acheminer des paiements au sein d'un réseau adversarial tout en préservant la vie privée des participants"
date: 2022-01-15T12:00:00+01:00
cover:
    image: "../images/storm.jpg"
    alt: "storm"
    caption: "<text>"
    relative: false
tags: ["lightning", "bitcoin"]
categories: ["articles"]
draft: false
---

Si le Lightning Network est si utile aujourd'hui, c'est en bonne partie grâce à la possibilité d'y **router** des paiements : si Alice souhaite payer Bob, il n'est pas indispensable qu'elle ait un canal direct avec lui. A la place, elle peut avoir un canal avec Carole et, si Carole a un canal avec Bob, passer par ce-dernier pour atteindre Bob.

Avec ce fonctionnement se pose une nouvelle question : comment de tels paiements, qui dépendent de la bonne volonté de tierces parties comme Carole, peuvent-ils être réalisés sans avoir besoin de faire confiance à qui que ce soit ? Pendant longtemps, ce sont les HTLCs (pour Hash Time Locked Contracts, un type spécifique de transactions conditionnelles sur Bitcoin) qui ont permis d'apporter une réponse satisfaisante à cette question. Mais les HTLCs viennent eux-mêmes avec leur lot d'inconvénients, notamment en matière de confidentialité des transactions.

C'est pourquoi un nouveau sauveur a été créé : les PTLCs (pour Point Time Locked Contracts), qui amènent les mêmes fonctionnalités que les HTLCs tout en préservant la vie privée des utilisateurs.

## Des HTLCs

Les HTLCs sont aujourd'hui une composante clé du fonctionnement de Lightning, car ils permettent aux paiements d'être acheminés sans confiance au sein du réseau. Il est ainsi possible d'envoyer des fonds à quelqu'un sur Lightning sans qu'il soit nécessaire d'avoir un canal direct avec cette personne, tant qu'il exite une route pour y parvenir.

L'aspect "sans confiance" est atteint de la même façon que c'est bien souvent le cas sur Lightning : en construisant et signant des transactions Bitcoin spécifiques, qui ne sont pas publiées dans la majorité des cas mais peuvent l'être, en cas de problème, afin que chaque partie prenante récupère les fonds qui lui reviennent sur Bitcoin (*on-chain*).

J'ai publié il y a bientôt un an une {{<newtabref href="https://www.youtube.com/watch?v=-JC4mkq7H48" title="vidéo">}} expliquant le fonctionnement des HTLCs. La vidéo est en français, et sous-titrée en français et anglais. Je vous invite à la visionner si le format vidéo vous sied davantage, mais je vais de toute façon réitérer ces explications dans les paragraphes qui suivent.

La vie d'un paiement sur Lightning commence lorsque la personne souhaitant être payée (Bob) crée une *invoice* (facture en anglais). Cette *invoice* contient diverses informations, comme la clé publique de Bob (son "adresse" au sein du réseau), le montant qu'il souhaite recevoir (par exemple 40 000 satoshis), etc. Elle contient également un nombre, souvent dénoté *r*. Ce nombre est le *hash* d'un secret, noté *s* et appelé **préimage**, que Bob a crée de manière aléatoire exprès pour ce paiement. Bob envoie ensuite l'*invoice* à la personne dont il veut recevoir le paiement (Alice).

```md
Demander un paiement :
1. Générer aléatoirement une préimage s
2. Calculer r = hash(s)
3. Créer une invoice contenant le montant, la clé publique, la préimage, etc.
4. Envoyer l'invoice à Alice.
```

Lorsqu'elle reçoit l'*invoice*, Alice commence par essayer de trouver une route jusqu'au nœud de Bob. Idéalement, il s'agirait d'un canal direct entre elle et Bob mais, bien souvent, il faudra passer par des nœuds intermédiaires au sein du réseau. Dans ce cas par exemple, Alice sélectionne une route qui passe par le nœud de Susie.

```md
+-----+        +-----+        +-----+
|     |        |     |        |     |
|Alice|<------>|Susie|<------>| Bob |
|     |        |     |        |     |
+-----+        +-----+        +-----+
```

Elle construit ensuite un paiement conditionnel, un HTLC, qu'elle envoie à Susie. Ce HTLC indique : "voici 40 000 satoshis. Pour les récupérer, vous devez me communiquer un secret *s'* tel que le hash de *s'* soit égal à *r* ". Dans le reste de cet article, nous noterons un tel HTLC `HTLC(r)`[^1]. Susie est également informée qu'un bon moyen pour elle d'apprendre le secret est de demander à Bob. Elle construit donc à son tour son propre HTLC(r), envoyant 40 000 satoshis à la condition de révéler un secret *s'* dont le hash est égal à *r* ; et l'envoie à Bob.

Partant de là, tout ce que Bob a à faire pour débloquer le paiement conditionnel de Susie et récupérer les 40 000 satoshis qu'il contient, est de révéler un nombre dont le hash vaut *r*. Or, il a justement ça en stock puisque, par construction, `r = hash(s)`. Bob révèle donc la préimage *s* à Susie, ce qui lui permet de débloquer le paiement conditionnel de Susie et de récupérer les 40 000 satoshis. Maintenant que Susie connaît *s*, elle peut à son tour le révéler à Alice et ainsi satisfaire la condition du HTLC d'Alice. Une fois que tous les HTLCs sont résolus, le paiement est complété : Alice a 40 000 satoshis de moins, Bob 40 000 de plus, et le solde total de Susie n'a pas changé. Pour déplacer 40 000 satoshis d'Alice à Bob, 40 000 satoshis ont donc été déplacés dans le canal entre Alice et Susie, du côté d'Alice vers celui de Susie ; et 40 000 satoshis ont été déplacés dans le canal entre Susie et Bob, du côté de Susie vers celui de Bob[^2] ; le tout de façon atomique.

Si le paiement implique deux nœuds intermédiaires (Susie et Tim) au lieu d'un seul, il y a simplement un HTLC de plus entre Susie et Tim. Chaque nœud intermédiaire n'est au courant que du nœud avant lui et de celui après lui : Susie sait qu'elle doit envoyer un HTLC à Tim pour apprendre le secret, mais elle ne sait pas si Tim est le destinataire final du paiement ou un simple intermédiaire. De même, elle ne sait pas si Alice est l'émettrice originelle du paiement, ou juste un autre nœud sur la route. Ce mécanisme se nomme Routage en Oignon, et il apporte une certaine confidentialité aux paiements sur le réseau Lightning.

```md
+-----+        +-----+        +-----+        +-----+
|     |        |     |        |     |        |     |
|Alice|<------>|Susie|<------>| Tim |<------>| Bob |
|     |        |     |        |     |        |     |
+-----+        +-----+        +-----+        +-----+
```

Ainsi, dans notre exemple à quatre nœuds, la procédure complète ressemble à :

```md
1. Bob génère aléatoirement une préimage s, calcule r = hash(s) et envoie r à Alice dans l'invoice.
2. Alice sélectionne une route vers Bob passant par Susie et Tim.
3. Elle envoie un HTLC(r) à Susie.
4. Susie sait seulement qu'elle a reçu un HTLC(r) de la part d'Alice, et qu'elle peut obtenir le secret correspondant (s) en demandant à Tim. Elle envoie donc un HTLC(r) à Tim.
5. Tim sait seulement qu'il a reçu un HTLC(r) de la part de Susie, et qu'il peut obtenir le secret correspondant (s) en demandant à Bob. Il envoie donc un HTLC(r) à Bob.
6. Bob révèle la préimage s à Tim, ce qui déverouille le HTLC de Tim et envoie les fonds qu'il renferme de Tim à Bob.
7. Tim révèle la préimage qu'il vient d'apprendre à Susie, ce qui déverrouille le HTLC de Susie et envoie les fonds qu'il renferme de Susie à Tim.
8. Susie révèle la préimage qu'elle vient d'apprendre à Alice, ce qui déverrouille le HTLC d'Alice et envoie les fonds qu'il renferme de Alice à Susie.
9. Tada ! 🎉 Le paiement a été effectué !
```

Les HTLCs permettent donc aux paiement d'être acheminés sans confiance d'un bout à l'autre du réseau, même en passant par de multiples tierces parties. Le Routage en Oignon paraît protéger la confidentialité des transactions de manière satisfaisante, en dissimulant l'origine et la destination des fonds aux nœuds intermédiaires. Alors pourquoi vouloir les remplacer par autre chose ?

## Vilains HTLCs ?

L'un des problèmes avec les HTLCs réside dans la réutilisation de la même préimage le long de l'ensemble de la route. Qui plus est, puisque la préimage est générée de manière aléatoire par le destinataire du paiement, la probabilité que deux paiements différents aient la même préimage est négligeable. Ainsi, si une entité (individu, entreprise, État, etc.) contrôle plusieurs nœuds sur la route d'un paiement donné, elle peut détecter que ce qui est entré en un point et ressorti en un autre correspond en fait à la même transaction. Ensuite, en utilisant certaines heuristiques (notamment concernant la longueur de la route ou le type de nœud Lightning), elle peut tenter de déterminer quel nœud sur la route est l'émetteur du paiement, et quel nœud en est le destinataire. La confidentialité apportée par le Routage en Oignon est perdue.

Considérons un exemple simple avec 5 nœuds : Alice, Bob, Carole, Daniel et Ève. Alice envoie un paiement à Ève mais, parce qu'il n'existe pas de canal direct entre elles, doit trouver une route au sein du réseau passant par d'autres nœuds. Elle choisit une route qui emprunte les canaux de Bob, Carole et Daniel. Ce qu'elle ne sait pas, en revanche, c'est que les nœuds de Bob et Daniel appartiennent en fait à la même entité (disons qu'il s'agit de {{<newtabref href="https://fanismichalakis.fr/posts/chainalysis-to-launch-lightning-network-support/" title="Chainalysis">}}).

```md
 +-----+        +-----+        +-----+        +-----+        +-----+
 |     |        |     |        |     |        |     |        |     |
 |  A  |<------>|  B  |<------>|  C  |<------>|  D  |<------>|  E  |
 |     |        |     |        |     |        |     |        |     |
 +-----+        +-----+        +-----+        +-----+        +-----+
 Émetteur        Spook      Nœud Honnête       Spook       Destinataire
```

Puisque les HTLCs utilisent tous la même préimage *s* (dont le hash est *r*), l'attaquant contrôlant les nœuds de Bob et Daniel sait qu'il s'agit d'un seul et même paiement. Le nœud de Bob sait qu'il a reçu un HTLC(r) provenant d'Alice et envoyé un HTLC(r) à Carole. Le nœud de Daniel sait qu'il a reçu un HTLC(r) de la part de Carole et envoyé un à Ève.

Avec ces informations, l'attaquant peut d'ores et déjà établir avec certitude que Carole est bien un nœud intermédiaire. S'il y avait d'autres nœuds entre Bob et Daniel en sus de Carole, l'attaquant ne les connaîtrait pas nécessairement tous, mais il saurait que quoi qu'il se passe à ce niveau, cela ne concernerait de toute façon que des nœuds intermédiaires.

Cependant, l'attaquant ne peut pas conclure avec certitude qu'Alice est l'émettrice du paiement. En effet, il pourrait il y avoir un autre nœud avant Alice, et Alice pourrait n'être qu'un intermédiaire de plus. Il en est de même pour Ève. Toutefois, nous savons que la fiabilité d'un paiement, sa capacité à être mené, décroit avec la longueur de la route : un nœud peut être hors-ligne, la liquidité d'un canal peut se trouver du mauvais côté par rapport à nos besoins, etc. ; et avec chaque nœud sur la route les probabilités que quelque chose échoue sont démultipliées. L'attaquant peut donc considérer qu'il est peu probable qu'une route compte plus de 3 intermédiaires[^3]. L'attaquant pourrait également savoir qu'Alice et Ève ont des nœuds mobiles (car elles sont souvent hors-ligne et que leur adresse IP change régulièrement) qui ne transmettent en général pas les paiements d'autres personnes et sont donc seulement émetteurs ou receveurs de paiements. En utilisant ce type d'heuristiques, l'attaquant pourrait considérer qu'il est *probable* qu'Alice est l'émettrice du paiement et qu'Ève en est la destinataire. Il pourrait dire quelque chose comme : "nos investigations ont déterminé, avec un intervalle de confiance de 90%, qu'Alice est l'émettrice et Ève la destinataire".

Si un attaquant dispose de quelques nœuds très bien connectés et pratiquant des frais compétitifs, il pourrait devenir un *hub* du réseau et se trouver régulièrement dans ce type de situation, où il lui est possible de "casser" la confidentialité du Routage en Oignon et déterminer l'origine et la destination d'un paiement. La confidentialité sur Lightning est-elle donc condamnée ?

## Les PTLCs à la rescousse

Le principal problème à l'égard de la vie privée est que nous réutilisons systématiquement la même préimage à chaque étape de la route. Plus précisément, chaque HTLC sur la route requiert la même préimage pour être déverrouillé[^4]. Existe-t-il un autre moyen de parvenir au même résultat ? Il faut garantir que :
- l'émetteur (Alice) soit en mesure de fournir une preuve de paiement au destinataire (Bob) une fois que le paiement est achevé,
- chaque nœud sur la route doit être en mesure de déverrouiller le paiement conditionnel envoyé par le nœud précédent en révélant un secret *s*,
- pour apprendre ce secret *s*, chaque nœud sur la route doit envoyer un paiement conditionnel au nœud suivant requérant qu'il lui révèle un secret *s'*, à partir duquel il est possible de retrouver *s*.

La voie "facile" pour y parvenir et vérifier ces trois conditions est de réutiliser le même secret *s* le long de la route. C'est ce qu'il se passe avec les HTLCs. Mais ce n'est pas le seul moyen. En effet, il n'est pas *nécessaire* que *s* et *s'* soient égaux. La seule condition indispensable est que les secrets soient tels que, en apprenant *s'*, un nœud puisse déterministiquement retrouver *s*. Que s'apelerio PTLCs.

Avec les HTLCs, le destinataire (Bob) commence par créer un secret pour ce paiement, la préimage. Avec les PTLCs, le destinataire fait quelque chose de très similaire, mais avec une clé privée. La préimage et la clé privée ne sont finalement rien d'autre que de grands nombres aléatoires, et la différence réside dans ce qu'on en fait.

Pour comprendre ce qui suit, quelques aspects basiques de cryptographie des courbes elliptiques sont nécessaires. Une courbe elliptique est une courbe bien spécifique, dont certaines propriétés sont très utiles aux cryptographes. L'objectif de cet article n'est pas de creuser trop profondément ce sujet, aussi nous contenterons-nous du strict nécessaire.
- On définit une opération d'addition, notée `+`, entre deux points sur la courbe elliptique. La somme `R` de deux points `P` et `Q` de la courbe est aussi un point de la courbe, mais sa localisation sur cette-dernière ne peut pas être directement reliée à celles de `P` et `Q`.
- On définit une opération de multiplication, notée `*`, représentant les additions successives d'un point de la courbe à lui-même. Ainsi, si `k` est un nombre et `P` un point de la courbe, `k*P = P + P + ... + P`, k fois. Parce que nous ajoutons `P` à lui-même à de nombreuses reprises, `k*P` peut être n'importe où sur la courbe. Autrement dit, même si je connais `P` et `k*P` (qui sont deux points sur la courbe), je ne peux pas trouver `k`.
- L'opération `*` a d'autres propriétés intéressantes, comme la distributivité : `a*P + b*P = (a + b)*P`.

Ces propriétés des courbes elliptiques sont appliquées à la cryptographie comme suit :
- Une clé privée `s` est un très long nombre.
- La clé publique associée à la clé privée `s` est `s*G`, où `G` est un point spécifique de la courbe, appelé générateur. Autrement dit, `G` est un point sur la courbe et une constante.
- Même si quelqu'un connaît la clé publique `s*G` et `G`, ils ne peuvent pas deviner la clé privée `s` pour autant.

Un autre point important à noter, bien qu'il puisse paraître trivial, concerne les additions classiques des nombres : connaître `a + b` est très différent de connaître `a` ou `b`. De même, même si je connais `a + b + c` et `a`, je suis loin de connaître `b` ou `c`.

Maintenant que notre esprit est armé de ces quelques concepts, reprenons notre exemple à 5 nœuds, où Alice paie Ève en passant par les canaux de Bob, Carole et Daniel ; et où Bob et Daniel se trouvent être un attaquant tentant de désanonymiser la transaction.

```md
 +-----+        +-----+        +-----+        +-----+        +-----+
 |     |        |     |        |     |        |     |        |     |
 |  A  |<------>|  B  |<------>|  C  |<------>|  D  |<------>|  E  |
 |     |        |     |        |     |        |     |        |     |
 +-----+        +-----+        +-----+        +-----+        +-----+
 Émetteur        Spook      Nœud Honnête       Spook       Destinataire
```

Le cheminent du paiement ressemble à quelque chose comme :

1. Ève génère une clé privée (donc secrète) `s` et donne la clé publique correspondante `s*G` à Alice dans une *invoice*, de la même façon qu'elle lui avait donné le *hash* de la préimage dans le cas avec les HTLCs.
2. Alice cherche une route jusqu'à Ève et en choisit une passant par 3 nœuds intermédiaires : Bob, Carole et Daniel.
3. Alice génère 4 nombres aléatoires `a`, `b`, `c` et `d`. Elle envoie `b` à Bob, `c` à Carole et `d` à Daniel. Elle envoie également `(a + b + c + d)` à Ève (la somme, pas `a`, `b`, `c` et `d` séparément).
4. Alice envoie un paiement conditionnel à Bob, pour lequel la condition est que Bob révèle la clé privée associée à `(a + s)*G`, qui est `(a + s)` par définition. Bob est également informé (dans le paquet oignon) que Carole connaît la clé privée associée à `(a + s)*G + b*G`, qui est `(a + b + s)`.
5. Bob réalise que, s'il connaissait `(a + b + s)`, il serait en mesure de calculer `a + s = a + b + s - b` et de le révéler à Alice pour récupérer le paiement conditionnel, puisqu'il connaît déjà `b` qu'Alice lui a communiqué à l'étape 3. Il envoie donc un paiement conditionnel à Carole, requérant qu'elle lui communique la clé privée associée à `( a + b + s)*G`.
6. Lorsque Carole reçoit le paiement conditionnel de la part de Bob, elle est également informée que Daniel connaît la clé privée associée à `(a + b + s)*G + c*G`, qui est `(a + b + c + s)`. Si elle connaissait `a + b + c + s` et `c`, Carole pourrait alors calculer `a + b + s` par soustraction. Elle envoie donc un paiement conditionnel à Daniel, avec la condition qu'il lui révèle la clé privée associée à `(a + b + c + s)*G`.
7. Lorsque Daniel reçoit le paiement conditionnel de Carole, il est également informé que Ève connaît la clé privée correspondant à `(a + b + c + s)*G + d*G`, qui est `(a + b + c + d + s)`. S'il connaissait `a + b + c + d + s` et `d`, il pourrait ensuite calculer `a + b + c + s` par soustraction et déverrouiller le paiement conditionnel de Carole. Pour découvrir `a + b + c + d + s`, il envoie un paiement conditionnel à Ève requérant qu'elle lui révèle la clé privée associée à `(a + b + c + d + s)*G`.
8. Ève connaît déjà `s`, puisqu'il s'agit du secret qu'elle a généré initialement. Elle connaît aussi `(a + b + c + d)`, puisqu'Alice le lui a envoyé à l'étape 3. Elle est donc en mesure de révéler `a + b + c + d + s` à Daniel et ainsi récupérer son paiement.
9. Maintenant qu'il connaît `a + b + c + d + s`, Daniel peut calculer `a + b + c + s` et le communiquer à Carole, récupérant ainsi son paiement.
10. Maintenant qu'elle connaît `a + b + c + s`, Carole peut calculer `a + b + s` et le communiquer à Bob, récupérant ainsi son paiement.
11. Maintenant qu'il connaît `a + b + s`, Bob peut calculer `a + s` et le communiquer à Alice, récupérant ainsi son paiement.
12. Alice connaît maintenant `a + s`. Puisqu'elle connaît déjà `a`, elle peut facilement calculer `s` par soustraction. Le secret `s` constitue alors la preuve de paiement d'Alice, qu'elle peut montrer à Ève pour lui prouver qu'elle a bien payé l'*invoice*.

```md
+-----+                    +-----+                    +-----+                    +-----+                    +-----+
|     |                    |     |                    |     |                    |     |                    |     |
|  A  |-----PTLC(a+s)----->|  B  |----PTLC(a+b+s)---->|  C  |---PTLC(a+b+c+s)--->|  D  |--PTLC(a+b+c+d+s)-->|  E  |
|     |                    |     |                    |     |                    |     |                    |     |
+-----+                    +-----+                    +-----+                    +-----+                    +-----+
```

Grâce à ce mécanisme, chaque nœud le long de la route est mis au courant d'un secret différent. Même s'ils travaillent ensemble, Bob et Daniel n'en savent pas assez pour pouvoir affirmer s'ils font partie du même paiement, ou s'il s'agissait de deux paiement différents :
- une fois le paiement complété, Bob ne connaît que `a + b + s`, `b` et `a + s`,
- une fois le paiement complété, Daniel ne connaît que `a + b + c + d + s`, `d` et `a + b + c + s`.

Même en rassemblant toutes ces informations, ils ne peuvent deviner s'ils ont participé à la même transaction globale. Depuis notre point de vue omniscient, nous voyons bien qu'ils peuvent calculer `c` avec `c = a + b + c + d + s - d - (a + b + s)`, mais ce nombre ne signifie rien pour eux, et ils en trouveraient de toute façon un, tout aussi abscon de leur point de vue, s'ils faisaient partie de deux paiement différents[^5]. Ils n'en savent tout simplement pas assez pour calculer `s`, le seul dénominateur commun du paiement.

Bien sûr, si l'attaquant contrôlait deux nœuds consécutifs d'un même paiement, il pourrait facilement déduire qu'il s'agit bien du même paiement, puisque chaque nœud sur la route connaît l'identité du suivant. Mais il lui faudrait alors contrôler les nœuds de Bob, Carole et Daniel pour pouvoir appliquer les mêmes heuristiques que précédemment (à savoir, qu'une route n'a "probablement" pas plus de 3 nœuds intermédiaires). Autrement dit, les PTLCs ne sont vraiment défaits que lorsque l'attaquant contrôle tous les nœuds d'une route. Et même ainsi, rappelons-le, il ne peut toujours pas affirmer avec certitude qu'Alice est l'émettrice et Ève la destinataire, puisqu'il se base sur des heuristiques.

## TL;DR

Parce qu'ils réutilisent le même secret le long de l'ensemble de la route, les HTLCs peuvent réduire considérablement les gains de confidentialité apportés (au prix de sérieuses inefficiences) par le Routage en Oignon. Les PTLCs, eux, emploient un secret différent pour chaque nœud sur la route. Ainsi, la confidentialité amenée par le Routage en Oignon est préservée.

## Ressouces complémentaires

Dans cet article, j'ai choisi de me concentrer sur les apports des PTLCs qui concernent la protection de la vie privée. Ils ont toutefois de nombreuses autres applications, détaillées dans cette séries d'article de {{<newtabref href="https://suredbits.com/payment-points-part-1/" title="Suredbits">}}.

[^1]: Le montant du paiement est omis car il n'est pas particulièrement utile dans cet article. Bien entendu, une notation plus détaillée pourrait être `HTLC(40000, r)` pour désigner un HTLC payant 40 000 satoshis à condition que le destinataire révèle un secret *s'* tel que hash(*s'*) = *r*.

[^2]: Nous omettons par simplification les frais de routage que Susie peut préléver.

[^3]: Évidemment, un paiement avec 4 nœuds intermédiaires est tout à fait possible. L'argument ici est plutôt qu'il est possible d'attacher des probabilités, dérivées de statistiques, à la réussite des paiements en fonction de la longueur de la route.

[^4]: Note : ce mécanisme n'impacte pas seulement la confidentialité. Dans notre exemple à 5 nœuds où Bob et Daniel travaillent en fait de concert, Daniel peut très bien envoyer la préimage à Bob dès qu'il l'apprend de Ève, et ainsi contourner Carole. Bob peut alors révéler la préimage à Alice : pour tout le monde excepté Carole, le paiement est complété. Pour Carole, il apparaît comme toujours en cours, jusqu'à ce que son HTLC périme. Mais entre temps, Bob et Daniel auront collecté les frais de routage de Carole à sa place.

[^5]: Il est également intéressant de noter qu'ils ne peuvent apprendre `c` qu'une fois que le paiement est terminé. Ainsi, contrairement aux HTLCs où Daniel pouvait transmettre la préimage directement à Bob et contourner Carole, ce type d'attaque (résultant dans le vol des frais revenant à Carole) n'est pas possible avec les PTLCs.