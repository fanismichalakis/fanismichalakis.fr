---
title: "Back Down, You Oniony Psycho!"
date: 2022-07-06T20:58:51+02:00
draft: true
---

A discussion regarding Onion Messages and counter-measures to potential Denial of Service (Dos) attacks on the Lightning Network has recently resurfaced on the Lightning-dev mailing list, following the Oakland Dev Summit. Onion Messages are one of the key parts of Bolt 12, a specification for reusable payment codes for Lightning (unlike invoices, which expire and must be generated dynamically). I've tended to be a bit skeptic regarding Onion Messages, as I fear they might put too much of a burden on average Lightning Nodes and lead to Dos, so this discussion very much interested me, to the point that I decided to write the present article. In the following lines, I'll try to contextualize and summurarize the current discussions on the topic, and I will also reproduce the mails from the mailing list in an appendix at the end of the article, for those that might find it easier to read it here.

## Context

{{<newtabref href="https://bolt12.org/" title="BOLT12">}} is a lot of things, mostly aiming at solving 2 issues in today's Lightning user experience:
- Bolt 11's invoices (the one we're used to) are ephemeral, in that a given invoice can only be used once and have an expiration time, usually of one hour or even less,
- Bolt 11's invoices require some extraneous communication between the payer and the payee, because the payee must generate the invoice and send it to the payer. For example, in order to withdraw money from a {{<newtabref href="https://lnmarkets.com" title="Lightning-enabled financial service">}}, you must generate an invoice on your wallet and communicate said-invoice to the service. A better UX would be to be able to receive simply by scanning a QR code on the service's website, without having to manually generate and transfer an invoice (especially between devices).

Bolt 12 consists in reusable payment code. You can have a Bolt 12 QR code as a static image on your website or your Twitter banner, leave it there indefinitly and receive payments. Alternatively, as I mentionned above, service providers could leverage Bolt 12 codes to offer a simplified withdrawal experience to their users.

You may know that a meta-protocol built on top of the Lightning Network already enables such use cases: {{<newtabref href="https://coincharge.io/en/lnurl-for-lightning-wallets/" title="LNURL">}}. The big difference between the two is that LNURL relies on classic HTTP communication (and hence on servers), whereas with Bolt 12 everything would happen on the Lightning Network (no need for web servers, yaï!).
