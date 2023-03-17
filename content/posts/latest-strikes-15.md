---
title: "Latest Strikes 15"
date: 2022-12-21T19:15:00+01:00
block: "768387"
cover:
    image: "../images/trading-bitcoin-p2P-dalle.min.png"
    alt: "Two men are trading Bitcoin peer-to-peer in a city street at night."
    caption: "'Trading Bitcoin P2P'. Generated with DALL·E."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
draft: false
---

A new LNBits release, a promising vision and builders keeping on building: that was Lightning last week. Read further to find out more, and remember: if you want to receive your weekly recap in your inbox before anyone else, all you have to do is subscribe {{<newtabref href="https://blog.lnmarkets.com" title="here">}}. Ready? Steady. Go!

## Ecosystem

### Breez Raises $4.5M

Breez {{<newtabref href="https://nitter.net/Breez_Tech/status/1602650058524332039" title="raised">}} 4.5 million dollars in a seed round led by {{<newtabref href="https://egodeath.capital/" title="ego death capital">}} and {{<newtabref href="https://entreecap.com/" title="Entrée Capital">}}, which will help Breez realize it's ambitious vision of a trustless yet frictionless mobile Lightning experience for all users.

The focal point of Breez's vision is that users should be able to spend and use their money in the least-friction way - that is, P2P. Middle men and regulators introduce a kind of friction that Lightning removes, but non-custodial Lightning (eg. the only Lightning implementation safe from middle men and regulators intrusion) comes with it's own drag forces.

That's what Breez will be trying to address though the combination of the Breez SDK and the Greenlight API, allowing app creators to easily integrate Lightning payments into their apps in a non-custodial way. The big difference with the way Breez works today is that the Lightning node itself will not be in the phone anymore, but rather on a remote server. The private keys, however, remain on the user's phone, thus reducing the trust required and ensuring LSPs remain only LSPs - and do not become banks, with all the inherent risks and regulations.

### Grants

The {{<newtabref href="https://hrf.org" title="Human Rights Foundation">}} dropped a 2 million sats {{<newtabref href="https://nitter.lacontrevoie.fr/gladstein/status/1605226003990605824" title="gift">}} to support Bitcoin development, education and communities. Lightning-wise, it includes a $25,000 {{<newtabref href="https://nitter.lacontrevoie.fr/gladstein/status/1605226016456159232" title="grant">}} to Dusty for his work on splicing.

### Sats Streaming Now Avaible In Podverse (Beta)

Podcast player Podverse {{<newtabref href="https://nitter.lacontrevoie.fr/Podverse/status/1604885344293425152" title="launched">}} (still experimental) support for Value for Value in the app. You can now send sats to your favorite shows, by enabling the feature and connecting your Podverse app to a Lightning wallet (right now, only Alby is supported, thanks to their great API).

For now, you can "only" send Boosts and Boostagrams, which are one time payments. In other words, you can't really automatically stream sats every minute just yet, but rather send a payment from time to time to show your appreciation or send feedback to the podcaster, without leaving the podcasting app.

If you already have an {{<newtabref href="https://getalby.com/login" title="Alby account">}}, you can use it in Podverse by logging in (for example using LNURL-Auth). Please note that an Alby account is a custodial wallet of its own, it's different from using Alby connected to your node or an LNBits instance, for example.

### Lucent Labs Make You Love Bitcoin ~~Cash~~ Cache

{{<newtabref href="https://www.lucentlabs.co" title="Lucent Labs">}} announced two {{<newtabref href="https://nitter.net/LucentLabz/status/1602376904111161345" title="new tools">}} to make the life of Bitcoin and Lightning operators easier: Bolt Node and Bitcoin Cache.

Bolt Node appeals to Bitcoin/Lightning operators running huge infrastructure at scale, and allow them to automate deployments using templates. From what I understand, it looks a bit like Ansible, but specialized in Bitcoin infrastructure deployment.

Bitcoin Cache is a "secure bitcoin treasury infrastructure", helping Lucent Labs's customers secure their organization's private keys, create proof of reserves or recover funds (if the worst was to happen).

## Wallets & Tools

### Alby

Alby {{<newtabref href="https://nitter.lacontrevoie.fr/getAlby/status/1602676428952281088" title="announced">}} the integration of MoonPay into its browser extension, allowing users to top up their Alby accounts with their dirty fiat.

Last week, Bumi also shared a {{<newtabref href="https://nitter.net/Bumi/status/1603459266026913792" title="sneak peek">}} showing how you can build a channel management frontend in the browser using Alby and the power of {{<newtabref href="https://webln.dev" title="webln">}}. Kinda cool, and reminded me of this {{<newtabref href="../latest-strikes-11/#new-alby-release" title="demo">}} they made of opening dual-funded channels directly from the browser.

### Wider LNURL-Auth Usage

LNURL-Auth is going places! Geyser {{<newtabref href="https://nitter.lacontrevoie.fr/geyserfund/status/1559485913595580424" title="added">}} it as an authentication mechanism, with the nice feature of being able to link multiple wallets to the same profile.

A LNURL-Auth plugin for Wordpress was also {{<newtabref href="https://nitter.net/dergigi/status/1604601105086025728" title="spotted">}} in the wild, allowing users and readers to login to Wordpress from their Lightning wallet (or any app supporting LNURL-Auth).

### New LNBits Release

A new version of LNBits was {{<newtabref href="https://nitter.lacontrevoie.fr/callebtc/status/1604856859193921536" title="released">}} introducing (among other things) a new Admin UI and superuser role (to manage one's LNBits instance Core settings), a new {{<newtabref href="../latest-strikes-2/#cashu" title="Cashu">}} extension and a whole load of fixes and improvements!

### Mostro

Last week my eyes were also {{<newtabref href="https://nitter.lacontrevoie.fr/negrunch/status/1604841310682316800" title="caught">}} by {{<newtabref href="https://github.com/MostroP2P/mostro" title="Mostro">}} which tries to do to P2P Bitcoin trading on Lightning what {{<newtabref href="https://usenostr.org/" title="nostr">}} did to P2P communications[^1]. Much like in nostr where people running clients connect to relays, people wanting to trade with others will connect to some Mostro instance, possibly their own, through a client. The Mostro instance serves as an escrow during the trade, and Mostro instances will compete to gain users (and hence, fees) in a reputation-based market. Interesting!

## Closing Bit

Le Verbe est feu, creuset, et moule :\
Il façonne et cuit, fond et désassemble,\
Il étiole ou fragmente, sépare puis rassemble\
Ces briques orangées que l'on trempe à la houle.

---

Want to receive Latest Strikes straight to your inbox every week? Couldn't be easier: subscribe to {{<newtabref href="https://blog.lnmarkets.com" title="LN Markets Ghost blog">}} and you're all set (remember to confirm your subscription by clicking the link sent via email).

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins to *fanis @ lnmarkets.com*, by scanning or clicking the QR code.

Thank you!

{{<figure align=center src="../../images/lnm_lnurl.png" link="lightning:fanis@lnmarkets.com">}}

[^1]: And it actually uses nostr as a communication medium, so I believe the comparison isn't too far fetched.
