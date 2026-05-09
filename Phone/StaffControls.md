# gPhone Staff Controls SOP

Staff controls for gPhone apps and subscriptions are handled through player commands in `weapons/-Commands.gs2`. Most app-management commands require staff level 4 or higher.

## Global App Maintenance

Use `/phoneapp` to disable or enable an app globally.

Commands:

- `/phoneapp list`
- `/phoneapp <app> status`
- `/phoneapp <app> off`
- `/phoneapp <app> on`

Examples:

- `/phoneapp erazon off`
- `/phoneapp erazon status`
- `/phoneapp erazon on`

Global disable is intended for maintenance or emergency shutdown. A disabled app is treated as unavailable for all players.

## App Ownership

Use `/phoneappown` to check, grant, or revoke app ownership.

Self-targeted format:

- `/phoneappown <app> status`
- `/phoneappown <app> on`
- `/phoneappown <app> off`

Targeted format:

- `/phoneappown <account> <app> status`
- `/phoneappown <account> <app> on`
- `/phoneappown <account> <app> off`

Granting ownership also removes the forced lock for that app. Revoking ownership force-locks the app and removes it from the owned list.

## Account Force-Locks

Use `/phoneapplock` to force-lock or unlock a managed app for a specific account.

Commands:

- `/phoneapplock <account> <app> status`
- `/phoneapplock <account> <app> on`
- `/phoneapplock <account> <app> off`

Force-locks are account-specific. They can be applied manually by staff and are also used by the subscription system.

## Subscription Commands

Players can use:

- `/phonesub status`
- `/phonesub cancel`
- `/phonesub reactivate`

Staff level 4 or higher can also update subscription pricing:

- `/phonesub status`
- `/phonesub base <amount>`
- `/phonesub perapp <amount>`

The default subscription configuration is controlled by `npcs/ePhone.gs2`:

- Base weekly fee default: `$2500`
- Per owned app weekly fee default: `$500`

Subscription config is stored in:

`data/phone/gphone_subscription_config.txt`

## Subscription Behavior

The `ePhone` DB NPC checks subscriptions on a schedule and charges eligible accounts weekly.

An account is eligible for subscription checks if it has a phone item, owns paid apps, or is already marked as a subscriber.

If payment succeeds:

- The fee is deducted from ATM balance.
- Funds are deposited into `atmphone-shipping-hold`.
- Purchased apps remain unlocked.
- A payment line is saved to `phones/subscription.txt`.

If payment fails:

- Managed apps are force-locked.
- The player is messaged if online.
- A locked line is saved to `phones/subscription.txt`.

If the player cancels:

- Subscriber state is cleared.
- Canceled state is set.
- Next due time is cleared.
- Managed apps are force-locked until reactivation.

If the player reactivates:

- The base fee or past-due amount is charged from ATM balance.
- Subscriber state is restored.
- Canceled state is cleared.
- Next due time is set one week out.
- Managed apps are unlocked.

## Troubleshooting

- If a player owns an app but cannot open it, check global disable state and account force-lock state.
- If all apps are locked, check whether the subscription is canceled or past due.
- If the app list looks wrong, sync the state bundle by reopening the phone or using the relevant command path.
- If a paid app purchase failed, verify ATM balance and app price in `getPhoneAppCatalog()`.
- If a subscription charge is disputed, check `phones/subscription.txt` and the account bank balance history.

## Source Reference

- `weapons/-Commands.gs2`
- `weapons/Phones%2FATMPhone.gs2`
- `npcs/ePhone.gs2`
- `classes/gui_phone_home.gs2`
