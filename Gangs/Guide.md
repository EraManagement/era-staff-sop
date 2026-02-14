Role
Access to all things gang related: shops, levels in bases, levels in pk maps, gang event levels, some databases, weapon, and class scripts.
-EventSystem for example (huge class involving all scripts for events logic), there is a command w/ awarding players with individual gang currency (:gcwinner), that needs updating every season to get right token (:awardguild “gang name”# is for the whole gang)
-Gangs/Weekly Awards, updated to award coins for proper season on weekly reset
-Staff/AwardGang, updating id to give proper season reward

In a level only 1 person at a time can view a script and edit it, on RC multiple ppl can but just remember coordinate w/ others working on it as “apply” saves YOUR current changes and overridfes other persons

dragon is databases - logic for big systems
sword is weapon - all weapons and events
papers is classes - function behind basic things

/npc gangs help in Remote Control to get the list of commands (use this to delete, add, rename gangs AND MORE)



To get item info (icon files, for example), use /npc iteminfo *item id) in RC

Staff blocks
Say :so and grab to make staff only
:block when grabbing block to create a kicker
:i <image name> to make image

Gang Structure

Nickname colors (when on gangtag) are part of a class that deals with all nicknames


Gang Rewards

Every season will have special crates for 10 coins and a previous season arena crate available for arena coins

For s2 Crime has handled creating the new gang guns and initial pricing


NE
Need specific :ne rights for specific levels to be able to edit
:ne is for editing npcs, some scripts are on the NPC or much larger in RC databases that make the script work like shops. 
In ne most scripts are editable on the NPC so be careful with quantities (check prices and quantity per purchase)
The left side of the ne menu is a whole bunch of scripts at boilerplate, if not there will need to look for it in other levels (but most likely theyre there)
Right click in a level in :ne to make an npc (top option is an npc to put a script in, bottom has a “char model”)
Can paste script in from the :ne menu
To replace item ids, use :fi “item” to get the ID




For double gang exp:
P menu > Admin > Force double xp (check on)


Automated broken, supposedly


Arena

Bases are tied to a class (Database NPC = Control_GangArena) that is tied to arena logic
Database NPCs are “The dragon head”, WeaponNPCs are the “sword”, and Class SCripts is the stack of papers (icons on RC)
Lines 514 and 1176 (as of 9/2/24) for adding new arenas


Arena logic is tied to everything
In arena script it defines what gets awarded, how much gets awarded, and what determines that you will get a reward
To check how many coins people have (or in general, how many items), on RC: !scanaccs <itemID>. Then say “list”. Use :fi for fining item id
:getallarenas in RC to get a list of active arenas
Use :changearena “name” to change the active arena


Gang Shop

Stocking, you type +# or -# and right click the shop to add remove


Gang Seasons

When a new season starts, best practice is to reset all player gang points. (/npc resetpoints)


Gang events
After gang events, host an arena (30-60 min), to reset weekly points it’s a simple rc command (/reset topweekly, to be confirmed)


Embassy warpto era_ow-inside-gangembassy-main.nw

Bases to add 9/3/24:
BH
era_blackholstbase0-0.nw
era_blackholstbase0-1.nw
era_blackholstbase0-2.nw
era_blackholstbase0-3.nw
(all black area?) era_blackholstbase1-0.nw
era_blackholstbase1-1.nw
era_blackholstbase1-2.nw
era_blackholstbase1-3.nw
(all black area?) era_blackholstbase2-0.nw
era_blackholstbase2-1.nw
era_blackholstbase2-2.nw
era_blackholstbase2-3.nw
(all black area) era_blackholstbase3-0.nw
era_blackholstbase3-1.nw
era_blackholstbase3-2.nw
era_blackholstbase3-3.nw
Obsidian
Era_gangbase-obsidian_a1.nw
Era_gangbase-obsidian_a2.nw
era_gangbase-obsidian_a3.nw
Era_gangbase-obsidian_b1.nw
Era_gangbase-obsidian_b2.nw
Era_gangbase-obsidian_b3.nw
Era_gangbase-obsidian_c1.nw
Era_gangbase-obsidian_c2.nw
Era_gangbase-obsidian_c3.nw
Era Mafia V2
Era_mafia_a1.nw
Era_mafia_a2.nw
Era_mafia_b1.nw
era_mafia_b2.nw
Era Mafia
era_mafiapk-heal.nw
era_mafiapk-main.nw
era_mafiapk-west.nw
Rec center (needs some face lifting?)
Era_rec-center_a1.nw
Era_rec-center_a2.nw
Era_rec-center_b1.nw
Era_rec-center_b2.nw
era_traphouse-pkv2.nw



Under consideration

Ghostface base? Current sim raid…
era_ghostfacebase-elevator.nw and 0-0, 0-1, etc
BB with elevator
Blazian gmap (needs a little TLC but this seems like a sicck map)
era_blazianbase0-0.nw
era_blazianbase0-1.nw
era_blazianbase0-2.nw
era_blazianbase0-3.nw
era_blazianbase1-0.nw
era_blazianbase1-1.nw
era_blazianbase1-2.nw
era_blazianbase1-3.nw
era_blazianbase2-0.nw
era_blazianbase2-1.nw
era_blazianbase2-2.nw
era_blazianbase2-3.nw
era_blazianbase3-0.nw
era_blazianbase3-1.nw
era_blazianbase3-2.nw
era_blazianbase3-3.nw
Snow resort
era_snow-resort1_1.nw
era_blazainbase_00-00.nw
era_blazegang-armory.nw
era_bb-meeting.nw
era_bk-elevator.nw
era_blackholst-1.nw
era_blackholst1-normal.nw
era_blackholst-ele.nw
Era Mafia
Era Mafia 2
Obsidian?
Osiris
Trap House
Buffalino Family
Beach
Contras (this one is huge)
era_base-contrasmain_00-00.nw



Sim Raid projects

1. Era_base-cabalmain.gmap
2. 

