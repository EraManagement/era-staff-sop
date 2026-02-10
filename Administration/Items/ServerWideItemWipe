**Resetting Seasonal Event Items (Yearly Wipe)**
================================================

Purpose
This SOP explains how to safely reset seasonal event items/currencies (ex: Christmas Coins, Valentines Coins) so players start fresh for a new yearly event.

This method ensures:
-Items are wiped once per year per player
-No repeated wipes on every login
-Clear messaging to players

**Scope**

-Applies to yearly seasonal events only
-Uses Player class logic
-Server-side, persistent per account

**Step 1  Open the Player Class**

1.1: Open the Player class script.
1.2: Locate or create a section dedicated to seasonal cleanup (usually near login/init logic).
1.3: Seasonal wipes must live in the Player class so they run automatically on login and apply consistently to all players. 


**Step 2  Identify Previous Year Items**

2.1: Locate the previous years event items and currency IDs.

Example (Valentines Day items):

//Valentines Day
if (!this.clientr.removedvdayitems25) {
  this.clientr.itemc820 = "";
  this.clientr.itemc10203003 = "";
  this.clientr.itemc10203004 = "";
  this.clientr.itemc10203005 = "";
  this.clientr.itemc10203006 = "";
  this.clientr.itemc10203007 = "";
  this.clientr.itemc924757 = "";
  this.clientr.removedvdayitems25 = true;
  this.sendPM("Your vday25 Misc Items have been removed. -Management");
}


Notes:

itemc<ID> corresponds to a specific item or currency.
Setting it to "" removes it from the player inventory.

**Step 3  Update Item IDs**

3.1: Replace all item IDs with the ones you want to wipe.

Double-check:
Event currency
Event misc items
Limited-time consumables

  Do not reuse old item IDs from a previous event year.

**Step 4  Update the Wipe Flag (CRITICAL)**

The flag controls one-time execution per year.

Rule:
Players who already have the flag set will NOT be wiped again.

Example logic:

Year: 2027
You want to wipe 2026 Valentines items
You must change the flag name
if (!this.clientr.removedvdayitems26) {
  ...
  this.clientr.removedvdayitems26 = true;
}

Always increment the year in the flag
Never reuse an old flag name

**Step 5  Update Player Message (Optional but Recommended)**

You may change the message to inform players:

this.sendPM(
  "Your 2026 Valentines event items have been reset for the new season.",
  "-Management"
);


Best practices:
-Be clear
-Reference the event/year
-Avoid technical wording

**Step 6  Apply the Wipe**

If the event is opening now

Run on Remote Control:

/npc reconnectall


This will:
-Force all online players to reinitialize
-Immediately apply the wipe

If the event is opening later:

Do nothing
The wipe will automatically occur on each players next login

-Safe to leave the script in place
-No performance impact

**Safety Checklist (Before Pushing Live)**

1) Correct item IDs
2) Correct year-specific flag
3) Message reviewed
4) Tested on dev account

 **/npc reconnectall only if needed**
