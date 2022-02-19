---
title: "AOPP: tout un fromage ?"
date: 2022-01-28T20:00:00+01:00
cover:
    image: "../images/aopp_meme.jfif"
    alt: "meme"
    caption: "Credits: @Loic_Psyduck"
    relative: false
tags: ["bitcoin", "régulateurs"]
categories: ["articles"]
draft: false
---

Une discussion (enflammée) sur un point de réglementation et son application s'est rapidement propagée sur Bitcoin Twitter entre hier et aujourd'hui, à la suite d'un Tweet de shaquille o'atmeal (@crypt0e):

{{< tweet user="crypt0e" id="1486782623930150913" >}}

J'ai trouvé le sujet suffisamment intéressant pour décider de rassembler mes idées à son égard dans un article. J'espère qu'il permettra aussi au lecteur d'y voir plus clair, et de bien en mesurer les enjeux.

## Un peu de contexte

Dans certaines juridictions (la Suisse et les Pays-Bas), les plateformes d'échange et assimilés (souvent appelées VASP dans le jargon, pour *Virtual Asset Service Provider*, l'équivalent international de nos Prestataires de Service sur Actifs Numériques) sont obligées par la loi de s'assurer que leurs utilisateurs retirent bien leurs fonds sur des adresses qui leur *appartiennent*. Cette obligation est "atteinte" en pratique en demandant à l'utilisateur de signer un message spécifique (quelque chose comme "Je soussigné, Fanis Michalakis, certifie posséder l'adresse bc1...") avec la clé privée associée à l'adresse sur laquelle il souhaite retirer.

La justification officielle pour cette curieuse réglementation est, comme à l'accoutumée, la lutte contre le financement du terrorisme et le blanchiment d'argent. Bien entendu, à l'instar du *KYC*, cette mesure est résolument inefficace contre ces deux maux, mais permet aux États d'assoir efficacement leur emprise et de paver la voie à une société de surveillance de masse. Il est par ailleurs intéressant de noter que cette mesure précise ne prouve absolument rien quand à la *possession* de l'adresse de retrait, puisqu'il est on ne peut plus simple pour l'utilisateur de demander à la tierce partie à laquelle elle appartient, le cas échéant, de signer quelque message que ce soit. L'inefficacité d'une loi n'est cependant pas une excuse pour sa mise en place.

## AOPP

Cette friction supplémentaire au moment du retrait pourrait freiner certains utilisateurs dans leur élan vers la garde propre (*self custody*) de leurs fonds, ce qui serait immensemment regrettable. Ainsi, {{<newtabref href="https://www.21analytics.ch/" title="21analytics">}}, un éditeur de logiciel suisse spécialisé dans la crypto-régulation, a initié le procole AOPP : *Address Ownership Proof Protocol* (Protocole de Preuve de Possession d'Adresse).

L'objectif est de permettre aux *wallets* de proposer un moyen simple et rapide de fournir cette preuve aux VASP. Si le portefeuille d'un utilisateur et la plateforme qu'il utilise supportent tous deux AOPP, alors l'utilisateur peut générer une preuve d'un simple clic sur le site du VASP. Ce clic ouvrira en effet automatiquement le *wallet*, qui signera le message voulu avec la clé privée appropriée, et l'enverra directement au VASP. On passe ainsi d'un processus fastidieux (copier et coller le message, le signer avec la bonne clé privée dans un logiciel le permettant, copier et coller le message signé) à un mécanisme de vérification en un clic.

```kd
+-------------+                         +--------+                           +---------------+
|             |-- clic sur un bouton -->|  Site  |--- message et adresse --->|    Wallet     |
| Utilisateur |                         |   du   |                           |      de       |
|             |<---------- OK ----------|  VASP  |<--- message signé avec ---| l'utilisateur |
+-------------+                         +--------+    la clé priv. corresp.  +---------------+
```

Pour que ce protocole fonctionne, il faut qu'au moins quelques portefeuilles l'implémentent. Certains le font : des *software wallets* comme BlueWallet ou Sparrow, et des *hardware wallets* comme Trezor. Les plateformes suisses et néerlandaises (comme Relai par exemple) peuvent également implémenter le protocole afin que leurs utilisateurs puissent bénéficier d'une vérification en un clic.

## Quel est le problème ?

Tout ce que fait ce protocole semble donc être de permettre d'appliquer plus facilement une loi qui doit de toute façon l'être (si l'on souhaite rester dans la légalité). L'implémenter paraît donc une bonne idée, puisque cela permet de réduire la friction vers la *self custody*. D'ailleurs, je crois que ce sont ces considérations qui ont conduit à l'élaboration de ce protocole et à son adoption par certains VASP et portefeuilles.

Cependant, cette loi et son application rendent tangible l'idée, farouchement opposée à l'ethos de Bitcoin, selon laquelle il faudrait obtenir *la permission* d'assurer soi-même la garde de ses propres fonds. Et qui dit permission, dit refus potentiel. Cette réglementation devrait donc être combattue, plutôt que d'en faciliter l'application. Si les utilisateurs souhaitent s'y conformer, qu'il en soit ainsi, mais les solutions de garde propre, qu'elles soient matérielles ou logicielles, se doivent de rester neutres en la matière. Ce point de vue est remarquablement détaillé dans ce thread de Samourai :

{{< tweet user="SamouraiWallet" id="1486771410949357571" >}}

Depuis, {{<newtabref href="https://twitter.com/SparrowWallet/status/1486785866739728386" title="Sparrow">}}, {{<newtabref href="https://twitter.com/bluewalletio/status/1486805550608392194" title="BlueWallet">}} et {{<newtabref href="https://twitter.com/Trezor/status/1487091879883722755" title="Trezor">}} ont tous annoncé se retirer de l'initiative, et retirer les fonctionnalités liées au protocole de leurs produits dans leurs prochaines *releases* respectives.