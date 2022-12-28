# 🗒️ Requirements

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
* Token Reserve
* Token Supply
* Probability of Collision (Pc)
* Tournament End Time
* Reserve Ratio
* Token Price


## Mechanisms

* Stake-to-Bid
* Burn-to-Withdraw
* Claim

## Initial Conditions

* Must set Tournament End Time Threshold to TCA


## Settlement Conditions

* Tournament End Time Threshold shall be met as a hard stop


# Actor/Agent Actions

* Bidding Agent
* Auction Moderator Agent
* Auction Outcomes Agent



</br>

> _**Please Note** that algorithmic dispute resolution has not been modelled into this iteration of the marketplace. For the current version, settlement is rather a simple stake-weighted aggregation of risk and the subsequent threshold. Programmatic dispute resolution requirements and definitions will be added with the inclusion of the data oracle (Laika) to transition tournaments more real-time._