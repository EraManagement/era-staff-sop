
Server Knowledge
============================
- say '/opencomments folders' in RC for a reference of the new folder structure permissions
--- we've migrated thousands upon thousands of files from old folders into new, more relevant folders
--- try to maintain an organised upload process with your server files, otherwise folders can become too large to open from RC3 application
------ if you cannot open a folder from your external RC, try the f6 (ingame) RC, as this should be able to load the folder(s) just fine


- all items are stored in the flags of DB_Items
--- item flag data is compiled into this database via:
1) NPC: DB_Items script
2) CLASS: items_hats
3) CLASS: items_guns
--- all item flag data will compile into this database's flags on-save (so when you save a class referenced above, the DB_Items dbNPC will re-compile and echo in RC on completion
--- you can only open this DB's flags via client RC as it's too large for external RC at this point
--- because item id's are consumed in upwards of 5-6 different places, you should always scan an id before trying to add a new item. so if you decide you'd like to use id 123456 because you can't find it used anywhere, first do '/npc iteminfo 123456' in RC to confirm if this is already taken as an item ID


- RC commands are split among two dbNPC's:
1) dbNPC: RC-Bot
2) dbNPC: Remote-NPC
--- (1) uses commands starting with !... say '!help' in RC
--- (2) uses commands starting with /npc... say '/npc help' in RC


