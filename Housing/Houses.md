**HousingV2 – House Flag Structure (DB NPC)**

---

Each house in HousingV2 is stored as:
this.house_<ID>.<property>

**Example:**

*house_10.<property>*

Below is a breakdown of each flag and how it interacts with the system.
Documentation is based directly on the active HousingV2 system logic

*house_10.entrance.level = era_sewerph-house2-1-remake.nw*

---

**What it does:**
Defines the level players are warped to when entering this house.
Used by enterHouse() which calls:

pl.setlevel2(
  this.("house_" @ house_id).entrance.level,
  this.("house_" @ house_id).entrance.x,
  this.("house_" @ house_id).entrance.y
);

---

**Technical Notes:**
Must be a valid level name.
If the level does not exist, tax recalculation will error and notify NC.
Used by door update logic (updateDoor()).

house_10.entrance.x = 39.5
house_10.entrance.y = 35

---

**What they do:**
Define the exact warp coordinates inside the entrance level.
Used together with .entrance.level inside enterHouse().

***Important:***

Decimal values are valid (GS2 supports float positioning).
Incorrect coordinates can spawn players inside walls.

*house_10.levels = era_sewerph-house2-1-remake.nw, era_sewerph-house2-4-remake.nw, era_sewerph-house3-1-remake.nw, era_sewerph-house3-1-spar.nw, era_sewerph-house4-1-remake.nw*

---

**What it does:**
Defines all levels that belong to this house.
Used by:

***1) isHouse(lvl)***

Checks if a level belongs to a house.

***2) getHouseID(lvl)***

Returns which house ID owns that level.

***3️) updateTax(house_id)***

Tax is calculated by looping every tile of every level in this list.

***4️) restoreFurniture(house_id)***

Loops through all levels to:
Remove placed furniture
Return furniture items to owner

***Important:***

If a level listed here does not exist, updateTax() logs an NC error.
Tax increases based on walkable tile count inside these levels.

*house_10.owner = (npc-server)*

---

**What it does:**

Defines the account that owns the house.
(npc-server) means the house is unowned and owned by the server.

**Used by:**
-hasControl()
-canEnter()
-giveHouse()
-canBuyHouse()

***Important Behavior:***

If owner is (npc-server):
Anyone can enter.
House is considered available for sale.

---

**When ownership changes:**

-Furniture is restored
-Access/control lists are wiped
-Safe balance is returned to previous owner

house_10.price = -1

**What it does:**

Determines sale state of the house.
Meaning of values:
Value	Meaning
-1	Not for sale
>= 0	House is for sale at that price

**Used by:**

-getPrice()
-hasAccess() → If price ≠ -1, house is publicly enterable
-setPrice() → Updates DB + refreshes control

***Important:***

If price is NOT -1:
House becomes accessible to anyone (even if locked)
Often used when placing house on market

house_10.tax = 1559

**What it does:**

Stores weekly tax cost for the house.

**Used by:**

-calculateTax()
-onPayTaxes()

**Tax System Behavior:**

Taxes collected every 604800 seconds (7 days)
If player cannot afford tax:

giveHouse(house_id, "(npc-server)")

House is repossessed
Player receives message

**How Tax Is Calculated:**
If tax <= 0:

// Loops every tile in every level
// +0.5 per non-wall tile
// Total is int() rounded

So:
Bigger houses = higher tax
More walkable space = higher tax

---

**How These Flags Work Together**
Flag	Affects entrance.level/x/y	Warp location
levels	Tax, ownership detection, furniture restoration
owner	Permissions, access, repossession
price	Sale state + public access
tax	Weekly payment enforcement

**Example Flow (Ownership Transfer)**
If a player loses house due to unpaid tax:
-onPayTaxes() triggers
Balance checked

**If insufficient:**
giveHouse(house_id, "(npc-server)")

-Furniture restored
-Access cleared
-Price reset to -1
-House closed
-Owner set to (npc-server)

---

***SOP Notes for Housing Admins***

-Always verify .levels matches actual house levels.
-Never manually edit .tax unless recalculating.
-Use :setprice instead of direct flag edit when possible.
-(npc-server) means server-controlled property.
-Tax is automatically recalculated if missing or <= 0.
