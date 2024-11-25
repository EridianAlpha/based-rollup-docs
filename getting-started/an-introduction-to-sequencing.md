# 🔢 An introduction to sequencing

An Ethereum validator secures Ethereum. It performs several duties but for Based Rollups only the `block proposal` duty will be discussed. Block proposals are random and rare, on average once every \~6 months but they provide the majority of the rewards a validator receives.

Even though based sequencing has only more recently been discussed in the context of L2s the Ethereum L1 has always been a sequencer.

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="482"><figcaption></figcaption></figure>

When a validator is selected to propose a block they have sole and complete control over the order of the transactions in the block they build. They can't insert any invalid transactions (tx) but can add any tx they like as long as it covers the base gas fee.

{% hint style="info" %}
This may change in future with features such as [FOCIL](https://eips.ethereum.org/EIPS/eip-7805) and [BRAID](https://www.coinlive.com/news/ethereum-s-road-to-anti-censorship-braid-and-focil-who-is-better) but as of writing, Ethereum validators are still absolute dictators during their block proposal.
{% endhint %}

When a validator only uses their local mempool to look for txs to include in their block it is called `vanilla block building`.

<div data-full-width="true"><figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure></div>

And that's it. An Ethereum validator can be a full participant of the network just by performing its required duties and proposing vanilla blocks. So why are over 85% of all Ethereum blocks built by just two block builders? MEV 🤖

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p><a href="https://etherscan.io/dashboards/block-producers">https://etherscan.io/dashboards/block-producers</a></p></figcaption></figure>

## MEV Boost

Maximal extractable value (MEV) is a [huge concept](https://docs.flashbots.net/new-to-mev) but from the perspective of an Ethereum validator, it's simple. Someone is willing to pay you to control the exact order of transactions within the blocks you propose.

<div data-full-width="true"><figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure></div>

Why does the specific ordering matter? Ethereum already has a way to get transactions included in a different order. The `priority fee` can be set higher so that validators have an incentive to include a particular tx first in a block. But there are cases where even greater control over the tx ordering can yield much higher rewards. This could be simple arbitrage between a centralized exchange and a DEX or a more malicious [sandwich attack](https://www.coingecko.com/learn/sandwich-attacks-prevention-crypto), but if there's money to be made (and there's [a lot of money](https://dune.com/defi_wonderland/mev-bots) to be made!) then someone will pay for it.

This is where [MEV Boost](https://docs.flashbots.net/flashbots-mev-boost/introduction) comes in. To allow any validator to participate in an auction for the tx order in the blocks they propose MEV Boost was created. All a validator has to do is run the MEV Boost software and tell it which relays it wants to use. From the perspective of a validator, this is a win-win. They can opt-in and opt-out at any time, it's free to use, and they get paid significantly more for each block proposal! There's even an option to set a `min-bid` parameter so that if you as a validator get a low offer for your proposal from the MEV Boost builders, you can fall back to building your own blocks locally.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

| MEV Boost - Pros                                                                                                                                   | MEV Boost - Cons                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| <ul><li>Free to use</li><li>Opt-in and opt-out at any time</li><li>Set <code>min-bid</code> value as a fallback for local block building</li></ul> | <ul><li>Centralizing effect on hyper-specialized block builders</li><li>Can decrease censorship resistance of Ethereum</li></ul> |

When a validator uses MEV Boost it must `blind sign` the block header without seeing what will eventually be included in the final block. This can be risky. If the block builder submits an invalid block or doesn't end up sending it at all then the validator would miss their proposal. Relays are used as the mediators for many block builders to check that blocks are valid and to give validators a trusted contant point to ask for the current highest bid for their proposal slot.

<div data-full-width="true"><figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure></div>

Notice that multiple block builders can talk to multiple relays and that a single MEV Boost client being run by a validator can select which relays it connects to. There is an auction for each block with block builders submitting their highest bid and the relays sharing those bids with the validtor. The bids increase throughout a 12-second slot, so there is an incentive for the validator to wait as late as possible before accepting a bid to maximize their profit. But if they wait too long, they might miss the slot completely!&#x20;

{% hint style="info" %}
These timing games are important to know about in the context of Based Rollups and preconfirmations as they add another level of economic incentive and penalty for missing a block proposal.
{% endhint %}

## Sequencing all the way down

Ethereum is a sequencer for its own transactions. A validator can choose to order the txs in their block proposals themselves or outsource it to specialized block builders through MEV Boost to significantly increase their rewards.

But what if you expand this sequencing concept further? What if instead of sequencing only the Ethereum L1 txs, Ethereum validators sequenced L2 txs as well. This is Based Sequencing and is the foundation of Based Rollups.

<div data-full-width="true"><figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure></div>

As an Ethereum validator, this means more revenue for you as those L2s will pay for you to sequence their txs. There's also a long list of other benefits (synchronous atomic composability, ..., etc.) that will be covered in detail in the following pages.
