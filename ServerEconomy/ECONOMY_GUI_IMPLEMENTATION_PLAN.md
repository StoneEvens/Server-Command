# Economy GUI Implementation Plan

## Overview
Create a GUI-based economy system that parallels command-line interfaces, with a main menu for 9 economy features and sub-menus for complex actions (Contract, Jury, Market, P2P Trade).

---

## File Changes Required

### 1. **ServerEconomyConstants.sk** - Add GUI Labels and Lores
Add the following constant structures (following existing `{labels}` and `{lores}` pattern):

#### Main Economy GUI:
- `{labels::default::economy::title}` = "Economy"
- `{labels::default::economy::transfer::name}` with `{lores::default::economy::transfer}`
- `{labels::default::economy::swap::name}` with `{lores::default::economy::swap}`
- `{labels::default::economy::contracts::name}` with `{lores::default::economy::contracts}`
- `{labels::default::economy::jury::name}` with `{lores::default::economy::jury}`
- `{labels::default::economy::market::name}` with `{lores::default::economy::market}`
- `{labels::default::economy::ptrade::name}` with `{lores::default::economy::ptrade}`
- `{labels::default::economy::balance::name}` with `{lores::default::economy::balance}`
- `{labels::default::economy::info::name}` with `{lores::default::economy::info}`
- `{labels::default::economy::supply::name}` with `{lores::default::economy::supply}`

#### Contract Sub-Menu:
- `{labels::default::economy::contracts::submenu::title}` = "Contracts"
- `{labels::default::economy::contracts::submenu::list::name}` with `{lores::...::list}`
- `{labels::default::economy::contracts::submenu::create::name}` with `{lores::...::create}`
- `{labels::default::economy::contracts::submenu::claim::name}` with `{lores::...::claim}`
- `{labels::default::economy::contracts::submenu::complete::name}` with `{lores::...::complete}`
- `{labels::default::economy::contracts::submenu::approve::name}` with `{lores::...::approve}`
- `{labels::default::economy::contracts::submenu::dispute::name}` with `{lores::...::dispute}`

#### Jury Sub-Menu:
- `{labels::default::economy::jury::submenu::title}` = "Jury"
- `{labels::default::economy::jury::submenu::list::name}` with `{lores::...::list}`
- `{labels::default::economy::jury::submenu::vote::name}` with `{lores::...::vote}`

#### Market Sub-Menu:
- `{labels::default::economy::market::submenu::title}` = "Market"
- `{labels::default::economy::market::submenu::sell::name}` with `{lores::...::sell}`
- `{labels::default::economy::market::submenu::cancel::name}` with `{lores::...::cancel}`
- `{labels::default::economy::market::submenu::buy::name}` with `{lores::...::buy}`
- `{labels::default::economy::market::submenu::browse::name}` with `{lores::...::browse}`

#### P2P Trade Sub-Menu:
- `{labels::default::economy::ptrade::submenu::title}` = "P2P Trading"
- `{labels::default::economy::ptrade::submenu::offer::name}` with `{lores::...::offer}`
- `{labels::default::economy::ptrade::submenu::itemswap::name}` with `{lores::...::itemswap}`
- `{labels::default::economy::ptrade::submenu::accept::name}` with `{lores::...::accept}`
- `{labels::default::economy::ptrade::submenu::deny::name}` with `{lores::...::deny}`

---

### 2. **ServerEconomyExecutables.sk** - Add Command and Click Handler

#### Add Command:
```
command /economy:
    aliases: /econ
    trigger:
        openEconomyMenu(player, {language::%uuid of player%})
```

#### Add Event Handler:
```
on inventory click:
    if event-inventory = (metadata tag "Economy" of player):
        cancel event
        handleEconomyMenuClick(player, index of event-slot)
    else if event-inventory = (metadata tag "EconomyContracts" of player):
        cancel event
        handleEconomyContractsMenuClick(player, index of event-slot)
    else if event-inventory = (metadata tag "EconomyJury" of player):
        cancel event
        handleEconomyJuryMenuClick(player, index of event-slot)
    else if event-inventory = (metadata tag "EconomyMarket" of player):
        cancel event
        handleEconomyMarketMenuClick(player, index of event-slot)
    else if event-inventory = (metadata tag "EconomyPTrade" of player):
        cancel event
        handleEconomyPTradeMenuClick(player, index of event-slot)
```

---

### 3. **ServerEconomy.sk** - Add GUI Functions (at end of file)

