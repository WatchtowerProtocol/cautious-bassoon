# 🗒️ Engineering Definitions & Requirements

In this section definitions and requirements are detailed for the system. Requirements for system variables, associated mechanisms, actors' admissible actions, initial and settlement conditions.

<!-- </br>
<a name="defs"></a>  -->

# Definitions

<!-- <br /> -->

> All definitions associated with the Reserve and Reserve Ratio, while defined in this document, won't be applied to version 1. A bonding curve with a reserve ratio will be introduced in v2 to allow bidding agents to enter auctions without the need of buying Watchtower tokens. Therefore, in v2 any loss in an auction will result in an staked amount equivalent of Watchtower tokens being burned.

<!-- <br /> -->

## State Variables

#### System State

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 1. | State Space | Collection of states of an Auction at any point during its lifecycle | $X$ |
| 2. | State | Configuration of the Auction at a given point in time where $x_t\;\epsilon\;X$ | $x_t$ | 
| 3. | Address | An index of shared state that represents actions taken by an agent where $a\;\epsilon\;A$ | $a$ | 
| 4. | Set of Addresses | A set of addresses for a given set of agents | $A$ |
| 5. | Local state space | A subset of the state space $X$ where an agent has influence as represented by their address ($X_a\,\subseteq\,X$)| $X_a$ |
| 6. | Set of Admissible Actions | A set of admissible actions agents can take in their local state space $X_a$ where, $u_a\:\epsilon\:U$| $U$ |


#### Agent-level State

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 7. | State Space | Collection of agent-level states at any point during the Auction lifecycle | $X_a$ |
| 8. | State | Configuration of the agent-level state at a given point in time. | $x_{a,t}$ | 
| 9. | Action | Represents a admissible action by an agent that may influence the state of the system at a point in time. | $u_{a,t}$ |

#### Timestep

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 10. | Time Step | The timestep is the block time of the settlement layer. The block time is the time taken to create a block containing a list of transactions as a result of agents' admissible actions associated with their addresses.  | $t$ |

#### Token Reserve

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 11. | Reserve | $R_t$ is the reserve at time $t$ during the tournament. This exists so bidding agents aren't tied to buying Watchtower tokens to participate.  | $R$ |

#### Token Supply

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 12. | Supply | $S_t$ is the supply at time $t$ during the tournament. | $S$ |


#### Risk Score/Probability of Collision (Pc)

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 13. | Risk Score | This state variable is the estimate of the probability of collision ($P_c$) of the conjunction event where $P_c\,\epsilon\,[0,1]$ and when $P_c=0$, it indicates no collision while $P_c=1$ indicates the highest likelihood of collision. | $P_c$ |

#### Tournament End Time

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 14. | Auction Time Period | The entire time period for a tournament defined by the Time to Closest Approach (TCA) where $t\:\epsilon\:T$ | $T$ |

#### Reserve Ratio

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 15. | Reserve Ratio | This is the ratio of the reserve over the localised market cap. ($P * S$ ) or $\phi = R/(P*S)$  | $\phi$ |

#### Token Price

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 16. | Price | The estimate of the value of the token where $P_t$ is the price at time $t$ during the tournament. | $P$ |


## Mechanisms

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 17. | Mechanism | A mapping of either individual or a set of states and addresses where  | $\digamma$ |

## Constraints

| # | Name | Description | Symbolic Representation | 
| :--- | :--- | :--- | :---: | 
| 18. | Risk Threshold | This is the minimum risk score required to determine whether a collision avoidance manoeuvre is necessary or not.  | $P_{c(threshold)}$ |
| 19. | Auction Time Threshold | This is the maximum allowable time required for submissions to be made where $T_{(threshold)} = T - 2 days$  | $T_{(threshold)}$ |

</br>

# System Requirements
#### Requirement 1
The economic mechanisms associated with the tournaments shall only incentivise behaviours that achieve the system's mandate and goals.

#### Requirement 2
All actors in the tournament shall be contrained in their action space to meet the system mandate and goals.

#### Requirement 3
The incentives associated to all admissible actions & thereby behaviours in the tournament are all contained within the mechanism of the system as per its mandate and goals.

#### Requirement 4
All variables at initialisation and settlement are conditioned upon the system's mandate and goals.




