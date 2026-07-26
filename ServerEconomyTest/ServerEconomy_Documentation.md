# 🌟 ServerCoin Economy - Official Player Guide 🌟

Welcome to the **ServerCoin (SC)** economy! We have completely overhauled how money, trading, and jobs work on the server. Say goodbye to the days of dropping valuable items on the ground and hoping you don't get scammed. 

Our server now runs a custom, fully automated, **player-driven economy** inspired by real-world decentralized finance (DeFi). The server admins don't control the prices, and money doesn't come from infinite admin shops. You, the players, dictate the entire market!

Here is everything you need to know to get started, earn money, and trade safely.

---

## ⛏️ 1. Earning ServerCoin (Dynamic Quests)
Money doesn't come from nothing. To introduce new ServerCoin into the world, you just have to play the game!

* **Auto-Tracking:** When you join the server, you are secretly assigned a random **Dynamic Quest** (e.g., *Mine 128 Stone, Eat 32 Bread, Catch 5 Fish*). You don't need to type any commands to start or finish these. The server tracks your actions automatically in the background.
* **Minting Rewards:** When you finish a quest, you are instantly rewarded with fresh **ServerCoin**, and a new quest begins. 

⚠️ **The Catch (Scarcity & Halving):** 
There is a hard limit of **1,000,000 SC** that can ever exist. As more coins are created and the "Unmined Pool" shrinks, the amount of SC you get per quest will periodically cut in half (just like Bitcoin's halving). **Get in early while the payouts are high!**

---

## 🏦 2. The Emerald Exchange (Supply & Demand)
Need digital ServerCoin but only have physical Emeralds? Or do you have too much ServerCoin and want Emeralds to trade with Villagers? Use the **Emerald Exchange**!

* This isn't a normal shop. The exchange uses a mathematical robot (an Automated Market Maker) that changes the price based purely on **Supply and Demand**.
* If players dump thousands of Emeralds into the exchange, Emeralds become cheap.
* If players buy up all the Emeralds, they become rare and expensive! 

**Commands:**
* `/swap emerald <amount>` - Sell your physical emeralds for SC.
* `/swap coin <amount>` - Spend your SC to get physical emeralds.

---

## 🤝 3. Trustless Trading (Market & P2P)
Never throw a diamond sword on the ground again! We have introduced **Scam-Proof Trading**. The server acts as a robotic middleman that instantly trades the items and the money at the exact same time.

### Method A: The Global Market (Auction House)
Want to sell something while you are offline?
* **Sell:** Hold an item and type `/market sell <price>`. The item is safely removed from your inventory and placed on the global board.
* **Buy:** Players can type `/market browse` to see what is for sale globally, and `/market buy <id>` to purchase it. The money goes straight to your balance, even if you are offline!
* **Cancel:** Changed your mind? `/market cancel <id>` instantly returns the item to you.

### Method B: Direct Player-to-Player Trading
Standing right next to someone and want to trade safely?
* **Offer for SC:** Hold your item and type `/ptrade offer <player> <price>`.
* **Offer for Item:** Hold your item and type `/ptrade itemswap <player>`. (The other player must be holding the item they want to trade back).
* **Accept/Deny:** The other player simply types `/ptrade accept` or `/ptrade deny`. The server swaps the items/money perfectly. If they deny, your item is safely returned to you.

---

## 📜 4. Smart Contracts & The Job Board
Need someone to clear a forest for you, or gather 10,000 netherrack? Don't want to pay them until the job is done? Use the **Contract System**!

* **Create a Job:** Type `/contract create <reward> <description>`. The server takes the reward money from your bank (plus a small 2 SC Validator Fee) and locks it in a secure vault.
* **Find a Job:** Players can type `/contract list` to see open jobs, and `/contract claim <id>` to accept one.
* **Get Paid:** When the worker finishes and types `/contract complete`, the creator types `/contract approve`. The vault unlocks, giving the worker the reward, and refunding the creator their 2 SC Validator Fee!

---

## ⚖️ 5. The Player Court (Jury Duty)
What if someone claims they finished a job, but they actually didn't? The creator can type `/contract dispute`.

* The job is immediately moved to the **Public Jury Board** (`/jury list`).
* Any random, 3rd-party player can claim the dispute (`/jury claim <id>`), look at the evidence/world, and vote on who gets the money (`/jury vote <id> <worker|buyer>`).
* **Why be a Juror?** The Juror gets paid the 2 SC Validator Fee for taking the time to resolve the conflict!

---

## ♻️ 6. The "Circular" Economy (Taxes)
You will notice tiny "taxes" or "fees" when you transfer coins (`/pay`), swap emeralds, or when a Juror rules in favor of the buyer. **These fees do NOT go to the admins!**

* Every single fee paid by a player is recycled directly back into the **Unmined Quest Pool**. 
* This ensures the server never actually runs out of money to pay players for doing quests, creating a perfect, eternal, circular economy!

---

## 📌 Command Cheat Sheet

### General Economy
* `/eco` - View the overall health of the server economy (total supply, unmined pool, current prices and fees).
* `/balance` (or `/bal`) - Check your current ServerCoin wealth.
* `/pay <player> <amount>` - Send coins to another player.
* `/swap <emerald|coin> <amount>` - Trade with the dynamic Emerald Exchange.

### Global Market
* `/market browse` - View all items currently for sale.
* `/market sell <price>` - List the item in your hand on the market.
* `/market buy <id>` - Purchase a listed item.
* `/market cancel <id>` - Cancel your listing and get your item back.

### P2P Trading
* `/ptrade offer <player> <amount>` - Offer the item in your hand to another player for SC.
* `/ptrade itemswap <player>` - Offer to swap the item in your hand for the item in their hand.
* `/ptrade accept` - Accept a pending trade.
* `/ptrade deny` - Deny a pending trade.

### Contracts & Jobs
* `/contract list` - View all open jobs.
* `/contract create <reward> <description>` - Create a new job and lock funds in escrow.
* `/contract claim <id>` - Accept a job. 
* `/contract complete <id>` - Mark a job as finished (waiting for approval).
* `/contract approve <id>` - Approve a finished job and release the funds to the worker.
* `/contract dispute <id>` - Send a job to the Player Court if the worker lied.

### Jury System
* `/jury list` - View all disputed contacts.
* `/jury claim <id>` - Volunteer to be the judge for a dispute.
* `/jury vote <id> <worker|buyer>` - Cast your final verdict and earn your Validator Fee!