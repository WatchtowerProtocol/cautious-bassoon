# 🕵️ System Specification

In this section the system specification is detailed for the system. This includes mathematical definitions, relations and specifications pertaining to the digital twin.

## Symbolic Representation

All definitions of the symbolic representation definitions have been described in the Engineering [Requirements](5_Requirements.md) Section. All upper case letters represent variables from the perspective of the system (Auction Tournament) while lower case letters represent variables from the perspective of the bidding agent (Data Scientist).

The legend below is short form description for this page.

| Symbols | Description |
| :---: | :--- | 
| $S$ | Total token Supply (Prize Pool) |
| $s$ | Agent token Supply |
| $\tau$ | An agent's private belief of the likelihood of a collision |
| $\Xi$ | The system's approximation of the likelihood of a collision |
| $P$ | Token price |
| $\omicron_{win}$ | An agent's claims on payouts conditioned on a win |
| $\omicron_{loss}$ | An agent's claims on payouts conditioned on a loss |
| $\Omicron$ | Total payout at Auction Settlement (Prize Pool)|


## System Specification
## State Variables

All system state variables for the simulation are outlined below and have been defined in the Engineering [Requirements](5_Requirements.md) Section.

* Supply ($S$)
* Price ($P$)
* Probability of Collision, $P_c\;$ ($\Xi$)
* Claim on auction settlement ($\Omicron$)


## Parameters

The total token supply $S$ and total payout at auction settlement $\Omicron$ are the same but rather used based on the time period throughout the auction tournament. They both represent the prize pool.

$$
    Prize\;Pool = S \;\;\;\;\;\;\;\; for \;\; t \;\epsilon \; [0, \; T_{threshold}] 
$$

$$
    Prize\;Pool = \Omicron \;\;\;\;\;\;\;\; for \;\; t \;\epsilon \; [T_{threshold}, \; T] 
$$

The prize pool is known to all bidding agents prior, throughout and the end of the auction. It is an invariant.

