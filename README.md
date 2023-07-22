# Cardano Crowdfunding Smart Contracts
This repository contains a comprehensive crowdfunding solution implemented through Cardano's Plutus smart contracts. It provides the necessary functionality to initiate a crowdfunding event, set a deadline, make bids, and close the event.

## Overview
The smart contracts in this project facilitate a bidding style crowdfunding model where:

Offer: Anyone who wishes to raise funds can start by making an offer. The offer is made by transferring the item that is up for bidding to the auctionValidator contract along with the Offer datum. The datum specifies the minimum bid and the address of the offerer (seller).

Set Deadline: The seller sets a deadline for the auction. This transaction consumes the Offer UTXO, and creates a NoBids UTXO at the auctionValidator.

Bid: Participants can bid on the item. Each bid should be greater than the previous one. This transaction consumes the NoBids or Bidding UTXO at the auctionValidator and returns a Bidding UTXO with a greater value and the updated highest bid and bidder.

Hammer (Close auction): After the deadline, the seller can close the auction. This transaction pays the highest bid amount to the seller and transfers the item to the highest bidder. If there were no bids, the item is returned to the seller.

## Setup
This project is built using Haskell and Plutus. Please ensure you have the latest versions of GHC, Cabal and Plutus installed on your system.

Clone this repository to your local machine and navigate into the project directory:
```
git clone https://github.com/yourusername/Cardano-Crowdfunding-Smart-Contracts.git
cd Cardano-Crowdfunding-Smart-Contracts
```

Install the necessary dependencies:
```
cabal update
cabal install
```

Compile the project:
```
cabal build
```

You can then interact with the contracts using the Plutus Playground or load them onto the Cardano blockchain.
