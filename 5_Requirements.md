# 🗒️ Engineering Definitions & Requirements

In this section the requirements are detailed for the defined system in the engineering model. Requirements for system variables, associated mechanisms, actors' admissible actions, initial and settlement conditions.

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

[^1]

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