#### Main GUI Function:
- `openEconomyMenu(p: player, lang: text)` - Opens 3-row chest with 9 items:
  - Slot 0: Transfer (Gold Ingot) with input via anvil GUI
  - Slot 4: Swap (Emerald) with input via anvil GUI
  - Slot 8: Contracts (Enchanted Book) → Opens Contract Sub-Menu
  - Slot 9: Jury (Mace) → Opens Jury Sub-Menu
  - Slot 13: Market (Chest) → Opens Market Sub-Menu
  - Slot 17: P2P Trade (Shulker Box) → Opens P2P Trade Sub-Menu
  - Slot 18: Balance (Bundle) → Direct call to `showBalance(player, null)`
  - Slot 22: Economy Info (Diamond) → Direct call to `showEconomy(player)`
  - Slot 26: Supply (Barrel) → Direct call to `showSupply(player)`

#### Main Click Handler:
- `handleEconomyMenuClick(p: player, slotObj: integer)` - Routes clicks:
  - Slot 0 → Set `{status::%uuid of player%}` to "transfer" and open anvil GUI
  - Slot 4 → Set `{status::%uuid of player%}` to "swap" and open anvil GUI
  - Slot 8 → `openEconomyContractsMenu(player, language)`
  - Slot 9 → `openEconomyJuryMenu(player, language)`
  - Slot 13 → `openEconomyMarketMenu(player, language)`
  - Slot 17 → `openEconomyPTradeMenu(player, language)`
  - Slot 18 → `showBalance(player, null)` and close inventory
  - Slot 22 → `showEconomy(player)` and close inventory
  - Slot 26 → `showSupply(player)` and close inventory

#### Sub-Menu Functions:
- `openEconomyContractsMenu(p: player, lang: text)` - Opens 3-row chest with 6 items (slots 2, 6, 11, 15, 20, 24):
  - Slot 2: List Contracts
  - Slot 6: Create Contract
  - Slot 11: Claim Contract
  - Slot 15: Complete Contract
  - Slot 20: Approve Contract
  - Slot 24: Dispute Contract
  
- `handleEconomyContractsMenuClick(p: player, slotObj: integer)` - Routes to contract entry point with appropriate args:
  - Slot 2 → `contractEntryPoint(player, "list", null, null)`
  - Slot 6 → `contractEntryPoint(player, "create", null, null)`
  - Slot 11 → `contractEntryPoint(player, "claim", null, null)`
  - Slot 15 → `contractEntryPoint(player, "complete", null, null)`
  - Slot 20 → `contractEntryPoint(player, "approve", null, null)`
  - Slot 24 → `contractEntryPoint(player, "dispute", null, null)`

- `openEconomyJuryMenu(p: player, lang: text)` - Opens 3-row chest with 2 items (slots 11, 15):
  - Slot 11: List Disputes
  - Slot 15: Vote on Dispute
  
- `handleEconomyJuryMenuClick(p: player, slotObj: integer)` - Routes to jury entry point:
  - Slot 11 → `juryEntryPoint(player, "list", null, null)`
  - Slot 15 → `juryEntryPoint(player, "vote", null, null)`

- `openEconomyMarketMenu(p: player, lang: text)` - Opens 3-row chest with 4 items (slots 2, 6, 11, 15):
  - Slot 2: Sell Item
  - Slot 6: Cancel Listing
  - Slot 11: Buy Item
  - Slot 15: Browse Market
  
- `handleEconomyMarketMenuClick(p: player, slotObj: integer)` - Routes to market entry point:
  - Slot 2 → `marketEntryPoint(player, "sell", null)`
  - Slot 6 → `marketEntryPoint(player, "cancel", null)`
  - Slot 11 → `marketEntryPoint(player, "buy", null)`
  - Slot 15 → `marketEntryPoint(player, "browse", null)`

- `openEconomyPTradeMenu(p: player, lang: text)` - Opens 3-row chest with 4 items (slots 2, 6, 11, 15):
  - Slot 2: Make Offer
  - Slot 6: Item Swap
  - Slot 11: Accept Trade
  - Slot 15: Deny Trade
  
- `handleEconomyPTradeMenuClick(p: player, slotObj: integer)` - Routes to ptrade entry point:
  - Slot 2 → `ptradeEntryPoint(player, "offer", null, null)`
  - Slot 6 → `ptradeEntryPoint(player, "itemswap", null, null)`
  - Slot 11 → `ptradeEntryPoint(player, "accept", null, null)`
  - Slot 15 → `ptradeEntryPoint(player, "deny", null, null)`

---

## Layout Diagrams

Slot reference: Row 0 (Top): [0][1][2][3][4][5][6][7][8] | Row 1 (Middle): [9][10][11][12][13][14][15][16][17] | Row 2 (Bottom): [18][19][20][21][22][23][24][25][26]

