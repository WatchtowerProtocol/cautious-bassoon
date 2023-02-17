# 🕵️ System Specification

In this section the system specification is detailed for the system. This includes mathematical definitions, relations and specifications pertaining to the digital twin.

## Symbolic Representation

All definitions of the symbolic representation definitions have been described in the Engineering [Requirements](5_Requirements.md) Section. All upper case letters represent variables from the perspective of the system (Auction Tournament) while lower case letters represent variables from the perspective of the bidding agent (Data Scientist).

The legend below is short form description for this page.

| Symbols | Description |
| :---: | :--- | 
| $S$ | Total token Supply (Prize Pool) |
| $s$ | Agent token Supply |
| $\xi$ | An agent's private belief of the likelihood of a collision represented as the amount of tokens staked to bid on their model's performance. |
| $\Phi$ | Total Staked pool of tokens by bidding agents |
| $\Xi$ | The system's approximation of the likelihood of a collision |
| $P$ | Token price |
| $\omicron_{win}$ | An agent's claims on payouts conditioned on a win |
| $\omicron_{loss}$ | An agent's claims on payouts conditioned on a loss |
| $\Omicron$ | Total payout at Auction Settlement (Prize Pool)|
| $\psi$ | The fee associated with running the auction tournament charged by WatchtowerDAO |


## System Specification
### State Variables

All system state variables for the simulation are outlined below and have been defined in the Engineering [Requirements](5_Requirements.md) Section.

* Supply ($S$)
* Price ($P$)
* Probability of Collision, $P_c\;$ ($\Xi$)
* Probability of Collision Threshold, $P_{c(threshold)}\;$ ($\Xi_{threshold}$)
* Claim on auction settlement ($\Omicron$)
* Auction Fee charged by WatchtowerDAO ($\psi$)
* Auction Threshold time. ($T_{threshold}$)
* Auction End time. ($T$)


### Parameters

The total token supply $S$ and total payout at auction settlement $\Omicron$ are the same but rather used based on the time period throughout the auction tournament. They both represent the prize pool.

$$
    Prize\;Pool = S \;\;\;\;\;\;\;\; for \;\; t \;\epsilon \; [0, \; T_{threshold}] 
$$

$$
    Prize\;Pool = \Omicron \;\;\;\;\;\;\;\; for \;\; t \;\epsilon \; [T_{threshold}, \; T] 
$$

The prize pool is known to all bidding agents prior, throughout and the end of the auction. It is an invariant.

## States
We describe the mathematical equations associated at system-level and agent-level for different states of the tournament lifecyle.

### Auction Creation

The auction creation and initialisation states can be prone to occurring at the same time. At this state, a factory contract creates a new auction contract with a predetermined prize pool which is the total supply of tokens minted for the tournament. Other variables are also set, shown in the equations below.

| State Equation | At auction creation... |
| :---: | :--- | 
| $\; S = Prize\;Pool \;$ | the prize pool is the total supply of tokens for the tournament. |
| $T = TCA$ |  the Time of Closest Approach (TCA) is confirmed and set at the length of the entire tournament inclusive of settlement. |
| $\Xi = 0 $ |  the system's approximation of the likelihood of a collision risk is set to zero. |
| $\psi = 0.00698$ |  the auction fee is set to $0.698\,\%$ of the final settlement payout which can be changed any time via DAO governance. |



### Auction Initialisation

At this state, initial conditions are set for the tournament to execute.

| State Equation | At auction intialisation... |
| :---: | :--- | 
| **Initial Conditions**  ||
| $\Xi_{threshold} = false$ |  the threshold of the system's approximation of the likelihood of a collision (which is $10^{-5}$) is set to false. |
| $T_{threshold}\; =\; T\; -\; 2\; days\;$ |  the threshold time for the tournament is set to $2\;days$ before settlement. |

### Auction Execution

During this state, two mechanisms are a play, the equations to both outlined under the Mechanisms subsection below. These are:
1. Stake-to-Bid: Agents deposit their tokens into the contract to bid on their model's performance.
2. Unstake-to-Withdraw: Agents remove full or partial amounts of their tokens from the contract as many times they wish prior to the threshold time of the tournament.


### Auction Settlement

At this state, settlement conditions must be met in the 2 day window between threshold time and TCA.

| State Equation | At auction settlement... |
| :---: | :--- | 
| **Settlement Conditions**  |
| $ 10^{-4} > \Xi_{threshold} > 10^{-5} \: $ |  the threshold of the system's approximation of the likelihood of a collision (which is $10^{-5}$) is set to false. |
| $T_{threshold}\; <\; T\; $ |  the threshold time for the tournament is set to $2\;days$ before settlement. |
| $\Omicron\; = Prize\;Pool \;$ | Total payout at Auction Settlement (Prize Pool)|
| $\omicron_a =  (\, \Omicron \ast \frac{\xi}{\Phi} \,) + \xi \,    \iff \omicron_a \Rightarrow \omicron_{win} $ | An agent's claims on payouts conditioned on a win and their stake returned ($+\xi$). |
| $\omicron_a =  0 + (-\xi) \iff \omicron_a \Rightarrow \omicron_{loss} $ | An agent's claims on payouts conditioned on a loss and their stake burned ($-\xi$). |



## Mechanisms
We describe the mathematical equations associated with the mechanisms that exist throughout the entirety of the tournament lifecycle.

### Stake-to-Bid

The system $P_c$ currently *will not update* during the auction execution phase

| State | Equation |
| :---: | :--- | 
| **System-Level** |  |
| System Supply | $S_{t+1} = S_t + \Delta S_t$ |
| System $P_c$ | $\Xi_{t+1} = \Xi_{t}$  |
| **Agent-Level** |  |
| Agent Supply | $s_{t+1} = s_t - \Delta S_t$ |
| Agent $P_c$ belief | $\xi_{t+1} = \Epsilon\,[\,{\xi_{t}\mid (c_{t}, \Omicron)\,]}  $ |

An agent's expected belief of $P_c$ is based on their private belief during the auction ($\xi_t$) conditioned upon confidence in their own modeling during the auction execution phase ($c_t$) and the prize pool value ($\Omicron$).

### Unstake-to-Withdraw

The system $P_c$ *only updates* during the auction settlement phase.

| State | Equation |
| :---: | :--- | 
| **System-Level** |  |
| System Supply | $S_{t+1} = S_t - \Delta S_t$ |
| System $P_c$ | $\Xi_{t+1} = \Xi_{t}$  |
| **Agent-Level** |  |
| Agent Supply | $s_{t+1} = s_t + \Delta S_t$ |
| Agent $P_c$ belief | $\xi_{t+1} = \Epsilon\,[\,{\xi_{t}\mid (c_{t}, \Omicron)\,]}  $ |


### Claim-to-Settle
When agents stake their tokens, they are making a bet on their ability to model collision risk accurately. As such, they submit their model, which provides their private belief of $P_c$ ($\,\xi\,$) and the performance of their model which is evaluated using the $logloss$ parameter that is a decent measure for binary classification problems.

| State | Equation |
| :---: | :--- | 
| **System-Level** |  |
| System Payout | $\Omicron = \Omicron_{win} + \Omicron_{loss}$ |
| System $P_c$ | $\Xi \in \R ,\,\,  10^{-4} > \Xi > 10^{-5} $ |
| System $logloss$ | $\Alpha \in \R ,\:\,  -\ln(0.5) < \Alpha <-\ln(0.5) $ |
| **Agent-Level** |  |
| Agent Supply | |
| Agent $P_c$ belief | |
