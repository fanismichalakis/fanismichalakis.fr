---
title: "Bitwage Annonce le Premier Paiement d'un Salaire via Lightning"
date: 2021-12-07T21:55:46+01:00
tags: ["lightning", "bitcoin"]
categories: ["logs"]
draft: false
---

Bitwage a annoncé aujourd'hui avoir effectué le tout premier paiement de salaire sur le réseau Lightning.

{{< tweet user="Bitwage" id="1467874344026230799" >}}

Personnellement, j'ai trouvé la nouvelle assez intéressante, car l'idée d'être payé, non seulement en Bitcoin, mais aussi sur le Lightning Network, ouvre la voie à quelques considérations *intrigantes*.

Se faire payer en Bitcoin a de bons côtés . C'est accrocheur, amusant à dire lors des réunions de famille, et cela protège de l'inflation et de la censure. Cela peut avoir ses inconvénients (à court terme), en particulier lorsque tout ce qui vous entoure est toujours évalué en bons vieux dollars. Mais c'est plutôt cool.

Si de plus en plus de gens commencent à être payés en bitcoins, nous pourrions commencer à voir un peu de trafic sur la chaîne de bitcoins à la fin du mois. Chaque entreprise envoie à ses employés leur salaire à peu près au même moment, que ce soit mensuellement ou hebdomadairement. Conséquence néfaste : file d'attente, retards, mempool surchargé. La seule idée de devoir attendre que le mempool se vide pour pouvoir recevoir son salaire semble *étrange*. C'est là qu'intervient Lightning.

Avec Lightning, vous pouvez recevoir votre salaire hors chaîne et indépendamment des conditions de trafic de la chaîne (par exemple, si le mempool est surchargé ou non) tant qu'il y a une route entre vous et votre employeur, et que cette route a suffisamment de liquidité dans la bonne direction (par exemple, allant de votre employeur vers vous).

De plus, on peut même imaginer utiliser le même canal chaque mois, encore et encore :
1. L'employé reçoit son salaire. Après cela, la capacité entrante de son canal est épuisée : il ne peut plus beaucoup recevoir.
2. L'employé paie ses dépenses tout au long du mois. Chaque dépense prend de la capacité sortante (ce qu'il peut envoyer) et pousse vers la capacité entrante du canal (ce qu'il peut recevoir). Par conséquent, à chaque dépense, la capacité de réception de l'employé augmente.

De cette façon, il serait **théoriquement** possible d'utiliser *Bitcoin over Lightning* sans plus jamais toucher la chaîne, en recevant son salaire avec le même canal chaque mois, et en dépensant à partir de ce même canal pendant le mois. Cela fonctionne tant qu'il y a suffisamment de capacité entrante chaque mois pour que le salaire soit payé[^1]. Par exemple, si l'employé dépense exactement ce qu'il reçoit chaque mois, cela peut fonctionner à l'infini.

Maintenant, deux choses me viennent à l'esprit :
- cela ne laisse pas beaucoup de place pour l'épargne
- qu'en est-il des frais ?

En ce qui concerne les économies, il y a plusieurs possibilités.

Par exemple, le canal que l'employé utilise pour recevoir son salaire pourrait être suffisamment important pour qu'il faille dix ans pour que la capacité entrante soit totalement épuisée, compte tenu des habitudes d'épargne de l'employé. Mais cela semble être une allocation de capital plutôt inefficace.

Sinon, les liquidités pourraient être *naturellement* dirigées vers l'autre côté du canal par le biais du routage.

Ou l'employé pourrait utiliser une sorte de *swap atomique Lightning <--> on-chain* pour épargner en Bitcoin tout en gardant suffisamment de liquidités entrantes pour obtenir son prochain salaire :
1. L'employé reçoit son salaire.
2. L'employé dépense une partie de son salaire pour payer ses dépenses.
3. L'employé envoie le reliquat à un service d'échange et reçoit en échange des BTC on-chain pour l'épargne à long terme. De cette façon, la liquidité sur le canal sera du bon côté pour recevoir le prochain salaire.

Les salaires en Bitcoin via Lightning pourraient même être une force motrice importante dans l'émergence de services d'échange et de marchés P2P, où les utilisateurs disposant de fonds excédentaires sur Lightning et désireux de les échanger contre des fonds on-chain (les épargnants) échangeraient avec des utilisateurs souhaitant augmenter leur bande passante sur le réseau Lightning (les dépensiers).

Enfin, un autre aspect intéressant du paiement de salaire sur Lightning est qu'il a le potentiel de redéfinir l'échelle de temps à laquelle le versement se produit. Pourquoi attendre un mois entier pour recevoir son salaire ? Pourquoi pas tous les jours ? Ou toutes les heures ? Avec Lightning, nous pouvons le faire sans risquer d'encombrer la blockchain. Et si le paiement circule dans un canal direct entre l'employeur et l'employé[^2], il n'y a aucun coût supplémentaire (hormis les frais administratifs).

Si je devais faire une supposition, je dirais que nous avons à peine effleuré la surface de ce que le paiement par Lightning implique, tant en termes d'innovation que de défis.

[^1]: Bien sûr, tout se complique lorsqu'il y a des intermédiaires supplémentaires entre l'employeur et l'employé sur le réseau, car chaque saut doit également avoir sa liquidité bien positionnée pour que cela fonctionne.

[^2]: Est-ce une bonne idée ? Cela signifierait zéro frais, mais cela signifierait aussi que l'employé devrait passer par le nœud de l'employeur pour dépenser son salaire.