## Mechanisms
There are three main mechanisms associated with the tournament where the former two are occur during the tournament and the latter last at the conclusion of it.

$$ \digamma \coloneqq \{ f_{stake}, f_{burn}, f_{claim}  \} $$

### Stake-to-Bid
The stake-to-bid mechanism adds Watchtower tokens as designated by the bidding agent (data scientist) into the auctions contract. The agent's action ($u_{a,t}$) transfers $\Delta S_t$ Watchtower tokens into the auction contract at time $t$.

The System-level (perspective) state after the admissible action is performed is now:
$$
    S_{t+1} = S_t + \Delta S_t
$$
The Agent-level (perspective) state after the admissible action is performed is now:
$$
    s_{a,t+1} = s_t - \Delta S_t
$$

#### Requirement 5
The action to stake-to-bid shall add a quantity of $\Delta S_t$ tokens at time $t$ to the auctions contract.

### Burn-to-Withdraw
The burn-to-withdraw mechanism removes Watchtower tokens as designated by the bidding agent (data scientist) out of the auctions contract. The agent's action ($u_{a,t}$) transfers $\Delta S_t$ Watchtower tokens out of the auction contract at time $t$.

The System-level (perspective) state after the admissible action is performed is now:
$$
    S_{t+1} = S_t - \Delta S_t
$$
The Agent-level (perspective) state after the admissible action is performed is now:
$$
    s_{a,t+1} = s_t + \Delta S_t
$$

#### Requirement 6
The action to burn and withdraw shall remove a quantity of $\Delta S_t$ tokens at time $t$ out of the auctions contract.

### Claim-to-Settle

#### Requirement 7

## Initial Conditions

### Tournament Time Threshold
The Auction/Tournament Time Threshold needs to be set prior to a state transition into the Creation, Initialisation and eventual commencement of the Auction/Tournament. This is based on the Time of Closest Approach and a margin of 2 days are defined above.

$$
T_{(threshold)} = T - 2 days
$$

### Risk Threshold
The Risk Threshold isn't as important at initialisation for a state transition but is defaulted to zero. As per guidance[^1], a conservative threshold is a $P_c > 10^{-5}$ or 1 in 10,000. Thresholds generally range between $ 10^{-4} > P_c > 10^{-5} \: $. The threshold for the tournament is initialised to zero and is determined during the course of the tournament but set to the range defined.

<br/>

$$
P_{c(threshold)} = 0
$$

<br/>

$$
where \;  P_{c(threshold)} \epsilon \; [10^{-4}, 10^{-5}]
$$

## Settlement Conditions

### Tournament Time Threshold
For a successful settelment, the Auction/Tournament shall prohibit submissions from bidding agents 2 days prior to the auction/tournament end time (or) the Time to Closest Approach, TCA ($T$). This will be a programmatic hard stop to ensure a margin is assured for both programmatic dispute resolution (in a future version of the tournament) and time to prepare for collision avoidance manoeuvres.

$$
T_{(threshold)} < T
$$

### Risk Threshold
For a successful settlement of the auction, the $P_{c(threshold)}$ shall be within the range guidance [^1] prior the Time to Closest Approach ($T$) and at the tournament time threshold ($T_{(threshold)}$).

<br/>

$$
P_{c(threshold)} \; \epsilon \; [10^{-4}, 10^{-5}]
$$

<br/>

$$ \lim_{0\to T_{\;(threshold)}}P_c  \; = \;   P_{c\;(threshold)} $$


# Actor/Agent Actions
Agents are represented by an address $a$ taking a admissible actions $u$ at a time step $t$. An agent can carry out a set of admissible actions over the entire tournament time period $T$ represented by a list of transactions (a set of addresses, $A$).

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
The moderator agent shall determine and mint the prize pool and subsequent token supply, respectively, for the auction tournament.

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


[^1]: (2020). NASA Spacecraft Conjunction Assessment and Collision Avoidance Best Practices Handbook. National Aeronautics and Space Administration
<!-- [^2]: Zargham, M., Shorish, J., & Paruch, K. (2019). From Curved Bonding to Configuration Spaces. (Working Paper Series / Institute for Cryptoeconomics / Interdisciplinary Research). -->