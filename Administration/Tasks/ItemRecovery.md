# Item Recovery and Missing Item Claims SOP

Use this SOP when a player reports a missing item, destroyed item, failed pickup, incorrect ownership, or item loss during a trade/drop/market interaction.

## When To Use

Use this for:

- Missing dropped items
- Claims that another player picked up an item
- Items destroyed on the ground
- Trade-drop disputes
- Marketplace or storage pickup issues
- Staff-approved item restoration after verified loss

Do not restore items from screenshots alone. Screenshots can support a case, but server logs are the source of truth.

## Required Access

Typical review requires access to RC logs and player log files.

Adding, removing, or transferring items requires staff item-spawn rights through `Staff.canSpawnItems()` or equivalent staff tooling.

## Evidence To Check

Start with the player's personal logs:

```text
logs/pl/<first_letter_of_account>/<account>*.txt
```

Useful personal logs include:

- `items`
- `bankatm`
- trade logs

System-wide item logs to check:

- `itemlog.txt`
- `item_drop-log.txt`
- `item_take-log.txt`
- `destroyeditemlog.txt`
- `itemsdrop.txt`
- `itemsdrop-droptrade.txt`
- `itemstorage.txt`
- `items_outofbounds.txt`
- `itemlog-noowner.txt`
- `rc_itemcontrol.txt`

For large or complex claims, cross-check marketplace, trade, lending, housing, and bank logs if relevant.

## Common Log Meanings

Drop:

- `classes/items.gs2` logs dropped items as `laid item`.
- Drop lines include owner, item name, amount, level, and coordinates.

Pickup:

- Pickup logs say a player `took item`.
- If the pickup player is not the owner, both the owner and taker can receive account item log entries.

Destroyed:

- Ground item destruction is logged in `destroyeditemlog.txt`.
- Items can be destroyed by decay, staff action, attack damage, invalid ownership, out-of-bounds placement, or special item rules.

Storage:

- Staff storage actions log to `itemstorage.txt` and `itemlog.txt`.

Trade drop:

- Items dropped in `era_mesh-trade.nw` also log to `itemsdrop-droptrade.txt`.

## Review Procedure

1. Confirm the real account name.
2. Confirm the item ID and item name with `/npc iteminfo <item_id>` when possible.
3. Get the approximate time, level, and other accounts involved.
4. Check the player's personal `items` log first.
5. Search `itemlog.txt` for the item ID, item name, account, level, and time window.
6. Check `item_drop-log.txt` and `item_take-log.txt` to pair the drop with a pickup.
7. Check `destroyeditemlog.txt` if the item was on the ground too long, attacked, deleted, or staff-sticked.
8. If the item was in a trade area, check `itemsdrop-droptrade.txt`.
9. If the item went into storage, check `itemstorage.txt`.
10. Decide whether the item was legitimately lost, transferred, picked up, destroyed, or still recoverable.

## Restoration Procedure

Only restore after evidence confirms the player should have the item.

Options:

- Use `/npc additem <account> <item_id> <amount>` for verified restoration.
- Use `/npc transferitem <from> <to> <item_id> <amount>` when the item should move from one player to another.
- Use `/npc removeitem <account> <item_id> <amount>` when correcting duplicated or wrongly restored items.

Before restoring:

- Confirm the exact item ID.
- Confirm the exact amount.
- Confirm whether the target player is online or offline.
- Record the reason and evidence.

After restoring:

- Verify the player received the item.
- Add a note to the staff ticket or case record.
- Include the log lines that justified the action.

## Known Item Drop Bug

There is a known item-drop issue where modified dropped item values can cause the server to protect itself by deleting nearby dropped items.

Existing recovery note:

- RC may show script errors around dropped item NPCs.
- Clear the affected level with `/clearnpcs <levelname>`.
- After clearing, review item logs before restoring anything.

## Do Not Do

- Do not restore from screenshots alone.
- Do not restore if logs show the item was validly picked up or traded.
- Do not use community names where account names are required.
- Do not ignore item ownership. Dropped item logs include both owner and taker for a reason.
- Do not use staff additem as a convenience reward path. It must be evidence-based.

## Source Reference

- `classes/items.gs2`
- `npcs/Remote-NPC.gs2`
- `Administration/Bugs/ItemDrop.md`
- `Administration/Server Knowledge.md`
