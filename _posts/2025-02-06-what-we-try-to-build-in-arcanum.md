---
layout: post
title:  "What we try to build in Arcanum"
date:   2025-02-06 00:00:00 +0500
---

This post will be covering what I am doing in Arcanum and what it's going to become. I will tell about it's tokenomics and the concept and will also describe how multipools of Arcanum works.

# The goal of Arcanum

Arcanum is a protocol that implements a game changing logic of asset management.

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>Lol, I can just go and buy any token I want and put them into my wallet, what's the point?</p>
</div>

Buying and holding a specific set of assets is only a single and pretty primitive form of managing your crypto portfolio. I want to give two scenarios that I think are enough to show the usecase.

**Scenario 1**

You are a normal chill guy that wants to build a portfolio in crypto but don't care that much even about specific assets. You are very low FOMO on a specific things, want to just pick up risk-profit ratio or a strategy and make it work.

In traditional finances you will most likely buy things like S&P500 or some other ETFs that will make you diversified enough and not worrying about this thing being maintained and up-to-date with promising assets.

**Scenario 2**

You want to invest, but you don't really like to operate with the idea that you buy assets for a specific value. Instead you want to hold a specific share of asset and want to control it's amount in your portfolio as accurate as possible.

Let's say you want to hold 90% of BTC and rest in Ethereum. You don't actually want to take more risk then holding 10% of ethereum in your wallet. In case Ethereum grows, rule remains, you want to sell Ethereum and buy extra BTC.

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>I think I can just use my wallet to trade this way right now, right?</p>
</div>

Yes, it's possible to do this, however both these strategies require you to keep a very active portfolio management. That is something that require you to constantly sit in front of your monitor and trade things, meanwhile these strategies are described for people who definately don't want to spend time on active trading.

This is something that some crypto protocols are trying to solve right now. However, if you do market research they suck in lots of ways.

# Why asset managers are not that good right now?

**Number of assets**

Most of currently existing asset managers work with a limited number of assets that is capped by around 25 assets per portfolio. This makes it very hard to create big indexes (we don't count any Coinbase 50 or other freaks as this is a completely centralized thing that also don't bring any value in addition to being index).

**Decentralization and permissionless**

On-chain solutions are usually very bad when it comes for them to be decentralized. Most of them force you to trust to a specific broker that implement some strategy for you and keep in mind all the numbers. Moreover mostly there are no opportunities to CHEAPLY do your ownd portfolio with current solutions.

**Asset management cost is hight**

Managing these portfolios requires big fees to be payed, involve other parties and are done in a way that capital doesn't bring enough value to the chain ecosystem.

**Asset management can only deal with big assets**

If you wan't to include a token that has only couple of pools only on the blockchain you operate on, you probably won't be able to do this. Bitcoin and Ethereum are okay, but usually you also want to get something small and perspective.

**Depostiting and withdrawals takes a lot of time**

Portfolios are usually designed in a way that they have epochs and they force you to wait some time with a withdrawal order placed to actually get the money back or in.

**You can't make profit**

Most of solutions don't provide any opportunities for you to benefit in terms of creating strategy or locking-in. Moreover there is no any additional monetization like farming or any utilities for these portfolios.

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>Okay, current portfolio managers sucks, why Arcanum is different then?</p>
</div>

# Arcanum's concept

Arcanum consist of couple of contracts, so called Multipools. Every this contract is an Independent portfolio managed by someone.

Multipools split asset management into several roles. 
There are:

**Strategy creators** - Guys who just propose the idea and specify assets to have within their shares (e.g I want to have a portfolio with hot defi stuff where token A will be 10% token B 40% and so on).

**Stratey executors** - These guys can use underlying multipool's liquidity for their own needs meanwhile also taking and putting in assets according to oracle prices and making them follow specified shares.

**Liqidity providers** - People who want to deposit into a specific strategy, they only need to supply one any asset from portfolio to mint shares. This makes it easy and quick to mint and burn.

Portfolios themselves are also ERC20 tokens, which means that they can be composable with other existing DeFi protocols.

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>I got something but it seems to be complicated</p>
</div>

Let's dive in a little more into every aspect, definig nuances of how these roles are acting.

# Creating multipool with a strategy

Multipool is extremely cheap and has alsmost no overhead due to very small gas cost for all operations. This means that issuing new portfolio is very cheap for anyone.

User needs to specify fee parameters (will be discussed later in a separate section), they are: management fee, some description on what this is and other meta information and assets with shares he wants to have inside.

Afterwards portfolio can be created within one transaction and some initial liquidity. The assets that can be chosen should only match two requirements:

* Be ERC20 compatible
* Have any price origin on-chain (uniswap v3 pool works)

