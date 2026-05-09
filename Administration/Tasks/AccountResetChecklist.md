# Account Reset Checklist SOP

Use this SOP when an admin is resetting a player account or verifying that an account reset was completed correctly.

## When To Use

Use this for:

- Full player reset
- Seasonal or economy reset review
- Reset-related support tickets
- Cases where an account was reset but still has old money, items, flags, or phone state

Account reset is high-impact. Confirm authorization before proceeding.

## Required Access

Reset workflows may require:

- RC reset command access
- Account file access
- Bank balance change access
- Item add/remove permissions
- SQL or DB NPC access depending on the affected systems

Staff notes warn that staff level 4 opens most administrative doors. Keep resets limited to authorized managers/admins.

## Critical Rule

Resetting a player does not automatically reset their bank account.

After any account reset, always check and reset the player's bank balance separately when appropriate.

Use:

```text
/npc checkbank <account>
```

Then follow:

```text
Administration/Tasks/BankBalanceReview.md
```

## Pre-Reset Checklist

Before reset:

- Confirm the real account name.
- Confirm the reset reason and authorization.
- Check whether the player is online.
- Record current bank balance.
- Record relevant inventory or valuable items if needed.
- Check active housing, gangs, marketplace listings, lends, trades, parties, and phone app state if relevant.
- Back up or document any special items that should be restored after reset.
- Notify the player only if policy requires it.

## Reset Procedure

1. Confirm account name and authorization.
2. Back up or log required pre-reset data.
3. Run the approved account reset process.
4. Disconnect/reconnect the player if the reset process requires it.
5. Confirm the account loads cleanly after reset.
6. Check bank balance.
7. Clear or correct bank balance if required.
8. Review inventory for items that should not remain.
9. Review system-specific leftovers.
10. Add staff notes with what was reset and what was intentionally preserved.

## Systems To Review After Reset

Bank:

- Check with `/npc checkbank <account>`.
- Reset or correct with `/npc changebank` only after calculating the intended final balance.

Inventory:

- Check remaining `clientr.itemc` state if the reset was meant to clear items.
- Review `auto-reset.txt` or item logs if old items were removed automatically.

gPhone:

- Review app ownership and force-locks if the player should start fresh.
- Subscription state may persist through `clientr.gphoneSubSubscriber`, `clientr.gphoneSubCanceled`, and `clientr.gphoneSubNextDue`.
- App ownership/layout is stored in `data/phone/gphone_app_ownership.txt`.

Housing:

- Check owned houses, furniture, storage, and keys if the reset should remove housing state.

Gangs:

- Check gang membership, loyalty items, gang points, and related flags.

Marketplace and Lending:

- Check active listings, stored marketplace items, lends, and borrowed items.

Cars:

- Check `player_cars` if car ownership or towing state is part of the reset.

Quests and Stats:

- Check quest flags, achievements, spar stats, bounty stats, job progress, and event currencies depending on the reset scope.

## Seasonal Reset Notes

Seasonal item wipes should use one-time flags so players are not wiped repeatedly on every login.

Before pushing a seasonal wipe:

- Confirm item IDs.
- Use a new year-specific flag.
- Test on a dev account.
- Use `/npc reconnectall` only when online players must be forced through login/init logic immediately.

## Do Not Do

- Do not reset a player without documenting the reason.
- Do not assume bank balance was reset.
- Do not reuse old seasonal wipe flags.
- Do not wipe special/restorable items without a backup.
- Do not use community names where account names are required.
- Do not leave trade, market, phone, housing, or gang state unchecked when doing a full reset.

## Source Reference

- `Administration/Server Knowledge.md`
- `Administration/Items/ServerWideItemWipe.md`
- `Administration/Tasks/BankBalanceReview.md`
- `npcs/Control_WinterReset.gs2`
- `npcs/Remote-NPC.gs2`
- `npcs/ePhone.gs2`
