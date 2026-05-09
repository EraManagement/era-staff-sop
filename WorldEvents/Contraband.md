# Contraband Shipment SOP

Contraband Shipment is a world event where players intercept a package, carry it to the correct drop-off, and receive rewards if the delivery succeeds. The event is controlled by `classes/worldevent_contraband.gs2` and registered through `npcs/WorldEvent_Control.gs2`.

## Staff Start Commands

- `/npc contraband` starts a random Contraband Shipment.
- `:contraband` starts Contraband at the staff member's current position while on staff tag.

The event will not start if another world event is already active.

## Player Objective

Players must find the package, grab it, carry it to the correct drop-off, and press the Drop key inside the valid circle. The carry weapon currently listens for keycode `65`, which is the `A` key.

The package starts with 2000 HP. Players can damage it, but if the package reaches 0 HP the event ends as destroyed and nobody receives delivery rewards.

## Drop-Off Rules

Drop-off eligibility depends on the carrier's affiliation:

- Civilian players deliver to the Civilian Dropoff on Gang Island.
- Era Police members deliver to the Era Police Dropoff.
- South Ridge Mafia members deliver to the South Ridge Mafia Dropoff.
- Other gang members can deliver to their gang base if `Gangs.isInGangBase()` recognizes the location.

Hard-coded special drop-offs:

- Civilian Dropoff: `era_overworld.gmap`, x `93`, y `324`, radius `12`
- Era Police Dropoff: `era_overworld.gmap`, x `83`, y `473`, radius `12`
- South Ridge Mafia Dropoff: `era_overworld.gmap`, x `222`, y `461`, radius `12`

## Carry Rules

When a player picks up the package:

- Weapons, melee, grab, and normal animations are temporarily disabled.
- The player uses box carry animations.
- Movement is slowed through `client.slowMovement`.
- Taking damage causes the carrier to drop the package.
- Entering invalid levels silently drops the package and warns the player.
- The package marker updates to follow the carrier on the overworld.

Invalid areas include houses, apartments, duel levels, tutorial levels, and jail levels. `era_traphouse-pkv2.nw` is explicitly allowed even though it contains `house` in the name.

## NPC Pressure

The event spawns route escort NPCs at the package. Additional waves can appear in two situations:

- Defense waves spawn after the package has been dropped and left idle.
- Carrier route waves spawn ahead of the carrier after enough travel distance and cooldown time.

These guards use `worldevent_baddy_routeescort` and are cleaned up with the event.

## Rewards

Successful civilian delivery:

- `$8000`
- `2` Event Coins

Successful gang delivery:

- Carrier receives `$10000`
- Carrier receives `3` Event Coins
- Carrier receives `1` Season 5 Arena Token

Gang helper reward:

- `$4000`
- `1` Event Coin

Gang helpers qualify by either carrying the package at least once or staying in the helper zone near the carrier for at least 20 seconds.

## Event End States

Contraband can end by:

- `gang_delivery`: gang delivery succeeds.
- `citizen_delivery`: civilian delivery succeeds.
- `destroyed`: package HP reaches zero.
- `expired`: timer or staff cleanup ends the event.

The event duration is 15 minutes. Cleanup removes the package, car prop, guards, wave NPCs, drop-off markers, helper zone, HUD state, and map marker.

## Troubleshooting

- If the event will not start, check whether `WorldEvent_Control.eventActive` is already true.
- If players cannot deliver, verify their affiliation and that they are inside the correct drop-off radius.
- If the package disappears, check whether the carrier died, entered an invalid level, or the package was destroyed.
- If markers remain after the event, use the controller stop function or resave/reload the controller so `onStopEvents()` clears state.

## Source Reference

- `npcs/WorldEvent_Control.gs2`
- `classes/worldevent_contraband.gs2`
- `classes/func_contraband_event.gs2`
- `classes/worldevent_addon_contrabandpackage.gs2`
- `weapons/WorldEvent%2FContraband Carry.gs2`
- `weapons/WorldEvent%2FContraband HUD.gs2`
