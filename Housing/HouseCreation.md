***How To Create a New House (Official Method)***

This guide explains the correct and complete method for creating a new house using the HousingV2 system.
---

**STEP 1 — Create or Enter the House Level**

*Either:*
Create a brand new .nw level
Or open the level that will become the house

*Make sure:*
-The level file name is correct
-It is uploaded and accessible
-You are standing inside it before continuing

---

**STEP 2 — Find an Available House ID**
Open the HousingV2 DB NPC.

*Scroll through existing:*

house_<ID>

*Find an unused ID.*

***!Never reuse an existing house ID.!***

Example:
If the last house is house_1110101, your new one can be:

*1110102*

You will use this ID in both NPCs placed in the level.

---

***STEP 3 — Add the House Panel NPC (Owner Management Panel)***
Inside the house level, create an NPC and add this script:

// Created by Smogy27
//#CLIENTSIDE
function onCreated() {
  this.house_id = 1110102;
  this.setShape(1, 32, 32);
  this.join("housingv2_panel");
}

***What This Does:***
-Sets the house_id
-Defines the clickable shape (32x32)
-Joins the housingv2_panel class

*Creates the command panel the owner will use to:*

-Manage access
-Manage control
-Manage price
-Manage house settings

This panel is required for house management.

---

***STEP 4 — Add the House Control NPC (Owner / Access Display)***

*Inside the same house level, create another NPC and add:*

// Created by Smogy27
function onCreated() {
 this.house_id = 1110102;
 this.notify_tax = true;
 this.join("housingv2_control");
 setimg("a");
}

***What This Does:***
-Links this NPC to the house using house_id
-Enables tax notifications with:
-this.notify_tax = true;
-Joins the housingv2_control class

*Displays:*
Current owner
Who has access
Who has control

***!This NPC works in conjunction with the panel.!***

***!Both are required.!***

---

***STEP 5 — Save the Level***

*After placing both NPCs:*

-Update the level to save the NPCs.
-Make sure no script errors appear.
-Confirm both NPCs are present in the level.

---

***STEP 6 — Set the House Entrance***

*Now:*

Stand at the entrance tile where players should spawn.
Type the command:

:setentrance

***What This Does:***

*This command automatically:*

Registers the level to the house ID

*Sets:*

-house_<ID>.entrance.level
-house_<ID>.entrance.x
-house_<ID>.entrance.y

*Links the level inside:*

house_<ID>.levels

*Calculates and sets:*

house_<ID>.tax

*Ensures flags are properly initialized*

***!You do NOT need to manually edit flags if using :setentrance.!***

***What Gets Automatically Created***

*After using :setentrance, the following flags will exist:*

house_1110102.entrance.level
house_1110102.entrance.x
house_1110102.entrance.y

house_1110102.levels
house_1110102.owner
house_1110102.price
house_1110102.tax

*Default behavior:*

owner → (npc-server)
price → -1
tax → Calculated automatically

---

***Final Result***

Once entrance is set:

✔ House is fully registered
✔ Tax is calculated
✔ Level is linked
✔ Panel works
✔ Control display works
✔ Ownership system active

***Voilà — you now have a brand new house!***

***!Important Notes!***

*-The house_id in BOTH NPCs must match the unused ID.*
*-If IDs do not match, the system will not work.*
*-Always use :setentrance after placing the NPCs.*
*-Do not manually edit DB flags unless necessary.*
*-Ensure no duplicate IDs exist.*
