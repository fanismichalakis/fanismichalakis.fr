---
title: "Latest Strikes 2 - Sept 18th 2022"
date: 2022-09-18T14:00:00+02:00
block: "754655"
cover:
    image: "../images/realistic_ivory_tower_whit_thunderstorm_92999d8a-fe06-4bd3-9fe2-a669c174bb45.png"
    alt: "Realistic ivory tower with thunderstom"
    caption: "'Realistic ivory tower whit (*sic*) thunderstom' Generated with Midjourney."
    relative: "false"
tags: ["bitcoin", "lightning"]
categories: ["strikes"]
paybuttonlink: "https://btcpay.fanismichalakis.fr/apps/2dTq39Qoj9oJrFdBTQNTXu2MjbMh/pos"
draft: false
---

Howdy! Welcome to this second edition of Lightning Strikes, your weekly recap of new shiny things in the world of Lightning. LFG!

## Ecosystem

### LN Markets Release

{{<newtabref href="https://lnmarkets.com" title="LN Markets">}} published a new {{<newtabref href="https://nitter.net/LNMarkets/status/1569343500923052032" title="release">}}, which includes the lifting of trading limits from 2 million sats to 10 million (eg 0.1 BTC), Lightning Node Connect support (where you can interact with your LND node directly from the browser), new multilanguage support (starting with Spanish and French), as well as free internal transfers between LN Markets users and the (here comes the controversy) adoption of the {{<newtabref href="https://satsymbol.com/" title="Sat Symbol">}} (aka kebab-symbol).

The company also {{<newtabref href="https://nitter.net/LNMarkets/status/1570795363493347328" title="tweeted">}} an update of their Lightning node's routing metrics. They reached a new monthly ATH in terms of routed volume this September with 58 BTC forwarded, and the month isn't even over! On aggregate, their Lightning node routed 600 BTC since its creation.

*LN Markets is a Lightning native, KYC-free trading platform for Bitcoin derivatives (futures and options). It leverages the Lightning Network instant settlement and low fees to enable users to enter and exit positions directly from their own non-custodial wallets. The funds are on the platform only while a trade is open.*

Disclaimer: I'm a developer at LN Markets, so by definition their releases always catch my eye.

### Value4Value in Wordpress
{{<newtabref href="https://nitter.net/Bumi" title="Michael 'Bumi' Bumann">}} from {{<newtabref href="https://getalby.com" title="Alby">}} published a short {{<newtabref href="https://www.youtube.com/watch?v=2vJyTLrhR9g" title="YouTube video">}} demonstrating how easy it is to accept Lightning donations on a WordPress website, thanks to the plugin developed by Alby.

Install the plugin, set it up (can be as easy as pasting a Lightning Address), and you're good to go! You can now add Lightning donation buttons in all your posts, just like you'd do with any other WordPress component. Once again, the Alby team rocks! 🤘

## Wallets & Tools

### Cashu
{{<newtabref href="https://nitter.net/callebtc" title="Calle">}} (the genius behind {{<newtabref href="https://nitter.net/LightningTipB0t" title="LightningTipBot">}}) released {{<newtabref href="https://nitter.net/callebtc/status/1569986110272540674" title="Cashu">}}, a Chaumian Ecash wallet and mint with Lighnting support.

Chaumian Ecash comes from the prehistory of Bitcoin, but can still play a role in a world where Bitcoin *is*. The idea is quite simple: users can create tokens and ask for a signature from the central server, which blindly sign them. The server doesn't know exactly what the token it just signed was, but it can check that some condition (such as a deposit for some amount) have been fulfilled before signing it.

Users can then send signed tokens to each other. Upon receiving tokens from someone else, a user must ask the server to burn them and sign new tokens for the same amount. This is how double-spend is prevented.

In Cashu, users can deposit funds in the mint with Lightning, simply by paying an invoice. Once the invoice is paid, the server will sign the tokens.

Alternatively, users can withdraw to Lightning simply by sending an invoice to the server, which will burn the corresponding tokens and send the sats on Lightning.

Calle just released a {{<newtabref href="https://nitter.net/callebtc/status/1571026663147966467" title="demo">}} showing Lightning fast deposit and withdrawal to and from a mint, as well as sending tokens between users.

Before you go nuts on Cashu, please remember that the software was just released and is still pretty experimental. So don't send to much money (which should more generally apply to any custodial setup anyway)!

### Lightning Support in Mercury

