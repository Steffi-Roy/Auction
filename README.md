## Decentralized Token Auction Smart Contract
A lightweight Solidity smart contract that implements a fixed-capacity, token-based auction system. Users register to receive a set allocation of bidding tokens, place bids on available items, and the contract beneficiary triggers a pseudo-random drawing to select winners based on the weight of the bids.

## 📌 Architecture & Design Rules
The contract operates under strict architectural rules, likely designed for a specialized classroom lab or constrained testing environment:

Fixed Participants: The system relies on a fixed array size of exactly 4 bidders.

Fixed Item Pool: There are exactly 3 auction items available for bidding (IDs: 0, 1, 2).

Capped Token Supply: Every registered user receives exactly 5 bidding tokens.

Weight-Based Lottery: Every token bid acts as a raffle ticket. If you bid 3 tokens on an item, your personId is entered 3 times into that item's pool, increasing your pseudo-random chances of winning.

🛠 Features & Functions
1. Initialization (Constructor)
Auction(): Sets the deploying wallet address as the beneficiary (owner) and initializes the 3 auction items with empty bidding history arrays.

2. Participant Registration
register(): Registers an external wallet into the auction.

Tracks participant counts up to 4.

Grants the wallet exactly 5 tokens to spend.

3. Bidding System
bid(uint _itemId, uint _count): Allows a registered user to allocate their tokens to a specific item.

Validates that the user has enough remainingTokens.

Validates that the _itemId is valid (0, 1, or 2).

Pushes the bidder's ID into the item's raffle pool multiple times based on the token count.

4. Winner Determination
revealWinners(): An admin-only function guarded by the onlyOwner modifier.

Calculates a pseudo-random winning index using the block number (block.number) against the total pool of tokens spent on that item.

Saves the winning bidder's wallet address into the public winners array.