- use '/scriptscan scripts <keyword>' to get around the many systems found on this server
--- a good strategy to take is when you have an issue with something (like a GUI), find words/messages/phrases used in the system or GUI (such as the GUI's window name/text). Then search for this most-probably-unique keyword using '/scriptscan scripts <keyword>' to find out which scripts reference that keyword and need investigating


- most hard-coded accounts from the past left lingering in code has either been transitioned to clientr.staff flag checks, or switched to my account name. you can find a lot of hardcode cases by simply scanning for my account name alone: /scriptscan scripts "Arch_Angel"

- 2 staff tools are primarily used here, although there are more to be found around the server
1) wNPC: -Tool
2) wNPC: Moon/Tool
--- these tools have been migrated to an organised log folder, where each staff has their own folder for all of their tool activity. Find them in the folders: logs/staff/accountName/*
--- blocks are controlled in the CLASS: block, where you can also add custom blocks for your staff team


- you can use :tpk (and the logic it uses in it's executed function) to quickly and easily flip players between pk and non-pk regardless of which safe zones they may be in


- old mall systems have had a lot of issues in duplications/glitches so its been disabled. this is mainly due to it conflicting with other systems having their own validations, guis and concepts, such as the Lend System
--- would not release or touch these old malls until you ensure it lines up perfectly with other systems like Lend/Rent/Temp Items etc
--- this has been replaced by a Market that uses on Item Drop logic, also used for all items in the game via the items CLASS (making it harder for random issues to pop up because we're running the same logic utilised in item drops (ie, you cannot drop lended or temporary items)
1) dbNPC: DB_Market
2) CLASS: market
3) CLASS: item

- for big databases we use SQL Lite tables. There is a SQL browser (accessible by the ` or ~ key) to help you navigate and update these tables directly
1) wNPC: -Admin/Explorer
--- common tables used are for gangs/gangpoints, marketplace, cars, alt/ip logs, spar tickets and achievements

- all login activity is now logged to associate alt accounts back to players (similar to how the globals handle this stuff). You can find the SQL table player_alts to dive into the row-by-row data, however there are commands on top of this table that make finding alts especially easy.
--- use the command '!alts <accountname>' in RC to pull a list of alts from an account name
--- you can also use !scanip and !scanips to get a list of IPs or accounts related to a specific IP, however this is less useful with the above being available
1) dbNPC: RC-Bot

- a lot of files have been migrated and old folders/data removed completely during my work here. try to keep folders organised to prevent folders becoming so packed full of files that external RC3 can no longer open them
--- most all folders fall under the levels/ root folder, levels actually being stored in levels/levels/* onwards
--- images and animations are mostly migrated into their categorized folders but try to prevent using anything outside of the levels/images/ folder for images


- you can use community names in almost any of the account/staff sections in server ops when adding staff to the various permissions
--- I would recommend to always use communitynames to keep things as clear as possible, but test first to make sure the permissions work as expected


- there is a common loot chest class that you can use to plug in any type of loot pools and costs to open the chest as needed
--- there are notes on how to use this chest in detail within the script itself
1) CLASS: npc_chest
--- additionally, there are two chests setup for quests to only allow opening after boss fights, taking into account quest timestamps/cooldowns, rewarding money after completion etc...
1) CLASS: quest_chest
2) CLASS: quest_chest-money
--- all quest chests are logged in logs/quest_chestlog*


- there are quite a few classes for things like npc dialogues, events, floating text/images and more
--- use these classes to your advantage, as they are all configurable in their level npc's so you can set up and use any of the many functions to improve the general experience/vibe around the server
1) CLASS: npc_events
2) CLASS: npc_fadeimg
3) CLASS: npc_floating-icon
4) CLASS: npc_moveable-object
5) CLASS: npc_styler
6) CLASS: npc_text
--- (1) can be used for many things, but primarily for dialogue when interacting with character NPCs around the map. use this to help explain things in shops, quests, tutorials, events and more
--- (2) can be used for those roofs on buildings that you want to fade away when a player walks under them. will adjust to any size image as needed by simply joining the script to your npc/image in your level
--- (3) can be used for floating icons above npc's, useful for showing which keys to press when nearby, or items required if its a crafting table. comes with various settings to fade the image out entirely/partially, also to set how quickly to bounce the image etc...
--- (4) a clientside script for quest or puzzle levels, allowing players to move any npc object that blocks them (or that they can grab/pull). movement is cleaned up and smooth and can be configured per level npc to change push/pull speed. wall detection could use a little optimisation but its alright as it is
--- (5) an npc character that lets you click them to load random heads/bodies straight from the server into a styler gui. place this in a level to let players browse and easily set new outfits on their characters (especially helpful for new players who don't know the setbody/head commands) (this was already used 27k times in <6 months, its very handy for players)
--- (6) for all things floating text related. this will draw your text characters as individual images, allowing them to move freely and independantly from one another. also allows you to place text at any 360* angle as desired, as well as flip text backwards. floating can be handled to bounce the entire text line at once or bounce each letter individually in a wave pattern
- more useful scripts like this can be found as a CLASS starting with npc_, all with decent documentation


- setup a download folder for your RC to increase how quickly you can edit files and re-upload them
--- find the Options button on RC and ensure a Downloads folder is in place
--- double-clicking items from the filebrowser in RC will download/open them on your computer
--- hitting Ctrl+s on that same file that has been opened from RC will automatically re-upload the file back on to the server, which is very useful for quick image/level/textfile edits being made


- a crafting script has been developed to make adding new elements/items to craft much easier and (mostly) painless
1) CLASS: crafting
--- you should only need to create a crafting table image and animation (when operating the table) and the script can do the rest
--- plug in your gani, images, required items and output items to be crafted all within the level npc
--- for every item that gets crafted, a unique log file will also be generated. this makes it very easy to scroll through logs/crafting/* to look at the kind of items being crafted to ensure staff isn't abusing level npc's by adjusting item reqts/outputs to their advantage

- you can load all comment files ever stored on era in case you're looking for old/lost notes or comments
1) wNPC: -angel/loadcomments
--- simply add yourself to the above weapon and run it to receive a PM contiaining a list of all comment files detected on the server


- generating mini map images can be done by adding the below weapon to your player:
1) wNPC: -angel/mapgen
--- add yourself this weapon and say the command ':gen' to generate a map. you can use ':gen #' to increase the map file size/resolution that gets generated in the end
--- maps are generated on a (mostly) 1:1 ratio with 1 block == 1 pixel. so if you have a gmap of 10 levels, you can expect an output file thats 640x640 pixels. If you wanted to scale this up to be 2.5x larger, you would say ':gen 2.5' on your player while on the gmap you want to generate a new file for
--- all maps generated are output to your local graal folder: Graal/scriptfiles/era/
--- your ingame map will be updated after the :gen is complete, but this is only local and specific to you (others will not see it)
--- be sure to re-save map images as 8-bit before uploading to the server. this helps vastly decrease the size of the image, but also helps get rid of a lot of the repeated noise added to the map from being condensed so much


- you can evaluate offline players via script
1) wNPC: -angel/tplayer
--- run this weapon to check a players attributes, whether they are on or offline


- staff levels are controlled via server ops and give your staff various bases of permissions to work with (see staff_level_x in ops)
1) level 1: very basic, added by default if not placed in a staff_level line in server ops
2) level 2: standard level for developer staff and soft admins like ET/Gang/House etc. comes with normal staff tools like stick, block, unstick, mouse warp...everything a dev needs to get by
3) level 3: not a huge jump up in terms of smaller tools, however, be considerate that level 3 now allows for the spawning of items via ':ai <itemid>' command. only give out to admins responsible for more than just a single area of development
4) level 4: highest level of staff, only give to manager and co/admin. keep as limited as possible, as most everything involving staff checks has a lvl 4 exception in it, which opens doors to most every command or tool on the server to make testing as easy as possible
--- you can add exceptions for certain players to remove any excess tools they should not have while in a given staff level. do so by finding and adding them to the 'staff_cant* ' lines in server ops accordingly


- most of the logic for players taking damage, dying and respawning can be found in CLASS living
--- you'll also find a wNPC named -HospitalSpawn which handles some player respawns


- the radio still works on era but you'll need to find URLs that host/stream music. some players enjoy taking ownership of the radio station, who then pay for a hosted service to stream their music library non-stop.
1) wNPC - Radio
--- you should only need to edit the URL used for streaming, everything else should work as expected


- you can right-click cars as a level 3+ staff to tow/remove/transfer them quickly and easily without the need for a Tow tool/weapon


- all logic surrounding job experience/leveling come from a player class that uses common functions to handle XP distribution, leveling up, scaling etc...
1) player_jobprogression
--- use this class' functions to make implementing XP for new jobs painless. you should only need to think of the xp scale algorithm you'd like to use and set it up within the class for your new job


- banning an IP via /openaccess command in RC doesn't seem to work anymore. because of this, certain IP's are banned via a manual disconnect script put in place in Control-NPC
1) dbNPC: Control-NPC
--- find the function onPlayerLogin to check, add and remove IPs listed here for disconnect on login
--- always add comments above any new IPs added to give context on who the ban is for (and for how long)


- all npc shops related to selling job materials and items have been migrated into a single system/gui
1) wNPC: Dan/MutliShop
2) dbNPC: DB_MultiShop
--- you can control all prices for all shops in the dbNPC listed above
--- for any bonuses applied to items and such (like csl for trash picking) can be picked up in the wNPC script, where you'll see some existing logic applied for other jobs (such as trashpicking)


- before you perma-ban an online player, first '/openaccess <account>' in RC. when the ban window opens, you should first ban their PC-ID which can be found in a tab within the new window. this tab only pops up when the player is actively online, so ban this first and then ban the account to enact a PC-wide ban for a person


- say :h and grab a block on the ground to get a list of the various commands you can use with blocks


- the entire staff team now has their tools logged in their own designated folders, making it easy to monitor those with admin capabilities
--- check logs/staff/*/* for the logs in question, providing individual level access for moon tool/staff tool/warping/summoning/blocks/quest abuse/npc editor abuse and more


