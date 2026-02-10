# Housing – Admin Commands

This document lists the administrative commands related to housing management, including usage requirements, arguments, examples, and known limitations.

---

## Basic Housing Commands

> These commands operate on the **current house** and require you to be standing inside a house-controlled level  
> (`player.level.house_control != null`).

### `:houseid`
Displays the current house’s ID in chat.

**Requirements**
- Must be inside a house

---

### `:addlevel`
Adds the current level name to the house’s level list (if not already present).

**Requirements**
- Must be inside a house

---

### `:updatetax`
Recalculates the house tax and displays the result in chat.

**Output**
Updated Tax: $X


**Requirements**
- Must be inside a house

---

### `:setentrance`
Sets the house entrance to your current:
- Level
- X coordinate
- Y coordinate

**Requirements**
- Must be inside a house

---

### `:takehouse`
Clears the current house owner (sets owner to `null`), if one exists.

**Requirements**
- Must be inside a house

---

## Commands with Arguments

### `:setprice <amount>`
Sets the current house’s sale price.

**Arguments**
- `<amount>` — Parsed as an integer

**Example**
:setprice 250000


**Notes**
- Non-numeric input is converted using `int()`
- Invalid input (e.g. `:setprice abc`) will likely result in a price of `0`

**Requirements**
- Must be inside a house

---

### `:givehouse <account>`
Transfers ownership of the current house to the specified account.

**Arguments**
- `<account>` — Target account name

**Examples**
:givehouse SomePlayer


**Special Case**
:givehouse (npc-server)

- Sets the house owner to `null`

**Requirements**
- Must be inside a house

---

### `:fh <ownerPrefix>`
**Find House** — Searches all owned houses where the owner name **starts with** the provided prefix.

**Arguments**
- `<ownerPrefix>` — Prefix match only

**Example**
:fh prin


**Output Format**
ID=<id> - <owner>


**Notes**
- Uses prefix matching (`starts()`), not substring matching

---

### `:wh <houseId>`
**Warp House** — Warps you to the entrance of the specified house ID.

**Arguments**
- `<houseId>` — Target house ID

**Example**
:wh 12345


**Failure Case**
- Will display `Could not find the house!` if the house does not have an entrance set

---

## Notes & Gotchas

- All **current house** commands require being inside a level with `house_control`
- `:fh` matches **prefix only**, not partial strings
- `:wh` requires the house to have an entrance set
- `:setprice` silently converts invalid input to `0`
- GUI buttons and `loadHousingInfo` client-side display are commented out
  - No chat command exists for those features in this implementation

---

## NPC Housing Commands

The following NPC commands are also available:

/npc housereport
/npc houseinfo <acc>
/npc checkhouses
/npc accountsearch <acc>
