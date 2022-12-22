# 🤔 Problem Overview

A common approach to determine a possible space object collision from a screened conjunction event is to determine the Probability of Collision (Pc) based on Conjunction Data Messages (CDM) [^1]. 

There are two approaches to calculating the Pc: 
1. The "two-dimensional" Pc calculation approach.
2. The "three-dimensional" calculation approach

The issue with both approaches arises when the primary and secondary object covariances for some orbit regimes contain significant correlated error, introducing inaccuracy in the calculated Pc [^2]. This problem of inaccuracy in the calculated Pc is commonly referred to as _**dilution**_ (or) _**probability dilution**_. This problem of dilution is rooted inaccuracies in spacecraft state estimation. Uncertainties in state estimation bleeds (autocorrelation errors) into risk calculation probabilities creating dilution.

The work around for such correlated errors is establishing a Pc threshold by the owner/operator (O/O) to mitigate a conjunction. This is a function of,

1. the risk tolerance of the O/O and,
2. the volume of conjunctions that the O/O is able to mitigate at a certain time period (or) time to closest approach (TCA).

These threshold values tend to be $10^{-4}$ per conjunction event. This means a remediation/avoidance actions are established when the likelihood of a collision is greater than 1 in 10,000. More conservative O/O's opt for $10^{-5}$ or 1 in 100,000 [^2].

> A Conjunction Event in the case of spacecraft collision is a future event (at least a week in advance) where the likelihood of one or more (secondary(s)) space objects come within proximity of a protected (primary) space craft/asset [^2].

At the European Space Agency's (ESA) Space Debris Office (SDO) for example, a _**time series**_ of CDMs covering one week is released _**for each unique close approach**_, with about 3 CDMs becoming available per day. For a given close approach the last obtained CDM, including the computed risk, _can be assumed_ to be the _**best knowledge**_ they have about the potential collision and the state of the two objects in question. For this reason, ESA missions, especially in LEO use thresholds ranging between $10^{-5}$ and $10^{-4}$ [^3]. 

A new approach is proposed where space debris scientists' communicate their calculated Pc models' veracity. Scientists compete in a competition by staking a crypto-token, Watchtower (WTR), on their Pc predictions. The auction mechanism for resolving these stakes will reward predictions of Pc agreed upon. Via Dora, scientists can now be able to express confidence in their models' live performance. This skin-in-the-game expressions of confidence aid in evoking a more robust calculated Pc for a screened conjunction event thereby making dilution effects economically irrational [^4].

## The Core Issue Being Addressed

The core problem that results in dilution (and spacecraft state estimation) is our flawed models of actual astrodynamics and our flawed models of actual sensor observations and methods of statistical inference to solve them [^5]. This creates a data quality problem. This data quality problem we argue _**is not just**_ _a scientific and statistical one but also a social one too_ created by norms such as intellectual property and national security [^6] that prevents actors in the ecosystem to share & come to consensus on the data to maintain a high quality data set [^7]. A similar problem when tackling the climate crisis. Watchtower is a _computational social system_ designed to accommodate for the current norms while working towards solving the true problem of space debris and the crowding of orbits.

</br>


[^1]: (2013). Conjunction Data Message. Recommendation for Space Data Systems Standards CCSDS 508.0B-1 Blue Book. The Consultative Committee for Space Data Systems.

[^2]: (2020). NASA Spacecraft Conjunction Assessment and Collision Avoidance Best Practices Handbook. National Aeronautics and Space Administration

[^3]: Uriot, T., Izzo, D., Simões, L.F. et al. Spacecraft collision avoidance challenge: Design and results of a machine learning competition. Astrodyn 6, 121–140 (2022). https://doi.org/10.1007/s42064-021-0101-5 

[^4]: Tsetsos, K., Moran, R., Moreland, J., Chater, N., Usher, M., & Summerfield, C. (2016). Economic irrationality is optimal during noisy decision making. In Proc. Natl. Acad. Sci. USA, 113(11), 3102–3107. https://doi.org/10.1073/pnas.1519157113

[^5]: Jah, M. (2019). [The world's first crowdsourced space traffic monitoring system | Moriba Jah](https://www.youtube.com/watch?v=Ta8KBJ4BTNg) 

[^6]: Watchtower | [History](https://metasolis.gitbook.io/watchtower/introduction/history)

[^7]: Ballandies, M. (2022). [From computational social science and complexity science to Cryptoeconomics](https://www.youtube.com/watch?v=IrPv5bwUDEM). Token Engineering Labs