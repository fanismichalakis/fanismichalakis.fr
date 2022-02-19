---
title: "NFC > NFT"
date: 2021-12-13T21:21:33+01:00
tags: ["bitcoin"]
categories: ["logs"]
draft: false
---

NFC seems to be all over Bitcoin Twitter recently, between Square/Spiral {{< newtabref href="https://squareselfcustody.substack.com/p/building-self-custody-hardware" title="annoucement" >}} of a NFC enabled hardware wallet, Coinkite teasing their {{< newtabref href="https://twitter.com/SATSCARD" title="Satscard" >}} and Coin Corner messing around with hilarious NFC Lightning payment {{< newtabref href="https://twitter.com/CoinCornerMolly/status/1469321657311543298" title="demos" >}}.

## What the hell is NFC?

NFC stants for Near Field Communication. It leverages one of the most elegant physical phenomenon Mother Nature gave us[^1] to enable communication between two devices that are very close to each other. A varying current in one circuit creates a magnetic field which in turn induces a current in the other circuit. This is used for example in induction cooking, where a magnetic field generates a current in the pan, resulting in the creation of heat via Joule effect. Or for wireless charging. Or to transfer information: by controlling the current in the emetting device, you are able to control the resulting magnetic field and therefore the current it induces in the receiving device. This way, you can wirelessly transfer information in the form of an electrical signal. That's NFC.

## Cool?

NFC is nice. It's quite convenient for paying, and we're quite used to it with our credit cards, debit cards[^2] and chip cards of all sorts. Additionnaly, it provides intersting features when dealing with Bitcoin.

Because the magnetic field is constrained very close to the emitting device, the two devices must almost touch for NFC to work. It is in stark contrast with WiFi or Bluetooth, which have a far wider rande and can therefore be remotely sniffed. With NFC, anyone willing to intercept the signal would have to be very, very close to you. Don't miss!

Another interesting aspect is that NFC doesn't require both devices to be powered. The current induced by the magnetic field in the receiving device can be enough to power the chip and make the data transfer happen. That's how NFC enabled cards work for example. This way, we could have hardware wallets that do not need a battery or to be plugged-in to work. I find it pretty neat, and it's no surprise Spiral and Coinkite are building on NFC[^3].

## What about NFTs?

Just listen to Keanu, friend.

{{< youtube Ywixfd63_Uk >}}


[^1]: Obviously, electromagnetic induction.

[^2]: You should use cash.

[^3]: I must also mention my friends at Satochip, who released an intringuing visual of a "{{< newtabref href="https://twitter.com/Satodime_io/status/1470398996787216389?s=20" title="Satodime" >}}". Given the name and the nice "SEAL - LOAD - VERIFY" mention on the card, I think I can already announce it will be some kind of NFC-enabled opendime-like, which we can also suspect Satscard will be.