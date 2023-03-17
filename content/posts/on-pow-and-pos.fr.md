---
title: "Non, la Preuve de Travail n'est pas une \"erreur follement coûteuse\""
date: 2022-03-30T09:55:00+02:00
block: "729667"
cover:
    image: "../images/nuns_at_work-min.jpg"
    alt: "Tableau de Nonnes au travail par un discipe d'Alessandro Magnasco"
    caption: "Nonnes au travail -Disciple d'Alessandro Magnasco <br> Open Access - MET Museum."
    relative: false
paybuttonlink: "https://donate.fanismichalakis.fr/api/v1/invoices?storeId=EqjDottuNfgWVwvJPnmMGTdHnqhFJeadqyQ9WiTaqok1&orderId=onpowandpos&checkoutDesc=test&price=1000&currency=SATS"
tags: ["bitcoin"]
categories: ["articles"]
draft: false
---

L'envie d'écrire cet article m'est venue de la parution récente de deux papiers[^1] de {{<newtabref href="https://lejournal.cnrs.fr/auteurs/jean-paul-delahaye" title="M. Jean-Paul Delahaye">}}, professeur émérite à l'université de Lille 1 et chercheur au Centre de recherche en informatique, signal et automatique de Lille (CNRS/Centrale Lille Institut/Université de Lille). J'ai cependant longuement hésité avant de m'y résoudre. En effet, j'avais l'impression que les contre-arguments à ceux de M. Delahaye existaient déjà à profusion, librement accessibles pour qui se donnerait la peine de les rechercher. J'avais donc le sentiment de n'avoir pas grand chose à ajouter au débat. De plus, M. Delahaye provenant du monde académique et de la recherche, je craignais que ma réponse, bien qu'authentique, puisse n'être interprétée que comme une opposition de plus entre les deux sphères malheureusement si peu recouvrantes de nos jours que sont le monde académique et la communauté Bitcoin[^2]. Mon nom, en effet, n'est pas celui d'un éminent chercheur du CNRS.

Ceci n'est pas un brulôt anti-académique ni, il me semble, le verbatim d'un Bitcoiner aveuglé. Ceci est une réponse honnête et argumentée à l'opinion développée par M. Delahaye, dont j'ai d'ailleurs trouvé les textes plutôt bien construits[^3]. Ce texte se veut d'une portée plus générale encore, même s'il prend pour base et fondement cette opinion. Il se veut un rappel quant à l'utilité de Bitcoin et de sa Preuve de Travail.

Je ne répondrai pas en détails à chaque argument de M. Delahaye un par un, car j'ai le sentiment d'avoir trouvé le noeud de nos divergences d'opinion, et c'est donc à ce noeud que je veux m'attaquer en priorité. Après un court préambule, nécessaire à l'usage de définitions communes, j'exposerai pourquoi Preuve de Travail et Preuve d'Enjeu ne sont pas comparables. Cela traitera du même coup bon nombre des points développés par M. Delahaye, qui découlent de cette incompréhension. Pour les points qui resteraient, je les aborderai en fin d'article.

## Préambule

Il est utile, avant d'aller plus loin, de poser quelques définitions et rappeler quelques fait établis. Ce préambule est ainsi composé de deux sous-parties : la première rappelle sommairement la différence entre **validation** et **confirmation** de transactions au sein d'un réseau distribué ; la seconde définit les termes de **Preuve de Travail** et de **Preuve d'Enjeu**.

### Validation & Confirmation

