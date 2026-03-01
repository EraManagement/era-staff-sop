**HousingV2 Furniture SOP**

***Purpose***
-This SOP explains how to properly:
-Add new furniture to HousingV2_Furniture
-Assign correct furniture IDs
-Set up class references
-Avoid breaking generated flags
-Backup and restore player-owned furniture

---

***Furniture Script Structure***

*Inside HousingV2_Furniture, furniture must follow this exact format:*

**//Furniture Token
this.229 = {"Alifz's Futuristic Chair", "futuristicchair-frontv2.png", "housingv2_alifz-chair-luxury", 25000, 10, true, "Fancy!", 229};**

*Structure Breakdown*
this.ID = {"name", "icon-image.png", "class name", price, maxquantity, sellable, desc, ID};

*Field Explanation*
//       {"name", "icon-image.png", "class name", price, maxquantity, sellable, desc, [id]}
**Position    	        Purpose**
"name"	                Name displayed in-game
"icon-image.png"	      Image file uploaded in file browser
"class name"	          Class reference OR image reference (img:imagename.png)
price	                  Price of the furniture
maxquantity	            Maximum quantity a player can own
sellable	              true or false (whether the furniture can be sold)
desc	                  Description shown in shop
[id]	                  Furniture ID (must match this.ID)

***The first ID (this.ID) and the last [id] value must match exactly.***

---

***Before Creating a New Furniture Piece***

Before adding a new furniture entry:

-Upload the Image First
-Upload the image into the file browser.
-Confirm the filename is correct.
-Confirm transparency and formatting are correct.
-You must have the image uploaded before referencing it inside the script.

---

***Finding an Available Furniture ID***

Before creating a new furniture piece:
-Scroll inside HousingV2_Furniture
-Locate the highest existing ID
-Choose the next available number
-Confirm the ID is not already used

***!Never reuse an existing ID.!***

***Creating the Furniture Class***

*If the furniture requires behavior (placement logic, interaction, shape, scripting behavior, etc.):*
Create a new class using this pattern:

**housingv2_addnamehere**

*Example:*

housingv2_alifz-chair-luxury

Then reference that class name in the third parameter of the furniture script line.

**If the Furniture is Only an Image**

If the furniture is simply a static image and does NOT require a custom class:

Instead of using a housingv2_ class, use:

img:imagename.png

Example:

this.300 = {"Simple Rug", "simplerug.png", "img:simplerug.png", 5000, 5, true, "Basic rug", 300};

This tells the system:
No custom class is required
Use the image directly

---

***Important — DO NOT MANUALLY EDIT FLAGS***

Once you add a new furniture line:
-The flags will automatically be generated.

***!Do NOT manually edit flags.!***

*If you manually edit flags:*
-They will not update the script correctly
-The furniture can break
-Ownership data can become corrupted
-The system will not properly sync

***Always let HousingV2_Furniture handle flag generation automatically.***

---

***Player Furniture Ownership Data***

If you scroll down inside of HousingV2_Furniture, you will see all furniture owned by players.

It will look like this:

Smogy27="134,1","133,1","135,1","139,1","140,1","143,1","148,1","13,1","1862,1","231,1","230,1","92025,1","1,1","2011,1","2006,1","2003,1","2005,1","2002,1","2013,1","2001,1","1861,1","2007,1","2014,1","2004,1","1863,1","2017,1","2016,1","2009,8","2008,1","2012,9","12,1","1989,2","1988,1","1982,1","1983,1","7,1","1981,1","130,1","129,1","141,1","142,1"
Format Explanation

Each entry follows this format:

"FurnitureID,Amount"

Example:

"2009,8"

Means:

Furniture ID: 2009

Player owns: 8 copies

---

***Backing Up Player Furniture Data***

*It is strongly recommended that you:*
-Download this section
-Save it locally
-Keep your own backup copy

Use this backup if:
-A script issue wipes furniture
-A player loses furniture
-Data corruption occurs

---

***Restoring Player Furniture***

If a player loses furniture:
-Locate their name in the furniture ownership list.
-Edit the values manually.
-Add back the correct "ID,Amount" pairs.
-Save the script.
-Update flags if required.

**Once saved:**

*The player will have their furniture added back.*

---

***Final Checklist Before Saving***

Before updating HousingV2_Furniture, verify:

 -Image uploaded
 -ID not already used
 -First ID matches last ID
 -Correct class name OR img: reference used
 -No manual flag edits
 -Backup saved (recommended)
