# ♻️ Tournament Lifecycle

In this section we define the interactions occuring in the tournament and the overall state transitions/changes occuring during the lifecycle of the Dora data science tournaments (the term auction(s) is used interchangeably with tournament(s)) and by extension in the broader Watchtower ecosystem. 

</br>

# Auction Creation
<p>Summary: Creates a tournament/auction.</p>
<p>Responsibility: Auction Owner (i.e. WatchtowerDAO/Foundation)</p>
<p>Description: The creation process is typically performed programmatically by a Factory contract. The creation of an auction involves creating an auctions contract with the necessary state variables for the auction such as auction end time (Time of Closest Approach [TCA]). In addition to this, the public keys of all data scientists registered for the tournament are included as a security measure to ensure only those registered for the auction can participate. 

> Please note that the states of Auction Creation and Initialisation can happen concurrently at the smart contract abstraction level.

## Transitions into Creation State
There are no transitions into Creation as this is the first state. At this stage, 
* The conjunction event is known and established to determine the TCA.

## State Inputs
There are no inputs that effect this state.

## State Outputs
There are outputs created in this state mentioned below:
* An Auction Start Time
* An Auction End Time
* A Risk (Pc) Score (a value between 0 and 1)
* A Risk (Pc) Threshold (a boolean)
* A Token Supply to Mint for the Auction
* A Maximum Reserve Ratio for the Bonding Curve
* A Minimum Reserve Ratio for the Bonding Curve
* An Auction Fee

## Transition out of Creation State
At the end of this state, a new auction contract is created (deployed) by the Factory contract. The contract will include state variables for the tournament which have been listed in the Outputs subsection above.

</br>

# Auction Initialisation
 <p>Summary: Sets the initial parameters of the auction.</p>
 <p>Responsibility: Auction Moderator/Admin (i.e. WatchtowerDAO/Foundation)</p>
 <p>Description: During the initialisation process, the moderator/admin initialises all parameters of the auction such as minting the required tokens based on the max. and min. reserve ratios as part of the bonding curve, establishing the fee, the end time at the Time of Closest Approach (TCA) and set all the permitted participant addresses in the auction.</p>

## Transitions into Initialisation State
All outputs from the previous state are used as inputs in this state. An events call is emitted to indicate the auctions contract has been created. At this stage, 
* The prize pool tokens supply is calculated.
* The Time to Closest Approach (TCA) is known.

## State Inputs
* An Auction Start Time
* An Auction End Time
* A Risk (Pc) Score
* A Risk (Pc) Threshold
* A Token Supply to Mint for the Auction
* A Maximum Reserve Ratio for the Bonding Curve
* A Minimum Reserve Ratio for the Bonding Curve
* An Auction Fee

## State Outputs
* Sets the Auction Start Time to 24 hours from Auctions Initialisation.
* Sets the Auction End Time to the TCA of conjunction event.
* Sets the Risk (Pc) Score to null
* Sets the Risk (Pc) Threshold to false
* Sets the Maximum Reserve Ratio for the Bonding Curve
* Sets the Minimum Reserve Ratio for the Bonding Curve
* Sets the Auction Fee
* At the very end, mints the Token Supply for the Auction based on annual issuance rate


## Transition out of Initialisation State
The state variables are all calculated and set for the execution of the Auction/Tournament. An events call is emitted to indicate the auctions contract has been initialised and ready for execution.

</br>

# Auction Execution
<p>Summary: The Auction is in process/being conducted.</p>
<p>Responsibility: Auction Moderator/Admin (i.e. WatchtowerDAO/Foundation)</p>
<p>Description: The auction execution state occurs for the length of the auction start and end time (TCA) as initialised in the prior state. In this state, data scientists are actively modelling and submitting/uploading their models, staking and unstaking their personal allocation of tokens with their subsequent submitted models and establishing a confidence score with their submissions. The risk score (Pc) and risk threshold is constantly being aggregated based on the weighted average staked and submitted models with an expected reliable score and threshold closer to the end of the auction (TCA).</p>

## Transitions into Execution State
On an event trigger that indicates the initialisation of the Auction, a separate event trigger indicating Auction Execution is emitted. At this stage, 
* The prize pool tokens are minted
* The maximum and minimum Reserve Ratios are set.
* The Auction End time is set.

## State Inputs
* The Auction Start Time is set to 24 hours after Auctions Initialisation.
* The Auction End Time is set to the TCA of conjunction event.
* The Risk (Pc) Score is set to  null
* The Risk (Pc) Threshold is set to false
* The Maximum Reserve Ratio is set for the Bonding Curve
* The Minimum Reserve Ratio is set for the Bonding Curve
* The Auction Fee is set.
* The prize pool tokens are minted

## State Outputs
* The staked-to-confidence ratio is recorded.
* The Risk (Pc) Score is updated.
* The Risk (Pc) Threshold is updated.
* The Reserve Ratio is set updated.

## Transition out of Execution State
The state variables are all updated and set for the settlement of the Auction/Tournament. An events call is emitted to indicate the auctions has been concluded and ready for settlement.

</br>

# Auction Settlement
<p>Summary: The Auction has ended and settled.</p>
<p>Responsibility: Auction Moderator/Admin (i.e. WatchtowerDAO/Foundation)</p>
<p>Description: At auction settlement, all staked tokens are released and if the data scientist wins the auction/tournament, part of the prize pool is distributed on top of their released token via a claim function. Prizes are distributed based on a staking-to-confidence score ratio established by the data scientist during the Auction. The risk score (Pc) and threshold are finalised in this settlement state which is subsequently published on a public conjunctions dashboard for spacecraft operators, insurance companies, etc.</p>

## Transitions into Settlement State

## State Inputs

## State Outputs

## Transition out of Settlement State

</br>

> _**Please Note** that there will be a couple other states in between Execution and Settlement to account for programmatic Dispute Resolution. For the current version, settlement is rather a simple stake-weighted aggregation of risk and the subsequent threshold. These phases will be implemented with the inclusion of the data oracle (Laika) to transition tournaments more real-time._