+++
math = false 
meta = false
toc = false
author = "Royce"
title = "A War for the Gauges"
date = "2022-01-02"
category = "blockchain"
description = "How the Curve wars is spreading to other gauge protocols"
collections = ["blockchain"]

+++

This is a short history of the Curve Wars and a review of how gaugue tokenomics has evolved. 

<!--more-->

# The old blue king

First, some ancient crypto history. A long time ago in 2020, Curve launched. . Originally focused on swaps between similar assets, Curve has a lot of big-brained math that makes their stablecoin pools the best for large swaps between like assets (i.e. USDC to USDT or wBTC to renBTC).

They launched with a unique tokenomics model that allowed users to lock CRV tokens for up to 4 years. The resulting voting escrow Curve (veCRV) is non-transferable but gives a host of benefits. Holders get governance rights and a portion of the platform admin fees. However, most coveted has been the ability to use veCRV to “boost” liquidity pools. LPs on Curve get a large percent of CRV inflation in the form of liquidity mining rewards. But by “boosting” a specific pool gauge, an LP can increase their percent of CRV emissions, effectively raising their pool's APR and making it more attractive to LPs.

The yield aggregator Yearn used this to great effect to increase their vault APY. By acquiring and locking CRV, Yearn was able to boost the underlying LP positions that generated yield for their vaults. They went as far as to use a good portion of protocol revenue to buy and lock more CRV. The magnum opus of Yearn’s Curve strategy would be the Backscratcher vault, which accepted Curve deposits, permanently locked it as veCRV, and compounded all admin rewards as more locked CRV. Curve was one of the largest decentralized exchanges and Curve emissions a valuable additional source of yield. It seemed like Yearn would be the largest of whales in the Curve pool, directing these emissions at will.

# The start of the Curve Wars

The Curve Wars kicked off in earnest in May ‘21 with the launch of Convex finance and the fight to control the veCRV gauges. Remember, before Convex’s launch, Yearn was the largest influencer of Curve gauge weights through a combination of their vaults and the new Curve focused backscratcher strategy. Convex came with a new protocol looking to take over the Curve gauges.

The premise was simple: part one was to have users permanently deposit CRV with Convex in exchange for cvxCRV tokens. Convex takes this CRV and locks it forever as veCRV, to be used to boost gauges of their choosing. Part two was to accept deposits of Curve LP tokens and use the new boost powers to increase the APR on these positions.

LPs that staked with Convex got the benefits of increased APY for their Curve positions without having to buy and lock CRV themselves. The CRV liquidity rewards received are deposited back in Convex and distributed to LPs as cvxCRV. This means Convex constantly gets more veCRV and the associated gauge control.

Users that wanted exposure to veCRV and the admin fee revenue could buy and stake cvxCRV. But unlike veCRV, the cvxCRV is transferable has an established market allowing users to easily exit the position. This means cvxCRV functions as a liquid version of locked veCRV.

{{< figure
  src="/veCrvShare.png"
  caption="Convex has become the dominant holder of veCRV"
  alt="Convex has become the dominant holder of veCRV"
 >}}
{{< section "end" >}}

Convex had recreated the Yearn backscratcher flywheel and made it even more powerful. In less than a month, Convex became the dominant holder of veCRV. It has only increased its share since and holds almost 50% of all veCRV. Shortly after, Convex created their own locking scheme that allowed locked CVX to direct the gauge weight votes.

Funding liquidity mining incentives with token emissions has been an expensive project for many projects. What folks started to realize in the second half of the year is that instead of funding farming incentives with token inflation, it would often be cheaper to increase pool APYs by directing Curve gauges to vote CRV emissions to the right pools. Andre Cronje deployed a bribe mechanism that let projects put up tokens to “buy” votes in the gauge.
This was more or less the state of the Curve Wars going into the fourth quarter of 2021, setting the stage for an even larger fight.

# The conflict shifts from Curve to Convex

The combination of Convex’s control of veCRV and the mechanism for locking and voting with CVX has meant that each dollar of locked CVX controls multiple dollars of veCRV.Whales like Tetranode and projects like Abracadabra realized that the most cost-efficient way to control CRV APRs on pools was actually to buy CVX, lock it, and vote the pools of choice. At times this has led to 5 times the votes per dollar.

The same bribe system that worked for Curve votes was expanded to CVX voting with the creation of Votium. The result was that locked CVX holders benefited from a ridiculous number of revenue streams. Beyond the original promise of APR in CRV from LP incentives, 3CRV from admin fees, CVX platform fees, and CVX inflation, there were now additional bribes coming from all sides.

CVX price has mooned as the market tries to price the actual power levels of how much revenue a single CVX can generate.

# The fight for the gauges

The Curve wars and Convex’s adaptation of the vote-locking system proved out the superiority of Curve’s early tokenomics decisions. Gauges and requiring locked vote-escrowed tokens for protocol fees or perks has become the gold-standard tokenomics model. 

Adopted by the likes of K3pr and Frax, and shortly even Yearn, it is a proven model that prevents some of the mercenary liquidity of other inflation schemes.

Convex is getting in on the game early and is in the process of releasing a cvxFXS, replicating their vote-locking model for the Frax gauges. This means that soon, CVX will control large parts of both Curve and Frax emissions, increasing the revenue per share even further.

New players like Redacted Cartel have entered the scene with the express mandate to acquire more and more of these revenue-generating assets. By using the OHM seignorage model, the Redacted treasury has quickly grown its stash of Curve and CVX.

As more projects move to the gauge model, similar fights will break out. The Curve Wars is becoming a larger conflict for the gauges.

_Not financial advice. I own CVX, cvxCRV and CRV._ 