By matching these two things you can easily opeate with a very small assets that are known only in your ecosystem. There is also no limit on the number of assets in the portfolio as more assets don't create additional overhead.

Basically, you can make money by receiving management fee, if your strategy is admired by cyrpto community.

# How strategy is executed

Important part is how this all system is actually managed. 

Anyone can use any multipool contract to execute swapping one underlying token for another. The swap is done within oracle price so it will be fair as your oracle price source and will make portfolio follow strategy.

Asset swap is an intent that works a little similar to 1inch fusion mode where anyone can come and execute your intent getting arbitrage benefits.

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>Swapping assets can change portfolio shares but why will they change to some specific ones?</p>
</div>

This is reached by adding fees and a special mechanic called cashbacks.

* *We use deviation do describe difference between current asset share and one specified by the strategy.*
* *There is base fee charged for every operation*. [mint/burn/swap]
* *If asset's deviation after your order decreases or remains, you are not charged with anything else.* 
[There is 5% of bitcoin missing and you minted share by putting 1% of BTC in]
* *Every time deviation grows, you pay extra fee for this.*
[If you have bitcoin deviation increased to 6% after being 5%, you pay extra fee]
* *Part of this deviation is collected to cashbacks of this asset.*
[Let's say 50% of fee is put there]
* *If someone decrease the deviation he receive cashback to him.*
[If deviation was 6% and I turned it into 3%, I reduced it by hald and will receive half of all collected cashback]

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>Is it enough incentives to manage shares of assets?</p>
</div>

Yes, as soon as anyone uses portfolio for it's own needs of issues/burns new portfolio shares, they are ready to pay extra for deviation, this immidiately creates and incentive for swapping back as it allows you to collect part of this fees to your pocket. That's just a more easy but less obvious way to pay for management.

# Putting and taking out liqidity

Not everyone needs to create their own portfolios. There are also a lot of people who would mostly want to join existing strategies that they like. This actually helps a lot:

* No need worry about discovering new assets in crypto to have the strategy being tuned with all the innovations.
* You can do copy trading of other person.
* It's anyway cheeper then mirroring the same actions as it's more cheap to manage in terms of blockchain transaction costs.

While putting assets you also only need to get any token that portfolio contains. This can be easily done by swapping this token for any other in same transaction to create a better mint-from-anything UX.

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>Yea, now it's clear enough, but you also mentioned tokenomics of Arcanum</p>
</div>

Arcaum contains a giant problem that is also it's giant strenght. It's the **share price**. Share price needs to be supplied within any transaction due to multipool's mathematics. This requires to have some oracles for it.

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>Why is it even a problem?</p>
</div>

Oracles for a permissionless tokens are not something provided by any off-chain oracle companies, moreover they usually can't work with something that complicated. Arcanum reqires you to sum up all asset's quantities multiplied by prices in order to retreive portfolio's share price. 

This made us to create our own oracle network specifically for Arcanum. 

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>So you need to constantly supply prices on-chain, Arcanum's infrastructure cost should be big then.</p>
</div>

Arcanum supply all the prices extremely efficiently due to several reasons:

1. **Oracles are optimistic and PoS based.**
This makes Arcanum oracles to provide some data optimistically (making price verification very cheap) and vulnerable to get slashed if they submit malicious price.
2. **Signed price is only supplied by trader when multipool is called.**
This makes Arcanum's strategy executors work closely with oracles.

And that's where things become our strenght:

* Arcanum has a $AREV (Arcanum revenue) token that serve for govenrance and PoS needs. It's fully collateralised by ecosystem's gas token and also encapsulates the potential of all future protocol's profit.
* Proof-of-stake mechanism allow to mint new $AREV token for oracle. The new portion is minted to the oracle who submitted it's price withinn a trade. Part of collected fees are used to collateralize newly minted $AREV.
* As an oracle you want to buy more token so buy want your price to be used in the code that generates more protocol revenue.
* That's why oracles are incentivised a lot to become strategy executers to arbitrage multipools and help people to mint shares more efficiently.

We turn oracles into a network of parties that are economically interested in making all system work. They exactly are incentiviesd for actions that make protocol useful and receive a fair reward according to their actions.

<div class="quote-wrap">
    <img src="/assets/img/thinking_kiddy.jpg" width="50" />
    <p>Okay, seems all clear, where can I learn more or participate?</p>
</div>

Main links related to Arcanum are:

[Github](https://github.com/arcanum-protocol)
[X account](https://x.com/0xArcanum)

In conclusion, Arcanum actually solves all the problems from the start of the post and a lot more. 

It gives tremendous flexibility and opportunities. For example you can also create a **yield managing** or **AI traded** portfolios using Arcanum and the same concept.

Let's make it work all togeather, there are not a lot of new decent crypto things going now.
Bye
