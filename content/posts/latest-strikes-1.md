---
title: "Latest Strikes - Sept 11th 2022"
date: 2022-09-11T21:32:00+02:00
block: "753681"
cover:
    image: "../images/a_space_pirate_surfing_on_an_antigravity_board_in_the_mi_fac42e40-c471-4be9-9c6c-1807ddb6aec3.png"
    alt: "A space pirate surfing on an antigravity board in the middle of a storm with lightning bolts"
    caption: "'A space pirate surfing on an antigravity board in the middle of a storm with lightning bolts.' Generated with Midjourney."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
paybuttonlink: "https://btcpay.fanismichalakis.fr/apps/2dTq39Qoj9oJrFdBTQNTXu2MjbMh/pos"
draft: false
---

Hello there, and welcome to this first edition of *Latest Strikes*, a brief weekly recap of what's new in the Lightning world. Buckle up!

## Wallets & Tools

### Alby

Alby announced their new release (v1.15.O). If you're interested in the details of the release, you can read their {{<newtabref href="https://nitter.net/getAlby/status/1568228464636956674" title="Twitter thread">}} or the {{<newtabref href="https://github.com/getAlby/lightning-browser-extension/releases/tag/v1.15.0" title="release notes">}}. In a few worlds: Alby now works in the Tor Browser, and will be even better than before at catching Lightning links such as LNURL or invoices. Notably, Alby will now capture links that were not present when the page was first loaded. A huge and appreciated improvement for dynamic websites (such as {{<newtabref href="https://lnmarkets.com" title="LN Markets">}}), which know work even better with Alby.

*Alby is a browser extension that allows you to interact with websites using your own Lightning node (or some custodial account). It supports a wide range of features from payment to authentication, and can detect Lightning links in a website metadata (like on this blog), or react to clicks on buttons and links. Learn more about Alby, and hopefully give a try, {{<newtabref href="https://getalby.com" title="here">}}.*

If you want to support the integration of Lightning and the web, you can donate to Alby using their <a href="lightning:hello@getalby.com" target="_blank">Lightning Address</a>.

### Mutiny

{{<newtabref href="https://mutinywallet.com" title="Mutiny">}} is a new, pricacy-focused Lightning wallet, built using the {{<newtabref href="https://github.com/L2-Technology/sensei" title="Sensei">}} architecure. It currently sacrifices features for privacy. For example, it is for now impossible to receive on Lightning to this wallet, because the privacy of the receiver is still limited in Lightning. This will change in the future thanks to things like route blinding, which Mutiny will use to enable receiving in the wallet.

Sending, on the other hand, already has pretty good privacy by default, thanks to {{<newtabref href="../onion-routing/" title="Onion Routing">}}. Yet, Mutiny takes it even a step further by spawning a new node every time a new channel is opened. The new channel is unannounced and funded with a whole UTXO coming from an external wallet: no change, no public identity on the network, etc. It's Lightning, but with stealth mode on.

If you're interested, please keep in mind the wallet is still in alpha (or even "barely in alpha").

## Papers

### Lightning Privacy

This week, a {{<newtabref href="https://arxiv.org/abs/2201.11860" title="paper">}} claiming that "with the growth of the [Lightning] network the overall anonimity decreases" managed to catch some understandable {{<newtabref href="https://nitter.net/LaurentMT/status/1566791574528442373" title="interest">}}. Turns out the paper made some incorrect assumptions regarding payment routing. One of the author's hypothesis was that source nodes always select the shortest path, which is incorrect on many levels:
- multipart payments (where one transaction follows multiple paths) is a thing since a lot of time,
- the path selection by the sender doesn't only consider fees or path length. Some randomness is also added specifically to break payment path predictability and prevent such anonimity issues.


## Ecosystem

### Let the Geyser Erupt!

Geyser just {{<newtabref href="https://nitter.net/geyserfund/status/1567537222005530625" title="announced">}} the first round of their grants! The platform allows creators, educators and projects to collect funds. It also leverages the interoperability enabled by the Lightning stack to funnel money from outside the platform. You can now donate to a campaing without even having an account on the platform where the campaing is running. Refreshing!

## An Old Thing I Only Discovered Now

I was still assuming zero amount invoices to be insecure because they could easily be exploited by the last hop in the route. Seems like I was wrong since more than a year!

{{< tweet user="FanisMichalakis" id="1568713558602518530" >}}

The idea of the attack was that, if the last hop guessed that it was a zero amount invoice (and hence, that the receiver had no real idea of the amount they was supposed to receive), they could simply forward as low an amount they wanted, get the preimage from the receiver and pocket the difference, unnoticed.

Since then, this issue has been {{<newtabref href="https://nitter.net/lucasdcf/status/1568738968862326784" title="fixed">}} in most Lightning implementations by making the presence of a `payment_secret` in the Onion Package mandatory[^1]. The original purpose of the `payment_secret` was to protect receiving nodes from probing: they would add the secret in the invoice, and the sender would then put it in the Onion, so that only the final node (the recipient) can see it. The recipient can then only accept HTLCs with the good `payment_secret`, and would therefore refuse any probing HTLC (which would by definition not have a good secret).

In the context of zero amount invoices, the `payment_secret` serves as a tamperproofing mechanism: to steal the funds as we described above, the last hop would have to forge a new HTLC which forwards, for example, only 1 sat to the final recipient. But the last hop would not be able to reproduce the `payment_secret` in their forgery, and hence would not be able to have the HTLC being accepted by the final recipient.

## Closing Bit

{{<blockquote>}}
De peur, d'ennui ou de déraison,\
N'embrasse pas cette nuit béante\
Redresse cette tête, jadis fière\
-- Aujourd'hui vacillante,\
Et porte-la au ciel comme une malédiction.
{{</blockquote>}}

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins in the jar. Thank you!

{{<paybutton text="🫙 TIPPING JAR 🧡" color="#D7816A">}}

[^1]: This is done by setting the feature bit 14 to true.