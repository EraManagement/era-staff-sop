**There's a known issue where if a player uses cheatengine to change the values of an item dropped it
the server will protect itself by deleting any items dropped on the floor in the vicinity of where it was done.**

---

**The Remote Control will alert you and it should look like this:**
[01:42 PM]RC:Script: Function setShape not found at line 20 of block in script of n
[01:42 PM]RC:Script: Function blockAgain not found at line 21 of block in script of n
[01:42 PM]RC:Script: Function onwall2 not found at line 42 of bounds in script of n
[01:42 PM]RC:Script: Function setShape not found at line 20 of block in script of n

[01:45 PM]RC:Script: Function destroy not found at line 39 of pluto_healring in script of npc
[01:45 PM]RC:Script: Function destroy not found at line 43 of pluto_healring in script of npc
[01:45 PM]RC:Script: Function drawunderplayer not found at line 14 of pluto_healring in script of npc
[01:45 PM]RC:Script: Function dontBlock not found at line 15 of pluto_healring in script of npc
[01:45 PM]RC:Script: Function destroy not found at line 39 of pluto_healring in script of npc
[01:45 PM]RC:Script: Function destroy not found at line 43 of pluto_healring in script of npc
[01:45 PM]RC:Script: Function level.findareaplayers not found at line 58 of pluto_healring in script of npc
[01:45 PM]RC:Script: Function destroy not found at line 47 of pluto_healring in script of npc

---

In order to clear the bug, you will have to use this command in Remote control:

**/clearnpcs levelname**

Once the level is cleared, everything should go back to normal.
