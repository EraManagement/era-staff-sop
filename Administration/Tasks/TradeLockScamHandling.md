# Trade Lock and Scam Handling SOP

Use this SOP when an admin needs to restrict a player from trading-related systems because of USD behavior, scams, repeated abuse, suspicious transfers, or ongoing investigation.

## When To Use

Use trade lock when a temporary or ongoing restriction is safer than an immediate ban, especially when staff need to preserve the account while preventing further movement of value.

Common reasons:

- USD trading or attempted USD trading
- Scam reports with credible evidence
- Suspicious item or money movement
- Repeated abuse of trades, lends, market, or bank transfers
- Player under investigation for economy abuse

## Required Access

Trade lock is applied by setting this player flag:

```text
clientr.tradelocked=1
```

Remove the restriction by clearing the flag or setting it back to false/zero, based on the staff tool being used.

## What Trade Lock Blocks

Existing staff notes say trade lock blocks:

- Bank transfers
- Picking up player-owned dropped items
- Trades
- Lends
- Marketplace activity
- Other economy-related areas

Script-confirmed examples:

- `-TradeSystem` closes trade flow if `player.clientr.tradelocked` is true.
- `classes/items.gs2` blocks pickup of player-owned items when the picker is trade locked.
- `Phones/ATMPhone` blocks sending gPhone bank transfers to a trade-locked target.
- `classes/betflip.gs2` blocks betflip participation while trade locked.

Players may still be able to pick up dropped money from the ground.

## Evidence To Collect First

Before locking when time allows, collect:

- Player account and community name
- Other accounts involved
- Trade logs
- Item logs
- `bankatm` logs
- `atmlog.txt` and `atmlog_bigxfers.txt`
- Marketplace logs if involved
- Player statements or screenshots as supporting evidence

If the player is actively moving items/money, lock first and document immediately afterward.

## Procedure

1. Confirm the real account name.
2. Review the active report or live evidence.
3. Apply `clientr.tradelocked=1`.
4. Check whether the player is currently trading, using gPhone transfers, using marketplace, or dropping/picking items.
5. Record the reason, time, staff member, and evidence.
6. Notify relevant staff channels if the case involves high-value items, USD, or multiple accounts.
7. Continue investigation using logs.

## Review While Locked

Check:

- Personal logs under `logs/pl/<first_letter>/<account>*.txt`
- Trade logs
- Item drop/pickup logs
- Bank ATM logs
- Marketplace logs
- Known alts and IP/PC relationships if needed

Use the lock to prevent additional damage while staff decide whether to restore, confiscate, warn, ban, or unlock.

## Unlock Procedure

Only unlock after:

- The case is resolved
- Required restorations/removals are complete
- Relevant staff agree the restriction is no longer needed
- Notes are updated

When unlocking, document who removed the lock and why.

## Do Not Do

- Do not use trade lock as a punishment without notes.
- Do not unlock a player only because they ask.
- Do not assume trade lock blocks every possible value movement.
- Do not skip log review when the case involves valuable items or large money transfers.
- Do not forget that trade-locked players may still pick up dropped money.

## Source Reference

- `Administration/Server Knowledge.md`
- `weapons/-TradeSystem.gs2`
- `classes/items.gs2`
- `weapons/Phones%2FATMPhone.gs2`
- `classes/betflip.gs2`
