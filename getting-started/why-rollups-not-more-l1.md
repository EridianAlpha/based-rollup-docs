---
hidden: true
---

# 🤔 Why rollups not MORE L1?

Ethereum L1 is slow. Why is it slow? To allow for true decentralization the hardware, bandwidth and technical requirements must remain low 🗺️&#x20;

It's not a secret that faster block times would greatly improve the user experience on Ethereum which is why the "Rollup Centric Roadmap" has been actively developed since XX.

## Ethereum L2s - More clicks, faster ticks ✅

Rollups Can have much shorter block times as they manage their own state and only snapshots of that state are stored on Ethereum using `blobs`. <mark style="color:yellow;">TODO: Rephrase to better explain what blobs are</mark>

If at time t=0 a user starts with 1 ETH in their wallet on an L2:

* t=2s the user buys an NFT on the L2
* t=4s the NFT is used in a game and the player wins 0.1 ETH
* t=6s the user sells the NFT for a profit of 0.2 ETH
* t=8s the user takes a break, it's been a busy 8 seconds!
* t=10s the user trades their ETH profits for USDC

At t=12s the L1 proposes the next block and the L2 bids to include the changes made by the user during the previous 12 seconds. This was a great experience for the user, every interaction they had with the L2 felt almost instantaneous and they were never even aware of the slower L1 block times.

<div data-full-width="true"><figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure></div>



It's the interface bettween this seperate states that are the difference between an Ethereum L2, a side chain and an alternative L1.

{% hint style="info" %}
<mark style="color:yellow;">TODO: Side chains brief explanation</mark>
{% endhint %}

Parallel innovation in the infinite garden.



