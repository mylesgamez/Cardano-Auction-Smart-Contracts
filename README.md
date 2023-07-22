# Cardano Plutus Auction Contract

This repository contains the implementation of an auction contract for the Cardano blockchain using Plutus smart contracts. The contract provides a mechanism for users to create auctions, place bids, set a deadline for bidding, and close the auction after the deadline. 

## Introduction

The smart contract implementation is split into two main parts:

- `Offchain.hs`: Contains the implementation of off-chain code that defines transactions for creating offers, bidding, setting a deadline, and closing the auction.
- `Onchain.hs`: Contains the on-chain code that validates the transactions made off-chain.

## Prerequisites

- GHC (The Glasgow Haskell Compiler)
- Plutus package

## Overview of the Auction Process

There are four transactions involved in this contract:

1. **Making an Offer**: Anyone who wishes to sell something can pay it to the 'auctionValidator' with the 'Offer' datum specifying the seller's address and the minimum bid. 
2. **Setting the Deadline**: This transaction consumes the offer UTxO and returns a 'NoBids' UTxO to the auction validator. It also mints the thread NFT that ensures the authenticity of the auction from that point onwards.
3. **Bidding**: This transaction consumes a 'NoBids' or 'Bidding' UTxO, and returns an UTxO with a higher value to the validator with a 'Bidding' datum recording the new highest bid and bidder. If there was a previous bidder, they are paid back their bid.
4. **Closing the Auction**: This transaction consumes an UTxO at the 'auctionValidator', pays the Ada amount corresponding to the highest bid to the seller, and the value originally offered to the highest bidder. If there were no bids, the offer is returned to the seller.

For more technical details and explanations, refer to the comments in the source code.

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