- after you reset a player, don't forget to also reset their bank account as this is not automatically done by resetting them
--- in RC type '/npc bankcheck <acct>' to check an account's balance
--- in RC type '/npc bankchange <acct>' to change an account's balance
--- all account names must be the real account name (no community names) and proper capitalisation

- you can tradelock people who are not behaving and continuing to violate rules around USD, CST, scams etc... this is a good alternative to banning players so quickly, since the active PC playerbase is quite low
--- to lock someone, add the following flag to their player: clientr.tradelocked=1
--- trade locking someone will lock them out from bank xfers, picking up items not owned by the server, trades, lends, marketplace and more small areas of the game...note: players can still pick up dropped money from the ground

- if you can't seem to find someones car and have access to the sql browser, you can open it (with the ` key) and open the table player_cars
--- in this table, search for their account name to get a list of their cars
--- when found, right click the car row and click modify row -> and change the last field of TOWED from false to true...this will put their car at the tow yard for pickup

- /opencomments unhats
--- these comments contain a list of hat images I've compiled across the server
--- the list hasn't been updated since I started using hats from this list, so always scriptscan before adding new hats
------ you can scan for an existing hat being used by typing '/scriptscan scripts <hat-img-name>' in RC
------ if no results are returned, it's (normally) safe to use add hat as a new item id


