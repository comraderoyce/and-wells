+++
math = false 
meta = false
toc = false
author = "Royce"
title = "More Audits on the Blockchain"
date = "2021-11-06"
category = "blockchain"
description = "An updated review of financial auditing practices using distributed ledger technology"

+++

This is an update and reflection on my prediction that blockchain technology would allow more transparent and precise audits.

# 2018 Prediction

In 2018 I wrote [an essay](/writing/audits) about the possibilities of conducting audits and forensic accounting on the open ledger enabled by blockchain protocols. I argued that this would allow a more radical kind of transparency in organizations when compared to the current system of centralized trust that upholds accounting and corporate reporting today.

# 2021 Update

With the expansion of blockchain technology, especially the growth of decentralized finance, there are a lot more opportunities to see the inherent audit capabilities of distributed ledgers. We get to see it in action, live in production. With increased adoption over the past year, the potential for various kinds of on-chain financial analysis has become reality.

Since all activity is recorded on chain and publicly visible, reporting statements from on-chain activity can be verified by any third party. Reporting can be directly generated from the on-chain data, providing real-time financial reporting. Chain analysis and forensic accounting on the blockchain allow for rapid post-mortem analysis of theft and exploits.

## Market analysis

Chain analysis is a fast-growing segment of financial data analysis tools. These tools let users derive and act on signals from data contained pulled from the distributed ledger. As more markets run on blockchain technologies that allow for always-open trustless settlement layers, this tooling for analyzing holdings and transactions like Nansen will gain even more utility.

