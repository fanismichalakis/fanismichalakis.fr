---
title: "Using Bitcoin OP_RETURN for Command and Control"
date: 2021-12-11T18:47:17+01:00
tags: ["bitcoin"]
categories: ["logs"]
draft: false
---

Today's article is a fun one. The story it describes is not new, but it has resurfaced recently following a {{< newtabref href="https://blog.google/threat-analysis-group/disrupting-glupteba-operation/" title="blog post" >}} by Google's Threat Analysis Group (TAG). A story of how a group of criminals has used (and, to the extent to what we know, still uses) Bitcoin in a quite unexpected way: to send data to their malware.

## Its name was Glupteba

Quoting Google, Glupteba is "known to steal user credentials and cookies, mine cryptocurrencies on infected hosts, deploy and operate proxy components targeting Windows systems and IoT devices". The malware has spread globally via different means.

For its operation, the malware notably relies on a network of Command and Control (C2) servers that can be used to send commands and exfiltrate data. To put it in layman's terms, that's basically how the attackers are able to control their malware.

Glupteba therefore connects to a hard-coded list of servers (via HTTPS) to listen for new instructions. But it also has the ability to "evolve" and learn new C2 servers addresses in case the hard-coded ones stop responding. This is where Bitcoin comes into play.

## Bitcoin OP_RETURN

OP_RETURN is a Bitcoin opcode that can be used to store small chunks of arbitrary data in the Bitcoin ledger. When someone talks about using Bitcoin to anchor and timestamp data, they usually have OP_RETURN in mind.

When a Bitcoin transaction spends to a OP_RETURN output, it basically marks the output as unspendable while allowing to attach up to 80 bytes of hexadecimal data to this output. Therefore, OP_RETURN outputs usually have a value of zero bitcoins, and the transaction that creates them only pays for the fees.

It is one of the most ancient and used ways of storing data onto the Bitcoin blockchain, notably used by protocols such as Omni (on which tokens such as USDT can be created for example).

## Malware resilience through Bitcoin

Back to Glupteba. The code of the malware contains a set of Bitcoin addresses. If the hard-coded C2 servers stop responding, the program will fetch the latest OP_RETURN transaction from the addresses and decode it. It will then decrypt the data contained in the OP_RETURN, using one of the two hard-coded keys that can be found in the malware's source code. And guess what? This data is the address pointing to the new C2 server to listen to.

Because we know the Bitcoin addresses used to send data and the cryptographic keys used to decypher it[^1], we can put ourselves in the skin of the malware and find the latest C2 server address by ourselves!

For example, let's look at {{< newtabref href="https://mempool.space/address/1CUhaTe3AiP9Tdr4B6wedoe9vNsymLiD97" title="1CUhaTe3AiP9Tdr4B6wedoe9vNsymLiD97" >}} on a block exporer. The last transaction ({{< newtabref href="https://mempool.space/tx/5ebc64978d6b87334d766f17edcb8d35057253d4f29c804dd3dd01ea7d40a517" title="5ebc64978d6b87334d766f17edcb8d35057253d4f29c804dd3dd01ea7d40a517" >}}) with a OP_RETURN (`5f72c7e743ea20f1f15361cf9e5d23d192b589e42a25b4441f118dd2a1c0fad4d6b5dbd9831688e481`) is quite recent: only two days ago! We can copy paste the OP_RETURN data it in a little Python program, alongside with the deciphering key found in the malware's source code:

```python
from cryptography.hazmat.primitives.ciphers.aead import AESGCM

key = bytes.fromhex('1bd83f6ed9bb578502bfbb70dd150d286716e38f7eb293152a554460e9223536')
script = bytes.fromhex('5f72c7e743ea20f1f15361cf9e5d23d192b589e42a25b4441f118dd2a1c0fad4d6b5dbd9831688e481')

iv = script[0:12]
ciphertext = script[len(iv):]
aesgcm = AESGCM(key)
print(aesgcm.decrypt(iv, ciphertext, None))
```

**When running this program, we obtain the address of the latest C2 server** (mydomelem[dot]com, don't go there)!

I found this way of using the Bitcoin permissionless network quite smart. The malware relies on a set of Electrum servers and blockchain.info API to fetch the data related to the three Bitcoin addresses it monitors, which would be quite hard to censor. Attackers could take it even a step further and actually use OP_RETURN data to pass instructions to the malware, instead of pointing it to new C2 servers from which to get instructions. Of course, it wouldn't allow them to extract data, but 80 bytes is more than enough to send instructions. For malwares that do not require the extraction of data (such as purely destructive ransomwares for example), this would provide attackers with a great advantage in terms of resilience. I bet they already do.

[^1]: Thanks to this {{< newtabref href="https://news.sophos.com/wp-content/uploads/2020/06/glupteba_final-1.pdf" title="great research" >}} made by Sophos in 2020.