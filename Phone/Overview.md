# gPhone Overview

The gPhone is the modern phone and remote ATM system. It is implemented mostly in the `Phones/ATMPhone` weapon, with supporting GUI classes and the `ePhone` subscription DB NPC.

## Source Systems

- Main weapon and server actions: `weapons/Phones%2FATMPhone.gs2`
- ATM app GUI: `classes/gui_phone_atm.gs2`
- Home/settings app GUI: `classes/gui_phone_home.gs2`
- Messages app GUI: `classes/gui_phone_messages.gs2`
- Contacts app GUI: `classes/gui_phone_contacts.gs2`
- EraZon app GUI: `classes/gui_phone_erazon.gs2`
- Subscription controller: `npcs/ePhone.gs2`
- Phone message storage: `npcs/Mail.gs2`
- Bank functions: `classes/bank_functions.gs2`
- Staff commands: `weapons/-Commands.gs2`

## Core Design

The phone is a client GUI shell backed by server-side validation in `Phones/ATMPhone`. Client actions call `triggerserver("gui", "Phones/ATMPhone", action, data)`, and the weapon handles each action in `handleServerAction()`.

The phone should be treated as a UI only. Bank balances, app ownership, subscriptions, purchases, transfers, and app locks are all validated server-side before anything is changed.

## App Catalog

The managed app list currently includes:

- `atm`
- `erazon`
- `camera`
- `contacts`
- `messages`
- `notes`
- `mp3`
- `ppa`
- `stocks`
- `news`
- `bounty`
- `gangs`

The phone also has a `settings` or `Menu` entry that opens phone settings. The app catalog controls label, icon, home position, base state, price, and description.

## App States

Apps can be:

- Installed by default
- Locked until purchased
- Disabled globally by staff
- Force-locked for an account
- Hidden or shown by the player's home screen layout

Global app disable is for maintenance. Force-lock is account-specific and is also used by the subscription system when a phone subscription is canceled or past due.

## Data Storage

App ownership and phone layout are stored in:

`data/phone/gphone_app_ownership.txt`

Common saved keys:

- `owned_<account>` for purchased apps
- `forcedlocked_<account>` for account-specific locks
- `homehidden_<account>` for hidden home apps
- `homeshown_<account>` for default-hidden apps that were manually shown

Notes are stored on the player's `clientr.atmphone_notes_blob` and mirrored to `clientr.atmphone_notes`.

Phone messages use SQL table `phone_messages_v2`, created by `Mail.ensurePhoneMessageTable()`.

## Related SOPs

- [ATM Banking](ATM.md)
- [Staff Controls](StaffControls.md)