Speaking of Lightning integration in server-based constructs on top of Bitcoin, {{<newtabref href="https://nitter.net/mercury_wallet/status/1570818987008884736" title="something">}} is brewing in Mercury Wallet!

{{< tweet user="mercury_wallet" id="1570818987008884736" >}}

## Specs & Implems

### Remote Signing in LND

Remote Signing is the idea of separating a Lightning node in two entities (preferrably running on distinct hadware): one that only has public key material and is in charge of almost everyting (P2P, invoicing, etc.) ; and a second one (the signer) that stores private keys and only does one thing: signing transactions.

The signer can be running on a very tightly secured network that only allows for one connection: the signing requests from the main node. This enhances the security of a Lightning node, allows for cool features such as *kill switches*, and more!

A {{<newtabref href="https://github.com/GaloyMoney/charts/pull/1581" title="pull request">}} was published by {{<newtabref href="https://nitter.net/openoms" title="openoms">}} this week, which implements Remote Signing in Galoy's version of LND.

### Blinded Routes in Eclair

Blinded Routes allow a receiver to conceal its identity on the network from the sender. The idea is that instead of the sender computing the whole route, the receiver will compute part of the route (eg a path going from some node J to them), and ask the sender to compute the route between them and J). This can be visualized in the following {{<newtabref href="https://nitter.net/evankaloudis/status/1569688244287340545" title="representation">}} by {{<newtabref href="https://nitter.net/evankaloudis" title="Evan Kaloudis">}} and {{<newtabref href="https://nitter.net/futurepaul" title="@futurepaul">}}

{{< tweet user="evankaloudis" id="1569688244287340545" >}}

The second part of the route (the one computed by the receiver) is hidden in the invoice, encrypted so that the sender can't read it, as well as any intermediary node until J, which then read it and proceeds to forwarding the payment along the route selected by the receiver.

This is a great improvement for the privacy on Lightning, and will soon make its way into {{<newtabref href="https://nitter.net/evankaloudis/status/1569352483587121152" title="Eclair">}} (as well as all the Lightning implems, in {{<newtabref href="https://www.youtube.com/watch?v=wrkxkBSvOUg&t=79s" title="due course">}}).

👉 The pull requests: {{<newtabref href="https://github.com/ACINQ/eclair/pull/2401" title="pull request">}} and {{<newtabref href="https://github.com/ACINQ/eclair/pull/2416" title="pull request">}}.

## Papers & Reports

### The Lightning Report #1
{{<newtabref href="https://ln.capital" title="LN.capital">}} released the {{<newtabref href="https://nitter.net/LN_Capital/status/1570728144293998598" title="first edition">}} of their Lightning Report. This issue focuses on routing nodes (which they define as nodes having more than 1 BTC in aggregate capacity and more than 10 channels).

The report is concise enough that I recommend its lecture to everyone, but here are a few highlights:
- in terms of capacity, routing nodes represent 87% of the network. Of this 87%, almost one half corresponds to "big nodes" (routing nodes with more than 40 BTC aggregate capacity),
- in terms of number of nodes, the routing nodes only represent around 5% of the nerwork,
- in the last two weeks, the absolute number of nodes has stayed approximately the same, while the number of routing nodes increased by around 2%.

This 3 observations draw the picture of a Lightning network where the liquidity is concentrated in *a few* nodes (around 930 nodes) ; and this concentration seems to be slowly increasing (at least it has been in the last 2 weeks).

*LN.capital is the company building {{<newtabref href="https://github.com/lncapital/torq" title="Torq">}}, a free and open source software helping routing nodes manage their capital efficiently on the Lightning Network.*

## Closing Bit

{{<blockquote>}}
Ta parole surgit -\
Comme un coup de fusain sur une page blanche\
Marque fugace, murmurée, répétée, oubliée aussi\
Un jour peut-être un sculpteur s'en saisira\
Et la gravera dans le marbre.
{{</blockquote>}}

---

If you enjoyed this recap, you can show your appreciation by throwing a few coins in one of the jars. The BTC Pay jar opens in a new tab, while the LN Address jar is a one-click button (with Alby) to send sats to *fanis @ lnmarkets.com*.

Thank you!

<div style="display: inline-grid;grid-template-columns: 50% 50%;align-items: center;width: 100%">
    <div>
        {{<paybutton text=" 🎩 BTC Pay 🏦" color="#51b13e">}}
    </div>
    <div>
        {{<paybutton text="✉️ LN Address 🐝" color="#f5ac11" link="lightning:fanis@lnmarkets.com">}}
    </div>
</div>