- /countnoclassnpcs
--- scan the server for local npc's that are not joined to a class (rendering them essentially useless)
--- you should get a message returned, such as: Found 803 dbnpcs/putnpcs which have not joined a class


- /clearnoclassnpcs
--- used in parallel with /countnoclassnpcs
--- use this to delete useless local npcs lingering on the server


- to properly survey a person's logs, find their personal log files in logs/pl/first_letter_of_acc/acc_name*.txt
--- each player will have useful personal logs such as:
(1) a bank atm log (withdraw, deposit, transfers)
(2) a trade log (all trade actions)
(3) item log (drops, pickups, destroyed items)
--- scan these logs to gather most of the information you need
--- all other logs should be found in specific log files pertaining to their area (ie crafting, marketplace, houses...)

- to add new guns to the scrap list (to be turned into components), find a list of scrappable weapons in the dbNPC: DB_Crafting
--- these define the components these items will craft in to - you'll find them referenced in the class: crafting
--- adding items id's to the dbNPC will compile them in server flags
------ these server flags are referenced by the class: inventory, to show if an item is scrappable in the description pane of the q-menu


- you can quickly generate gmaps using the dbNPC: GmapGenertator
--- edit the script ti include 3 things: (1) your gmap/level prefix name, (2) your gmap width (in levels), (3) your gmap height (in levels)
--- after saving the script with the above updated, your gmap will be generated in the folder levels/gmapgen/
--- drag your .gmap file to the levels/levels/gmaps/ folder
--- drag your levels to whatever levels folder they need to go to
--- warp to your gmap name first (ex: warpto 30 30 my_gmap.gmap) to stitch the levels together and load the gmap... then you can warp to the gmap's level names individually thereafter


** migrating guis to mobile **
1) add join("gui_common"); at the top of your script
2) call addControlsContainer(); clientside, before creating any of your GUI
3) wrap existing GUI window/bitmap in ControlsContainer2
--- ex, nest your entire GUI inside this: with (ControlsContainer2) { }
4) change the window ctrl to a bitmap ctrl (may not be necessary anymore)
--- ex: profile.bitmap = era_mobile-window-bitmap.png and change GuiWindowCtrl to GuiBitmapCtrl
5) change the x/y of the window/bitmap ctrl to new coords:
--- x = ControlsContainer2.clientWidth / 2 - width / 2;
--- y = ControlsContainer2.clientHeight / 2 - height / 2;


** adding touch-scroll to guis **
1) add this.join("gui_touchscroll_erapc"); to scroll controls
2) add catch event for the child ctrls (rename events called):
- thiso.catchEvent(this, "onMouseDragged", "onDragged");
- thiso.catchEvent(this, "onMouseUp", "onUp");
- thiso.catchEvent(this, "onMouseDown", "onDown");
3) add event functions for each event to be called, which triggers the parent:
- function onDown(obj, modifiers, mx, my, clickcount)
---obj.parent.trigger("onMouseDown", modifiers, mx, my, clickcount);


- no longer need to put seteffect() in a timeout in your level NPCs...if you see this, please update it
--- do so by replacing any seteffect() level npc with this code, plugging in the new values you want to use:
    //#CLIENTSIDE
    function onPlayerEnters(){
      // red, green, blue, alpha values (0-1)
      setEffect(0, 0, 0, 0.4);
    }


- auction results can be output in a nice legible format using -angel/auctionlogparser
--- spits a file into temp folder all formatted with accounts, item purchased and value
--- blank items (0s) are houses


- there is a new baddy system with good pathfinding and ability logic foundation in angel_baddy* classes
--- you can add areas to consistently spawn baddies from this system via Control_Baddys
----- you can also manage loot drops from these mobs in this same dbnpc
--- there are some "waves" of baddies that can also be scheduled or let loose as a one-off in Halloween_ZombieInvasion


- there is an ideal way to handle temporary currency items that we dont utilise often enough
--- create the currency item and make it non droppable
--- let your holiday or temporary event run it's course
--- when the event is done, allow some kind of exchange to get rid of them (optional)
--- after a reasonable amount of time, or before starting the follow up year's holiday, remove the item from all players
----- you can do this using the !removeall command added in RCBot
------- it will scan and remove item IDs from all players everywhere
--- following this approach, you won't have to create an item every year or replace all quest/craft/etc item IDs to a new one
----- remember to always use !scanaccs after performing this to double check the item gets removed as expected