Le réseau Bitcoin est composé de machines, appelées "noeuds", qui peuvent remplir différentes fonctions suivant leur type :
- les noeuds complets stockent l'intégralité du registre. Lorsqu'un nouveau bloc est proposé, ils en vérifient la validité, ce qui consiste notamment à s'assurer que l'ensemble des transactions qu'il contient sont bien valides (ie qu'elles suivent les règles du protocole), que le bloc est bien formé, et que la preuve de travail associée est également valide,
- les mineurs rassemblent les transactions en attente dans des blocs qu'ils tentent de faire accepter à l'ensemble du réseau. Chaque mineur travaille sur un bloc, qui peut être différent (i.e., contenir des transactions différentes) de celui de son voisin. Pour pouvoir proposer son bloc au reste du réseau, un mineur doit être le premier (parmi l'ensemble des mineurs) à trouver un nombre satisfaisant une condition bien précise. Sans rentrer dans les détails techniques, il suffit de se représenter que ce mécanisme ressemble fort à une loterie : le seul moyen de trouver ce nombre est d'en essayer beaucoup, au hasard, en espérant trouver le bon. C'est ce processus, précisément, qui consomme de grandes quantités d'énergie lorsques des milliers de mineurs s'y adonnent.

Une fois qu'un mineur a trouvé un nombre satisfaisant la condition, il l'ajoute à son bloc et publie le tout. Tous les autres noeuds (mineurs ou noeuds complets) en vérifient alors la validité. Notamment, si le nombre trouvé satisfait bien la condition requise, c'est la preuve que le mineur a dépensé de l'énergie pour le trouver : la fameuse preuve de travail. Dès lors (et sous réserve que tout le reste dans le bloc soit également valide), tous les noeuds acceptent ce bloc comme étant la nouvelle page du registre et l'ajoutent à leur propre version locale. Puis, les mineurs reprennent leur travail sur un nouveau bloc.

Il peut être intéressant de noter, et M. Delahaye le fait d'ailleurs, que le processus de validation en lui-même est très rapide et peu couteux en énergie. C'est le processus de sélection du prochain mineur autorisé à proposer son bloc qui est énergivore. Cependant, on trouve souvent le qualificatif impropre de "validateurs" pour parler des mineurs ou de leur "équivalent" dans les blockchains à Preuve d'Enjeu. Bien sûr, les mineurs valident les transactions avant de les ajouter dans leur bloc, mais simplement pour se prémunir d'y ajouter quelque transaction illicite vis-à-vis des règles du protocole, qui vaudrait à leur bloc d'être rejeté s'ils avaient la chance de gagner la loterie. La validation des transactions ne distingue donc pas les mineurs des autres noeuds, pas plus qu'elle ne distingue leur pendant à Preuve d'Enjeu des noeuds complets des réseaux PoS[^4].

Or, lorsqu'une transaction est ajoutée dans un bloc et ce bloc accepté, il est d'usage de dire qu'elle a été confirmée ; ou encore qu'elle a "reçu une confirmation". Puis, chaque bloc qui s'ajoute dans la chaîne au-dessus de ce bloc ajoute à la transaction une confirmation supplémentaire. Ainsi, car c'est une dénomination qui semble cohérente, et qui met bel et bien en exergue le rôle distinctif des mineurs et de leur homologues à Preuve d'Enjeu, nous désignerons les noeuds chargés de créer et publier les nouveaux blocs sous le terme de "confirmateurs" (ou simplement de "mineurs" pour le cas de Bitcoin et des blockchains à Preuve de Travail).

### Travail et Enjeu

La différence entre Preuve de Travail et Preuve d'Enjeu tient en premier lieu dans le critère de sélection du confirmateur ajoutant le prochain bloc.

- Dans la Preuve de Travail, il s'agit du mineur qui trouve le premier un nombre satisfaisant la condition requise. Puisque le seul moyen d'y parvenir et d'essayer autant de nombres que possible jusqu'à trouver, les chances de gagner la course d'un mineur sont proportionnelles à sa puissance de calcul.
- Dans la Preuve d'Enjeu, il s'agit d'un confirmateur sélectionné au hasard parmi l'ensemble des confirmateurs. Cependant, il n'y a pas un ticket par confirmateur : la probabilité pour un confirmateur d'être tiré au sort est proportionnelle au nombre de jetons de cryptomonnaie qu'il a mis en gage.

## PoW et PoS ne sont pas comparables

L'argument principal de M. Delahaye est que, la Preuve de Travail (PoW) et la Preuve d'Enjeu (PoS) parvenant au même résultat, il est moral de préférer la seconde, plus économe en énergie, à la première. Présenté ainsi, l'énoncé paraît peu discutable. Cependant, PoW et PoS ne sont pas si facilement comparables, car ils ne remplissent pas les mêmes objectifs et n'exhibent pas les mêmes propriétés.

### Protection face aux attaques Sybil

Le rôle commun de la Preuve de Travail et de la Preuve d'Enjeu est de protéger le réseau face aux attaques Sybil. Une attaque Sybil consiste pour un acteur malveillant à faire tourner de nombreux noeuds afin de simuler une multitude d'acteurs différents et d'en tirer parti. Imaginons par exemple que la probabilité pour un confirmateur d'être choisi ne soit pas proportionnelle à sa puissance de calcul ou à sa richesse mise en gage, mais que chaque confirmateur ait la même chance que tous les autres. Par exemple, chaque confirmateur a un ticket de loterie, et un gagnant est tiré au sort. Puisque le coût marginal de mettre en place un nouveau noeud est faible (et décroissant), des acteurs malicieux pourraient faire tourner des milliers de noeuds, obtenant ainsi des milliers de fois plus de chances d'être sélectionnés. C'est pourquoi le hasard pur, sans autre considération, n'est pas un bon outil face à la menace Sybil. D'où l'utilité des Preuves de Travail et d'Enjeu.

M. Delahaye, et c'est là un élément essentiel de sa thèse, prétend que la Preuve de Travail et la Preuve d'Enjeu parviennent aussi bien l'une que l'autre à assurer la protection face aux attaques Sybil. Nous admettrons pour l'instant ce point, avant de le discuter plus avant plus loin dans cet article. En effet, il est avant tout un aspect bien plus crucial qu'il importe de soulever.

Ce que M. Delahaye dit aussi, bien qu'implicitement, c'est que la seule fonction de la PoW et de la PoS est la protection face aux attaques Sybil. Si cela est vrai en première approximation, cette conception ignore cependant certains effets qui découlent d'une bonne protection face à Sybil, et sur lesquels PoW et PoS ne sont pas équivalents.

### Résistance à la censure

L'un de ces effets, d'une importance monumentale, est la résistance à la censure. On désigne sous ce terme la capacité d'un réseau à résister durablement à une prise de contrôle arbitraire qui censurerait ou filtrerait certaines transactions. Ce pouvoir décisionnaire est déjà acquis à certaines entités (étatiques ou privées) au sein des systèmes de paiement traditionnels et centralisés. Il est crucial pour les réseaux distribués que, quiconque parvenant à s'arroger ce droit pour un certain laps de temps, il en soit instament débouté. Autrement dit, ces réseaux doivent être résilients et, si un attaquant parvenait à obtenir une position au sein du réseau lui permettant en pratique de censurer des transactions, il faudrait qu'il lui soit impossible de s'y maintenir. Or, comme Eric Voskuil l'a démontré dans son {{<newtabref href="https://github.com/lugaxker/cryptoeconomics-FR-translation/blob/main/chapters/ch072-proof-of-stake-fallacy.md" title="Sophisme de la Preuve d'Enjeu">}} (ici traduit par Ludovic Lars[^5]) :

{{<blockquote>}}
La résistance à la censure dépend des personnes qui paient les mineurs pour vaincre le censeur. Vaincre la censure n’est pas possible dans un système de Preuve d'Enjeu, puisque le censeur a acquis la part majoritaire et ne peut pas être évincé. De ce fait, les systèmes de Preuve d'Enjeu ne sont pas résistants à la censure.
{{</blockquote>}}

Une fois qu'un acteur a amassé suffisamment de richesses pour être assuré d'être si souvent choisi pour proposer son bloc qu'il est en mesure de censurer des transactions, aucun retour en arrière n'est possible : il ne cédera pas d'unités de cryptomonnaies à d'autres ; et le seul moyen d'en obtenir de nouvelles, via les récompenses liées à la confirmation, il se l'est approprié pour lui seul.

Cela contraste singulièrement avec la Preuve de Travail, où un tel tyran peut être renversé en branchant de nouvelles machines. Le seul moyen pour l'attaquant de se maintenir serait d'augmenter encore davantage sa puissance de calcul (et donc sa consommation électrique). Sur le long terme, il serait obligé d'investir dans de nouvelles machines, de nouvelles infrastructures énergétiques, etc. Parce que le paramètre déterminant la probabilité de proposer le prochain bloc est exogène et coûteux, le réseau est protégé de la censure.

D'ailleurs, M. Delahaye le souligne lui-même très bien, croyant tenir là un argument contre la Preuve de Travail :

{{<blockquote>}}
La POW est une POS qui confisque les mises ! (...) La POS fait aussi bien que la POW (lutter contre les attaques Sybil) sans obliger un validateur à une dépense importante.
{{</blockquote>}}

Ce que M. Delahaye prend pour un défaut (la confiscation des mises et le coût qui s'ensuit pour le validateur) est en fait l'un des éléments essentiels permettant d'affirmer que Bitcoin est résistant à la censure. Sans ce coût continu exprimé dans une unité externe (l'énergie), le censeur peut se maintenir indéfiniment. Avec le coût externe (en énergie et en investissements), le censeur peut être renversé à tout moment.[^6]

Une question qu'il est pertinent de se poser à ce stade, est de savoir si la Preuve d'Enjeu ne dispose pas d'un autre mécanisme lui permettant d'être résistante à la censure. Aussi étonnant que cela puisse paraître, la réponse est non. Certains arguent qu'à mesure qu'un acteur achète sur le marché des unités de cryptomonnaie afin de se constituer un capital à même de lui permettre de contrôler une part significative de la masse monéraire, le prix augmente en conséquence, rendant la tâche ardue, voire impossible. Je crains qu'il ne s'agisse malheureusement d'une mauvaise estimation du modèle de menace. Un acteur qui souhaiterait se rendre censeur d'un réseau distribué aurait en effet, selon toute vraisemblance, des outils à sa disposition lui permettant d'acquérir à un coût raisonnable les montants requis : saisies ou injonctions auprès des grandes plateformes qui ne manquent pas de se former dans les environnements à Preuve d'Enjeu, impression monétaire, etc.

### Conclusion

L'erreur principale que commet M. Delahaye est de considérer la PoW et la PoS uniquement au prisme de la protection face aux attaques Sybil. Or, comme nous l'avons montré, ce cadre d'analyse est trop réducteur. La résistance à la censure est la propriété fondamentale de Bitcoin, nécessaire à l'expression de ses autres propriétés. Elle n'est donc pas négociable, et seule la Preuve de Travail permet aujourd'hui d'en assurer l'existence et le maintien. C'est là l'utilité première de cette-dernière.

Les détracteurs de Bitcoin pourront arguer qu'un tel système, résistant à toute censure, n'est pas nécessaire, voire n'est pas souhaitable. C'est une opinion qu'il leur est possible d'avoir et de défendre, mais cela reste une opinion. De même, ma conviction qu'un tel système est absolument nécessaire pour une société libre reste une opinion (que je crois toutefois de plus en plus étayée, comme en témoignent les récents événements au Canada par exemple).

Le débat sur l'utilité de Bitcoin et de sa Preuve de Travail est donc une discussion philosophique sur le type de société dans laquelle chacun souhaite vivre. Il ne s'agit pas de la controverse technique à laquelle M. Delahaye a voulu le ramener comme, je le crois, cette première partie vient de le démontrer.

{{<paybutton text=" 💪 Soutenir mon Travail " color="#1da1f2">}}

## Autres considérations

Dans cette seconde partie, je m'attacherai à traiter des points soulevés par M. Delahaye qui ne sont pas déjà adressés par la première. Ce traitement ne se vaut pas exhaustif, et je renvoie le lecteur au tableau en annexe de cet article s'il souhaite un aperçu rapide, point par point, des contre-arguments apportés aux assertions de M. Delahaye.

### Décentralisation

Qui s'est déjà un tant soit peu penché sur la question du minage de Bitcoin n'a pas pu s'empêcher de remarquer une certaine concentration de la puissance de calcul entre quelques coopératives de minage (*mining pools* en anglais) seulement. C'est ce qui était généralement exprimé par l'idiomatique "tout est centralisé chez quelques mineurs en Chine" que certains répétaient à l'envi avant l'Exode.

Cette remarque appelle deux commentaires : le premier concernant le sens à placer derrière la notion de *décentralisation* ; le second relatif à la nature des coopératives de minage susmentionnées.

La notion de décentralisation dans les réseaux monétaires distribués n'est pas simple à appréhender, et il est aisé de se méprendre. Que cherche-t-on à décentraliser exactement ? Une réponse possible est que nous cherchons à décentraliser le pouvoir exécutif d'ordonnancement des transactions. En effet, dans le whitepaper de Bitcoin, Satoshi Nakamoto écrit que la Preuve de Travail permet d'établir un *serveur d'horodatage distribué* en pair-à-pair. Ce serveur distribué se substitue aux traditionnels serveurs centralisés en usage jusqu'alors et qui agissaient comme source de vérité quant à l'ordre des transactions.

Si l'on considère la décentralisation par cet unique prisme, alors la centralisation du minage entre quelques coopératives peut être une source légitime d'inquiétude. Une coopérative de minage est le résultat de la coordination de plusieurs mineurs qui travaillent de concert et se partagent les récompenses éventuellement obtenues, afin de bénéficier de certains avantages comme une réduction de la variance des gains ou la {{<newtabref href="https://github.com/lugaxker/cryptoeconomics-FR-translation/blob/main/chapters/ch036-proximity-premium-flaw.md" title="prime de proximité">}}. Une telle coopérative fonctionne généralement avec un coordinateur qui distribue le travail et les récompenses aux membres. Or, même si les mineurs sont, en théorie, individuellement libres de changer de coopérative à tout instant, voire de miner en solitaire, il n'est pas évident qu'ils fassent ce choix, même en cas de prise de contrôle de la coopérative par une entité, si leur intérêt économique est d'y demeurer[^7].

Une analyse grossière peut pousser à croire que la Preuve d'Enjeu est exempte de ce problème de concentration, et qu'elle est donc plus décentralisée que la Preuve de Travail. Cet écueil est lié à une mauvaise estimation des raisons qui poussent les mineurs à s'associer en coopératives. J'ai déjà cité deux de ces raisons (réduction de la variance et premium de proximité), auxquelles ont peut par exemple ajouter les éventuelles économies d'échelle, ou encore une plus grande résilience face aux variations de marché. Or, toutes ces raisons sont encore présentes dans un système de Preuve d'Enjeu. Pire, de nouvelles pressions de concentration (ie de nouvelles raisons de former des coopératives) peuvent apparaître dans ce-dernier, comme par exemple lorsqu'un montant minimum est requis pour paritciper à la confirmation des transactions, incitant les petits porteurs à se fédérer pour dépasser cette limite.

Les pressions de concentration ne diffèrent donc pas entre la Preuve de Travail et la Preuve d'Enjeu par leur nature, mais (éventuellement) par leur degré. Il est ainsi admissibles que les économies d'échelles soient moins importantes dans un système PoS que dans un système PoW, quoique cela dépende fortement des caractéristiques minimales requises pour opérer un noeud confirmateur dans un système PoS donné.

De plus, il est possible d'arguer que la structure incitative de la Preuve d'Enjeu rend la confiscation, et donc la prise de contrôle, plus aisée. En effet, les mêmes pressions de concentration qui poussent certains participants à mettre en commun leurs jetons dans un système PoS les incite également à confier ces jetons à des intermédiaire de confiance, comme les plateformes d'échange par exemple, afin de bénéficier de meilleurs rendements (souvent en raison de frais moins élevés). En témoigne par exemple la répartition des validateurs d'Ethereum 2.0 (en test), avec près de 10% des ethers stakés par une seule plateforme (Kraken). [^8].

Or, même s'il n'est pas certain que des mineurs quitteraient leur coopérative si cette dernière devenait hostile à une certaine conception de l'intérêt général, il leur serait en tout cas beaucoup plus facile de le faire que pour leurs homologues à Preuve d'Enjeu qui auraient déposé leurs fonds auprès d'un tiers. En effet, il suffit pour les mineurs de rediriger leur puissance de calcul ailleurs - un simple changement de configuration sur leur machine - tanids que les possesseurs de jetons se verraient répondre avec fermeté que les retraits sont suspendus.

Ainsi, si l'on juge que la Preuve de Travail présente un risque de centralisation important en raison des pressions de concentration qui s'y exercent, encore faut-il appliquer avec rigueur le même raisonnement à la Preuve d'Enjeu, pour constater que les mêmes pressions y existent, et que leurs effets sont potentiellement plus durs à modérer.

### Impact environnemental et sociétal

L'autre critique si souvent adressée à la Preuve de Travail est son impact environnemental. Une réponse détaillée serait certainement l'objet d'un article complet, voire d'un meta-article. Une réponse plus condensée tient en quelques considérations :

1. Toute activité humaine a un impact environnemental et sociétal. Quand vous prenez le bus. Quand vous vous brossez les dents. Quand vous regardez Netflix en attendant que le sèche-linge ait fini de tourner. Cet impact est toujours à comparer avec les bénéfices apportés par cet activité.

2. L'utilité de Bitcoin est de fournir un protocole monétaire et de paiement ouvert, sans-permission, équitable et résistant à la censure.

3. La consommation de Bitcoin est souvent comparée à celle d'un pays comme la Suède. Pour avoir à l'esprit un ordre de grandeur tout aussi dénué de sens, il est amusant de constater que cela correspond par exemple à la consommation annuelle d'un tiers des sèches-linges aux Etats-Unis.

Si le lecteur acquiesce à la proposition 1., la question est de savoir s'il reconnaît que la proposition 2. justifie la consommation énergétique présentée en 3. Pour alimenter cette réflexion, je conseille au lecteur l'excellent {{<newtabref href="https://medium.com/@AlexStach/manuel-de-survie-dans-la-jungle-des-poncifs-anti-bitcoin-version-longue-523e381745ff" title="manuel de survie">}} écrit par Alexandre Stachtchenko. Encore une fois, il s'agit d'une réflexion philosphique et éthique, à la fois propre à chacun et véritable débat de société. En aucun cas d'une question d'ordre purement technique, comme nous l'avions déjà souligné en conclusion de la première partie.

Enfin, il y a un véritable questionnement à avoir sur la prétendue inocuité environnementale des protocoles à Preuve d'Enjeu. Ce sera sûrement l'affaire d'un prochain article, mais face à la multiplication de ces projets, dont certains à l'éthique douteuse, lors de la récente euphorie de marché, le sujet d'un éventuel "Effet Rebond" se pose.

## Annexe - tableau récapitulatif

Ce tableau permet au lecteur qui chercherait à peser les arguments de M. Delahaye d'y trouver, pour chaque argument, numéroté selon la nomenclature de M. Delahaye, mes observations éventuelles. Mon souhait est que ces remarques permettent d'enrichir le débat et de nourrir la réflexion de chacun.

| Argument | Résumé | Observations |
|--|------------|------------|
|A | Pow et PoS font la même chose, mais la PoS le fait de manière plus économique/écologique | Traité dans la [première partie](#pow-et-pos-ne-sont-pas-comparables). |
|B1|Le minage incite au vol d'électricité|Le vol d'électricité est en effet condamnable, quelle que soit l'utilisation qui est faite de cette énergie par la suite. Tout comme les *ransomwares*, même si dans une moindre mesure, Bitcoin rend plus facilement rentable une activité qui existait de toute façon avant lui. Il ne faut donc y voir que l'adoption par les criminels de meilleurs outils, qu'il serait vain de rendre illégaux puisque les criminels, par définition, agissent déjà dans l'illégalité. La solution n'est donc pas d'interdire Bitcoin ou la PoW, mais de renforcer la sécurité de l'approvisionnement électrique, tout comme le monde de l'IT a pris conscience de la menace cyber.|
|B2|Le minage incite au vol de puissance de calcul|Même réponse que pour B1.|
|B3|"La POW contribue à la pénurie de composants électroniques" |Pas plus que d'autres industries. Il s'agit encore une fois de comprendre l'utilité de la PoW, mise en évidence dans la première partie. Il faut d'ailleurs noter que, contrairement à ce qu'indique M. Delahaye, bon nombre de réseaux PoS requièrent des machines puissantes et dédiées pour les noeuds confirmateurs.[^9]|
|B4|"Les validateurs doivent vendre une partie de leurs gains pour payer les coûts du minage", ce qui influence négativement le cours en créant une pression vendeuse.|La pression acheteuse suffit largement à absorber ces ventes, lorsqu'elles ont lieu. De plus, la dynamique à cet égard semble avoir considérablement changé, avec des mineurs qui vendent de moins en moins les bitcoins minés, maintenant qu'ils ont accès à d'autres sources de financement. Argument non étayé par les faits.|
|B5|Lorsque le cours augmente, miner du Bitcoin devient d'autant plus rentable (hors *halving*) et la puissance de calcul totale du réseau augmente en conséquence. Or, comme cela n'est possible que dans une certaine mesure, la croissance du prix du Bitcoin s'en trouve bornée.|Oui. Il ne me paraît pas absurde que la monnaie, dans un monde fini, soit bridée par la physique de ce monde. C'est malheureusement une réalité de laquelle les monnaies fiduciaires nous ont éloigné.|
|B6|La Pow, en concentrant l'attention sur l'attaque des 51%, tend à dissimuler les autres risques.|Subjectif et non établi par des faits.|
|C1|Ce n'est pas parce que le minage de Bitcoin utilise des énergies renouvables qu'il ne pollue pas.|Correct, toute énergie produite est une pollution, à mettre en regard avec ses bénéfices. Il faut de plus noter que Bitcoin utilise également une part croissante d'énergie gaspillée, qui elle ne coûte rien à consommer, économiquement ou environnementalement parlant.|
|C2|Certains acteurs se détournent de la PoW au profit de la PoS, en raison de la pollution engendrée par la première.|Sophisme *ad verecundiam*.|
|C3|Le minage a pu créer des pannes électriques.|Il est tout à fait envisageable que le minage soit en cause dans certains désordres sur des réseaux électriques. Le minage peut cependant également s'avérer très utile dans la stabilisation des ces-derniers. D'où l'importance d'un dialogue et d'un travail commun entre producteurs d'énergie et mineurs, comme pour toute industrie électro-intensive.|
|C4|"Les usines de minage créent des troubles dans leur environnement immédiat."|Certains des exemples cités ici ont été débunkés. M. Delahaye indique par exemple que certaines installations ont conduit à "chauff[er] l’eau de certains lacs au États-Unis", indiquant en source un article du Figaro qui précise pourtant que l'eau du lac en question est restée égale aux normales de saison. Ce qu'un simple raisonnement sur les ordres de grandeur aurait d'ailleurs pu nous apprendre.|
|C5|Dans certaines zones, le minage a pu conduire à une augmentation des prix.|Cet argument n'est malheureusement étayé que par une seule source. S'il est avéré, la réponse est similaire à celle du point C3.|
|C6|La PoS permet une bien meilleure décentralisation que la PoW car elle ne requière pas l'achat de machines coûteuses.|Ce point mérite une réponse en plusieurs phases. Premièrement, la décentralisation d'un réseau ne se mesure pas qu'à la seule décentralisation de ses noeufs confirmateurs, mais également à celle de ses noeuds validateurs. Le chiffre de 15000 noeuds Bitcoin présentés par M. Delahaye correspond d'ailleurs à un sous-ensemble des noeuds validateurs, et non aux noeuds confirmateurs (improprement désignés par le qualificatif de "validateurs" par M. Delahaye). Le nombre réel de noeuds validateurs Bitcoin est d'ailleurs supérieur à 15000, suivant les estimations, faisant de Bitcoin de loin le réseau le plus décentralisé. De plus, il est abusif de prétendre que la PoS permet une plus grande décentralisation des noeuds confirmateurs, surtout lorqu'on prend en considération, suivant les réseaux, les quantités de fonds à mettre en gage ou les caractéristiques du matériel requis.|
|D1|L'équivalent de milliards de dollars sont sur des réseaux PoS comme Solana ou Cardano, prouvant ainsi leur sécurité. |En période d'euphorie de marché, la capitalisation atteinte par certains projets ne permet pas de déduire quoi que ce soit quant à leur sous-jacent technique. En outre, dans bon nombre de ces projets, une bonne partie de la masse monétaire est sous le contrôle de quelques entités liées de près ou de loin à l'équipe de développement. Enfin, de nouveaux papiers de recherche mettent régulièrement en évidence des failles affectant des protocoles PoS de premier plan[^10].|
|D2|"Les nouvelles blockchains n’utilisent jamais la PoW"|Non factuel et ne démontrant rien. La PoS est à ce cycle de marché ce que les ICOs étaient au précédent : un moyen simple de distribuer un token initialement sans valeur, et de générer à moindre coût un ersatz d'effet de réseau.|
|D3|Ethereum va passer en PoS.|Sophisme *ad verecundiam*. Et on permettra également aux sceptiques de douter quant au passage d'Ethereum à la Preuve d'Enjeu en 2022.|
|E1|Certains promoteurs de la PoW prétendraient que : « La dépense électrique massive de la POW sécurise des attaques 51 % et fournit donc une protection parfaite dans le cas du réseau Bitcoin. »."|Je n'ai jamais entendu personne dire cela.|
|E2|Certains promoteurs de la PoW prétendraient que : "« Il est normal que la sécurisation ait un coût. L’absence d’un tel coût important pour la sécurisation des réseaux POS montrent qu’ils sont moins bien protégés que les réseaux POW »."|J'ai déjà pu entendre ou lire des sophismes approchant celui-ci. M. Delahaye a ici raison de le souligner. Mais cela n'est pas un argument en faveur de la PoS, ni même contre la PoW... On frise ici l'argument *ad auditores*. Je n'insiste pas !|
|E3|La PoW a beau utiliser des surplus électrique, ce n'est pas vertueux pour autant car toute énergie produite est polluante. Il faudrait donc plutôt en finir avec les surplus. |J'accorde à M. Delahaye que, dans un monde parfait, il n'y aurait aucun surplus électrique, l'énergie serait disponible au bon moment, au bon endroit et en bonne quantité. Cependant, en pratique, il est nécessaire de s'accomoder de la physique, et donc bien souvent de surdimensionner des installations pour faire face à des pics de consommation, ou encore parce qu'on anticipe une hausse démographique, etc. Il est également important de ne pas projeter le réseau électrique français ou européen comme vérité universelle : bon nombre de réseaux dans le monde bénéficient de l'effet stabilisateur de la demande pilotable des mineurs de Bitcoin.|

\
Vous avez trouvé cet article intéressant ? Partagez-le autour de vous ! Et si le coeur vous en dit, n'hésitez pas à glisser une piécette dans le chapeau.

{{<paybutton text=" 🎩 Chapeau ! " color="#1da1f2">}}


[^1]: Ce long {{<newtabref href="https://institut-rousseau.fr/les-arguments-en-faveur-de-la-preuve-denjeu-pos-et-contre-la-preuve-de-travail-pow-pour-les-chaines-de-bloc/" title="papier">}} publié par l'Institut Rousseau, et cette {{<newtabref href="https://lejournal.cnrs.fr/billets/le-reseau-bitcoin-une-erreur-follement-couteuse" title="tribune">}} publiée dans Libération et par le Journal du CNRS.

[^2]:Si ce sujet intéresse le lecteur, je le renvoie vers l'analyse qu'en fait le Professeur de Philosophie {{<newtabref href="https://twitter.com/thetrocro" title="Troy Cross">}} au micro de {{<newtabref href="https://anchor.fm/daniel-prince6/episodes/thetrocro---A-Philosopher-Talks-Bitcoin--234-e1ec98b" title="Daniel Prince">}}.

[^3]: Ils témoignent en tout cas d'une bonne compréhension du fonctionnement technique de la Preuve de Travail, bien que certains arguments me paraissent discutables, tandis que d'autres n'apportent rien au débat.

[^4]: Si tant est qu'il en existe.

[^5]: Pour la version originale en anglais, voir {{<newtabref href="https://github.com/libbitcoin/libbitcoin-system/wiki/Proof-of-Stake-Fallacy" title="Proof of Stake Fallacy">}}.

[^6]: Il est tout à fait possible qu'il soit ardu de supplanter la puissance de calcul du censeur, si celle-ci est très importante. Le point crucial à comprendre ici est que, dans un système PoS, une fois que le censeur est en place, il est impossible à évincer **en théorie et en pratique** en conservant intactes les règles de consensus préxistantes, car il reçoit tous les nouveaux jetons dont les acteurs souhaitant le renverser auraient besoin pour le supplanter. Avec la PoW, le censeur a beau recevoir également les récompenses de bloc, cela ne lui est d'aucune utilité pour se maintenir au pouvoir puisque le coût pris en compte dans l'attribution des chances de confirmer un bloc (l'énergie) est externe au système.

[^7]: Voir {{<newtabref href="https://github.com/lugaxker/cryptoeconomics-FR-translation/blob/main/chapters/ch045-cockroach-fallacy.md" title="Sophisme du Cafard">}}.

[^8]: Il est également utile de noter qu'une part non négligeable de la masse monétaire reste concentrée entre quelques acteurs, tandis que la part de la masse monétaire réprésentée par les ethers préminés représente toujours plus de 50% du total. Un avantage qui, s'il est bénin dans un système PoW, prend tout à coup un éclairage bien différent sur un réseau en PoS.

[^9]: Voir par exemple la documentation de {{<newtabref href="https://docs.solana.com/running-validator/validator-reqs" title="Solana">}}.

[^10]: Voir par exemple le dernier {{<newtabref href="https://arxiv.org/abs/2203.01315" title="papier">}} en date, publié début mars 2022.