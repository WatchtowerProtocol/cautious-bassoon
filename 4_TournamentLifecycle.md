# ♻️ Tournament Lifecycle

In this section we define the interactions occuring in the tournament and the overall state transitions/changes occuring during the lifecycle of the Dora data science tournaments (the term auction(s) is used interchangeably with tournament(s)) and by extension in the broader Watchtower ecosystem. 

</br>

# Creation State
The creation state represents the creation of the tournament/auction. This is an auctions contract for a specific tournament and is typically performed programmatically by a Factory contract. The creation of an auction sets initial parameters for the auction such as auction end time (Time of Closest Approach). This is primarily conducted by the Auctions Owner which in this instance is the Watchtower Foundation with the eventual transition to the DAO. 

On top of creating the auction contract, the public keys of all data scientists registered for the tournament are included as a security measure to ensure only those registered for the auction can participate.

## Transitions into Creation State

## State Inputs

## State Outputs

## Transition out of Creation State

</br>

# Initialisation State

## Transitions into Initialisation State

## State Inputs

## State Outputs

## Transition out of Initialisation State

</br>

# Execution State

## Transitions into Execution State

## State Inputs

## State Outputs

## Transition out of Execution State

</br>

# Settlement State

## Transitions into Settlement State

## State Inputs

## State Outputs

## Transition out of Settlement State

</br>

> _**Please Note** that there will be a couple other states in between Execution and Settlement to account for programmatic Dispute Resolution. For the current version, settlement is rather a simple stake-weighted aggregation of risk and the subsequent threshold. These phases will be implemented with the inclusion of the data oracle (Laika) to transition tournaments more real-time._