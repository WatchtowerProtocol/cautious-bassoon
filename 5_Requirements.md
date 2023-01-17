# 🗒️ Engineering Definitions & Requirements

In this section definitions and requirements are detailed for the system. Requirements for system variables, associated mechanisms, actors' admissible actions, initial and settlement conditions.

</br>
<a name="defs"></a> 

# Definitions

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 1. | State Space | Collection of Auction states at any point during the Auction lifecycle | $X$ |
| 2. | State | Configuration of the Auction at a given point in time where $x\;\epsilon\;X$ | $x$ | 
| 3. | Address | An index of shared state that represents actions taken by an agent where $a\;\epsilon\;A$ | $a$ | 
| 4. | Set of Addresses | A set of addresses for a given set of agents | $A$ |
| 5. | Local state space | A subset of the state space $X$ where an agent has influence as represented by their address ($X_a\,\subseteq\,X$)| $X_a$ |
| 6. | Action | Represents a admissible action by an agent that may influence the state of the system | $u_a$ |
| 7. | Set of Feasible Actions | A set of feasible action for an agent in their local state space $X_a$ where, $u_a\:\epsilon\:U$| $U$ |
| 8. | Mechanism | A mapping of either individual or a set of states and addresses where  | $F$ |
| 9. | Time Step | A time step is defined as one block  | $t$ |
| 10. | Auction Time Period | The entire time period for a tournament defined by the Time to Closest Approach (TCA) where $t\:\epsilon\:T$ | $T$ |
| 11. | Reserve | The total WTR bonded to the bonding curve contract where $R_t$ is the reserve at time $t$ during the tournament.  | $R$ |
| 12. | Supply | The total WTR supplied for a tournament issued by the bonding curve where $S_t$ is the supply at time $t$ during the tournament.  | $S$ |
| 13. | Price | The estimate of the value of WTR token where $P_t$ is the price at time $t$ during the tournament. | $P$ |
| 14. | Risk Score | This state variable is the estimate of the probability of collision ($P_c$) of the conjunction event where $P_c\,\epsilon\,[0,1]$ and when $P_c=0$, it indicates no collision while $P_c=1$ indicates the highest likelihood of collision. | $P_c$ |
| 15. | Reserve Ratio | This is the ratio of the reserve over the localised market cap. ($P * S$ ) or $\phi = R/(P*S)$  | $\phi$ |
| 16. | Risk Threshold | This is the minimum risk score required to determine whether a collision avoidance manoeuvre is necessary or not.  | $P_{c(threshold)}$ |
| 17. | Auction Time Threshold | This is the maximum allowable time required for the tournament to exist.  | $T_{(threshold)}$ |

</br>

# System Requirements
#### Requirement 1
The economic mechanisms associated with the tournaments shall only incentivise behaviours that achieve the system's mandate and goals.

#### Requirement 2
All actors in the tournament shall be contrained in their action space to meet the system mandate and goals.

#### Requirement 3
The incentives associated to all admissible actions & thereby behaviours in the tournament are all contained within the bonding curve mechanism of the system as per its mandate and goals.

#### Requirement 4
All variables at initialisation and settlement are conditioned upon the system's mandate and goals.


## State Variables

* System State
* Timestep
The timestep is the block time of the settlement layer. The block time is the time taken to create a block containing a list of transactions. These transactions are a result of agent actions
* Token Reserve
* Token Supply
* Risk Score/Probability of Collision (Pc)
* Tournament End Time
* Reserve Ratio
* Token Price


## Mechanisms

* Stake-to-Bid
* Burn-to-Withdraw
* Claim-to-Settle

## Initial Conditions

* Must set Tournament End Time Threshold to TCA


## Settlement Conditions

* Tournament End Time Threshold shall be met as a hard stop


# Actor/Agent Actions
Agents are defined as per [definition 6](#defs) where they are represented by an address $a$ taking a admissible actions $u$ at a time step $t$. An agent can carry out a set of admissible actions over the entire tournament time period $T$ represented by a list of transactions (a set of addresses, $A$).

## Bidding Agent
The Data Scientists take on the role as Bidding agents and are provided with admissible actions to execute mechanisms inside the tournament.

#### Operational Requirement 1
Bidding agents shall be able to call the stake, burn and claim actions.

#### Operational Requirement 2
Bidding agents shall only be able to execute Stake-to-Bid, Burn-to-Withdraw and Claim-to-Settle mechanisms.

## Auction Moderator Agent
The Dora smart contract takes on the role as the Auction/Tournament Moderator Agent and is programmed to administer the auction/tourament for each conjunction event. It is also the owner of the auction throughout the tournament until settlement.

#### Operational Requirement 3
The moderator agent shall create, initialise and settle the auction/tournament for an individual conjunction event.

#### Operational Requirement 4
The moderator agent shall determine and mint the prize pool and subsequent token supply, respectively, for the tournament bonding curve.

#### Operational Requirement 5
The moderator agent shall broadcast the final risk score and threshold to be updated on the conjunctions dashboard at settlement.


## Auction Outcomes Agent
The Dora smart contract takes on the role as the Auction/Tournament Outcomes Agent and is programmed to determine, distribute and settle the outcome of auction/tourament for each conjunction event.

#### Operational Requirement 6
The outcomes agent shall determine the rewards to be distributed for the auction/tournament.

#### Operational Requirement 7
The outcomes agent shall distribute the rewards to the auction/tourament winners and burn any stakes of the losers.



</br>

> _**Please Note** that algorithmic dispute resolution has not been modelled into this iteration of the marketplace. For the current version, settlement is rather a simple stake-weighted aggregation of risk and the subsequent threshold. Programmatic dispute resolution requirements and definitions will be added with the inclusion of the data oracle (Laika) to transition tournaments more real-time._

[^1]: Zargham, M., Shorish, J., & Paruch, K. (2019). From Curved Bonding to Configuration Spaces. (Working Paper Series / Institute for Cryptoeconomics / Interdisciplinary Research).