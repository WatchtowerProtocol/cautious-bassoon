# ♻️ Tournament Lifecycle

In this section we define the interactions occuring in the tournament and the overall state transitions/changes occuring during the lifecycle of the Dora data science tournaments (the term auction(s) is used interchangeably with tournament(s)) and by extension in the broader Watchtower ecosystem. 

</br>

# Auction Creation
The creation state represents the creation of the tournament/auction. This is an auctions contract for a specific tournament and is typically performed programmatically by a Factory contract. The creation of an auction sets initial parameters for the auction such as auction end time (Time of Closest Approach). The main role responsible is the Auctions Owner which in this instance is the WatchtowerDAO. 

On top of creating the auction contract, the public keys of all data scientists registered for the tournament are included as a security measure to ensure only those registered for the auction can participate.

## Transitions into Creation State
There are no transitions into Creation as this is the first state.

## State Inputs
There are no inputs that effect this state.

## State Outputs
There are outputs created in this state mentioned below:
* An Auction Start Time
* An Auction End Time
* A Risk (Pc) Threshold
* A Token Supply to Mint for the Auction
* A Maximum Reserve Ratio for the Bonding Curve
* A Minimum Reserve Ratio for the Bonding Curve
* An Auction Fee

## Transition out of Creation State
At the end of this state, a new auction contract is created (deployed) by the Factory contract. The contract will include state variables for the tournament which have been listed in the Outputs subsection above.

</br>

# Auction Initialisation

## Transitions into Initialisation State

## State Inputs

## State Outputs

## Transition out of Initialisation State

</br>

# Auction Execution

## Transitions into Execution State

## State Inputs

## State Outputs

## Transition out of Execution State

</br>

# Auction Settlement

## Transitions into Settlement State

## State Inputs

## State Outputs

## Transition out of Settlement State

</br>

> _**Please Note** that there will be a couple other states in between Execution and Settlement to account for programmatic Dispute Resolution. For the current version, settlement is rather a simple stake-weighted aggregation of risk and the subsequent threshold. These phases will be implemented with the inclusion of the data oracle (Laika) to transition tournaments more real-time._