### Main Economy Menu (9 items):
```
Row 0: [Transfer] [ - ] [ - ] [ - ] [Swap] [ - ] [ - ] [ - ] [Contracts]
       [0]        [1]  [2]  [3]  [4]   [5]  [6]  [7]  [8]

Row 1: [Jury] [ - ] [ - ] [ - ] [Market] [ - ] [ - ] [ - ] [P2P Trade]
       [9]    [10] [11] [12] [13]       [14] [15] [16] [17]

Row 2: [Balance] [ - ] [ - ] [ - ] [Info] [ - ] [ - ] [ - ] [Supply]
       [18]      [19] [20] [21] [22]     [23] [24] [25] [26]
```
Slots: 0, 4, 8, 9, 13, 17, 18, 22, 26

### Contract Sub-Menu (6 items):
```
Row 0: [ - ] [ - ] [List] [ - ] [ - ] [ - ] [Create] [ - ] [ - ]
       [0]  [1]  [2]    [3]  [4]   [5]  [6]       [7]  [8]

Row 1: [ - ] [ - ] [Claim] [ - ] [ - ] [ - ] [Complete] [ - ] [ - ]
       [9]  [10] [11]    [12] [13] [14] [15]        [16] [17]

Row 2: [ - ] [ - ] [Approve] [ - ] [ - ] [ - ] [Dispute] [ - ] [ - ]
       [18] [19] [20]      [21] [22] [23] [24]       [25] [26]
```
Slots: 2, 6, 11, 15, 20, 24

### Jury Sub-Menu (2 items):
```
Row 0: [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ]
       [0]  [1]  [2]  [3]  [4]   [5]  [6]  [7]  [8]

Row 1: [ - ] [ - ] [List] [ - ] [ - ] [ - ] [Vote] [ - ] [ - ]
       [9]  [10] [11]   [12] [13] [14] [15]  [16] [17]

Row 2: [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ]
       [18] [19] [20] [21] [22] [23] [24] [25] [26]
```
Slots: 11, 15

### Market Sub-Menu (4 items):
```
Row 0: [ - ] [ - ] [Sell] [ - ] [ - ] [ - ] [Cancel] [ - ] [ - ]
       [0]  [1]  [2]    [3]  [4]   [5]  [6]      [7]  [8]

Row 1: [ - ] [ - ] [Buy] [ - ] [ - ] [ - ] [Browse] [ - ] [ - ]
       [9]  [10] [11]   [12] [13] [14] [15]       [16] [17]

Row 2: [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ]
       [18] [19] [20] [21] [22] [23] [24] [25] [26]
```
Slots: 2, 6, 11, 15

### P2P Trade Sub-Menu (4 items):
```
Row 0: [ - ] [ - ] [Offer] [ - ] [ - ] [ - ] [ItemSwap] [ - ] [ - ]
       [0]  [1]  [2]     [3]  [4]   [5]  [6]        [7]  [8]

Row 1: [ - ] [ - ] [Accept] [ - ] [ - ] [ - ] [Deny] [ - ] [ - ]
       [9]  [10] [11]      [12] [13] [14] [15]      [16] [17]

Row 2: [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ] [ - ]
       [18] [19] [20] [21] [22] [23] [24] [25] [26]
```
Slots: 2, 6, 11, 15

---

## Implementation Checklist

- [x] Add all label and lore constants to `ServerEconomyConstants.sk` - Added `caliberateEconomyGUILabels()` function with all labels and lores
- [x] Add `/economy` command to `ServerEconomyExecutables.sk` - Added with aliases `/econ`
- [x] Add click handlers for all sub-menus to `ServerEconomyExecutables.sk` - Added unified `on inventory click` handler for all economy GUIs
- [x] Call `caliberateEconomyGUILabels()` on load in `ServerEconomyExecutables.sk` - Added to `on load` event
- [x] Implement `openEconomyMenu()` in `ServerEconomy.sk` - Main menu with 9 items
- [x] Implement `handleEconomyMenuClick()` in `ServerEconomy.sk` - Routes all main menu clicks
- [x] Implement `openEconomyContractsMenu()` in `ServerEconomy.sk` - 6 contract actions
- [x] Implement `handleEconomyContractsMenuClick()` in `ServerEconomy.sk` - Routes contract clicks
- [x] Implement `openEconomyJuryMenu()` in `ServerEconomy.sk` - 2 jury actions
- [x] Implement `handleEconomyJuryMenuClick()` in `ServerEconomy.sk` - Routes jury clicks
- [x] Implement `openEconomyMarketMenu()` in `ServerEconomy.sk` - 4 market actions
- [x] Implement `handleEconomyMarketMenuClick()` in `ServerEconomy.sk` - Routes market clicks
- [x] Implement `openEconomyPTradeMenu()` in `ServerEconomy.sk` - 4 P2P trade actions
- [x] Implement `handleEconomyPTradeMenuClick()` in `ServerEconomy.sk` - Routes P2P trade clicks
- [ ] Test all GUI menus and click handlers in-game
- [ ] Verify language support across all menus
- [ ] Verify anvil GUI input handling for transfer and swap actions