Already open tools like [Dune](https://dune.xyz/) (used in the Aave dashboard below) allow [SQL](/writing/sql-tableau) access to transaction-level chain data. They have also abstracted several other transaction categories like trades on distributed exchanges.

Order flow, volume, price, and other metrics can be computed and available on chain. Both real-time and historical data are easy to gather because the history of transactions is an immutable part of the underlying ledger. Large transactions, holdings, and market moves are available and [real-time notification](https://twitter.com/whale_alert) systems can be built on top.

More advanced paid tools like Parsec give huge flexibility over chain analysis workflows. Traditional finance data is notoriously opaque. Blockchain data is the opposite, and even free tools can provide enormous insight.  

{{< figure
  src="/parsec2021.png"
  type="full"
  caption="A Parsec Finance dashboard."
  alt="A Parsec Finance dashboard."
 >}}
{{< section "end" >}}

## Basic Financial Reporting

Some protocols have formalized this reporting using traditional finance metrics derived from on-chain data. 

For example, Yearn Finance [publishes](https://github.com/yearn/yearn-pm/tree/master/financials/reports) "quarterly reports" that include income statements and balance sheets. {{% marginnote %}}I wrote more about Yearn in my early 2021 [review](/writing/blockchains-2021) of blockchain projects to watch.{{% /marginnote %}}

Other examples are less formal but just as informative. 

Here's a reporting dashboard for the lending protocol Aave. It shows the reserve factor for their loan book. This is the treasury money that pays organizational expenses and would be used to cover bad debt.

{{< figure
  src="/duneaavetreasury.png"
  type="full"
  caption="A Dune Analytics dashboard for Aave's treasury."
  alt="A Dune Analytics dashboard for Aave's treasury."
 >}}
{{< section "end" >}}

Similar to a bank, a healthy capitalization ratio and loan book are necessary for a successful DeFi lending protocol. Yet blockchain transparency is such that you can see every loan that is on the books. 

Since data is publically available and on-chain, detailed financial information--once again with present and historical data readily available for review. More analytics tooling will make it further accessible. 


## Forensic Accounting

> “In a world of thieves, the only final sin is stupidity.”
>
> \- Hunter S. Thompson

A [2019 Accenture study](https://www.accenture.com/us-en/insights/financial-services/cost-cybercrime-study-financial-services) found that financial organizations pay almost $19 million annually as a result of hacks and data breaches. [A 2020 report by the FBI](https://www.fbi.gov/contact-us/field-offices/anchorage/news/press-releases/fbi-releases-2020-internet-crime-report) estimated some $4.1 billion was stolen from reported US households as a result of cybercrimes. In a 2003 survey of companies in 50 countries, PWC found 37 percent suffered from fraudulent acts, with an average company loss of more than $2 million. One of four frauds was committed by executives or managers. I don't expect that decentralized finance is any different. 

Yet a unique feature of blockchain is the ability to conduct forensic audits around hacks, exposing the mechanism and address of the attacker. The result is that exploits can be analyzed and the exact accounting of stolen funds reported. 

[Here](https://blog.alphafinance.io/alpha-homora-v2-post-mortem/) is an example of a hack post-mortem breaking down the various transactions leading to the exploit. Each action is recorded in the blockchain and can be analyzed after the fact. 

This kind of forensic accounting is even more useful when combined with methods to link individuals to their addresses.

For example, in the Poly Network hack over $600m in various cryptocurrencies was stolen. The money was [returned](https://www.theverge.com/2021/8/23/22638087/poly-network-600-million-stolen-crypto-hack-restored-defi) after a security firm's on-chain analysis and exchange know-your-customer records identified the attacker. 

A member of SushiSwap's development team managed to steal 865 ETH (~$3m at the time) with a supply-chain attack before getting doxed. The developer subsequently [returned the funds](https://cryptoslate.com/hacker-returns-865-eth-stolen-from-sushis-token-launch-platform-miso/).

Users of Open Sea's NFT marketplace found that the head of product was [wash trading](https://www.theverge.com/2021/9/15/22676075/opensea-insider-information-nft-trading-nate-chastain) based on insider information. Community members found trades front-running frontpage listings linked to his ENS name and other claimed assets including a CryptoPunk. He eventually left the company.

Ribbon Finance community members discovered that a VC firm had sybil farmed the $RBN airdrop with insider information. The community and other investors pressured the firm [to return](https://www.coindesk.com/tech/2021/10/08/airdrop-ethics-vc-firm-draws-ire-following-25m-ribbon-finance-exploit/) millions of dollars worth of $RBN.

Law enforcement is already regularly using chain analysis for [investigations](https://blog.chainalysis.com/reports/silk-road-doj-seizure-november-2020). 

Free and open-source tools for data analytics and auditing of on-chain data are readily available. More value accruing to the ecosystem will increase demand for these tools. On-chain data provides fraud protection, verifiable history of past action, and a wealth of other market data.

## An Exception

Tether is one counterexample to the transparency afforded by distributed ledgers. $USDT itself once on chain is clear and trackable but the issue is the underlying backing. Supposedly it is 1:1 USD, but skeptics abound. This returns us to a classic problem in speculative finance and banking. Tether's role in one of the largest shadow-banking operations of our time is better explained in a separate piece.

But in many ways, the Tether saga makes me further convinced in the importance of financial information living on-chain in a public ledger. Tether's audit for $60B of dollar reserves consists of signed statements from their accountant with top-level numbers from a single date.

There are some novel experiments with legal structures and DAO frameworks that look to solve the fiat bridge problem. Yet the current market leader is still Tether, which is the opposite of transparent. Maker DAO is already starting to incorporate real-world assets into their balance sheet, including a solar farm and euro bonds. Those debt positions will be actively represented on chain, but there will still need to be some accounting of this collateral that doesn't live on chain with an oracle or trusted third-party. This is a hard problem and will be an area of active development for a long while still as it is one main weakness of the system.

# Predictions

Looking back on my previous predictions, I think I did decently. The extended use cases of auditing with a blockchain are manifesting. 

In general, blockchains allow for more transparency and users are leveraging this transparency in unique ways. In some cases, audits and forensic analysis by user communities have put pressure on fraudsters or bad actors.

Further addressing the specifics of my earlier [predictions](/writing/audits/): 

> Software to analyze and report on transactions on a blockchain would give individuals the ability to audit the network, verifying that everyone plays by the rules.

Tools to audit transactions and other on-chain data are readily available. Many are open source and based on public ledger data allowing anyone to review transaction histories. For example, Etherscan links are common ways to produce evidence and link users between different wallets.

The analytics tooling around blockchains is still early, but already a large market. Financial analysis in the vein of Nansen or Messari uses on-chain data as the basis for reporting.

> We may find that our trust in some organizations is misplaced. It is possible, even likely, that many of these third parties are cheating the current system.

There has been clear exposure of insider trading and manipulation with evidence provided in the form of transaction receipts. 

The public ledger is forever and one slip in opsec either on-chain or when using on/off-ramps means that all past activity is now compromised. 

Many actors have not caught on to this fact, are sloppy, or do not think they had reason to conceal their activity. Connections between wallets can lead to ENS names that lead to public profiles. These connections are now common occurrence and will last as long as the blockchain. 

> Far superior products are coming to market that offer open and honest records of business. The utility of the distributed, record, available for anyone to audit and confirm is only in its beginning stages.

The utility of this is still playing out. Blockchains are still small technology, though growing fast. Further integration with real-world assets will make audits of the distributed ledger even more useful.

> Expect to see many more interesting use cases as the technology matures.

More assets are going to be securitized and their value representations tracked with blockchain distributed ledgers. See for example the work of [Toucan](https://docs.toucan.earth/protocol/), which is building out a bridge infrastructure to verify base carbon tons and securitize them on chain. 

The composable nature of smart contracts then lets an organization like [Klima DAO](https://klimadao.finance/) build an on-chain treasury of carbon credits. More assets like the base carbon ton will be securitized on chain to be accounted for transparently. The additional liquidity provided by the 24/7 global market living on the blockchain is a bonus.

## Further Predictions

Much of the important data can be computed or inferred from the chain state that contains the current and historical record of transactions. Price oracles can bring in trustless feeds of outside data for use on chain. However, more interesting is data moving natively on chain.

A good example is the ability to compute price data from Curve v2's internal oracle. With chain state and the open access to the Curve contracts, full pricing data for their exchange is transparently available. Curve may now be offering one of the tightest spreads between Euro and Dollar swaps. 

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Curve EUR/USD v2 pool has under $100k in liquidity, but a swap is already more than competitive with Wise <a href="https://t.co/79O6XLgxcX">pic.twitter.com/79O6XLgxcX</a></p>&mdash; royce (@thatRoyce) <a href="https://twitter.com/thatRoyce/status/1455638136483110918?ref_src=twsrc%5Etfw">November 2, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Ethereum's current design makes data storage and execution relatively expensive, but there are a large number of technical solutions in exploration phases. There is a lot of design space to play in. For example, zero-knowledge proofs and the rollup calculations they enable could provide reputation scores or sybil warnings based on all previous chain data.

I think these kinds of applications are a bit further off in the future. I think we continue to see chain analytics be a key theme ("just check the chain"). I expect that shady behavior continues to surface and a lot of it will come from the larger community instead of traditional law enforcement. Longer term, data availability and lower computation costs will enable forensic-accounting-as-a-service solutions based on chain state data. These can then be readily available as part of the composable layer of on-chain applications.

As more assets are securitized and added to the distributed ledger, transparent accounting will continue to be a theme and benefit from the network effects of additional capital and data. The pitfalls will be joining real-world assets with on-chain data. As we have seen with Tether, the liminal space between "real" assets and their on-chain representations is where the transparency of the ledger will break down. 

A higher percentage of on chain assets will mitigate this somewhat. Transactions on the network are open and transparent by default. Auditing transactions and compiling financial statements for addresses is a matter of the right tooling. Improved chain analysis tools can always be retroactively applied to the historical state of the ledger. So once an asset is on chain, it will be accounted for.