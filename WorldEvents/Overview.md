# World Events Overview

World Events are server-spawned public activities controlled by the `WorldEvent_Control` DB NPC. They are designed to create short server-wide objectives with global announcements, map markers, temporary NPCs, and automatic cleanup.

## Source Systems

- Controller: `npcs/WorldEvent_Control.gs2`
- Staff command bridge: `npcs/Remote-NPC.gs2`
- Player alert GUI: `weapons/-GUI/World_Events.gs2`
- Contraband event: `classes/worldevent_contraband.gs2`
- Cops and Robbers event: `classes/worldevent_copsrobbers.gs2`

## Event Selection

`WorldEvent_Control` defines the available events in `DefineEventParams()`. Each event has:

- Public display name
- Short abbreviation
- Whether teams are used
- Team count, if applicable
- Class spawned into the level
- Minimum player count

Current configured examples include King of the Hill, Zombie Apocalypse, Contraband Shipment, and Cops and Robbers.

## Player Count Rules

The controller has a default minimum player count of 10. Individual events can require a higher count:

- Contraband Shipment requires 25 players.
- Cops and Robbers requires 18 players.

If the player count is too low, the controller cancels pending event schedules and checks again later.

## Staff Controls

Staff can force newer world events through staff-only commands. These commands require sufficient staff level and will fail if another event is already active.

Common commands:

- `/npc contraband` forces a random Contraband Shipment.
- `/npc copsrobbersscene` forces a random Cops and Robbers scene.
- `/npc clearcopsrobbersscene` clears the active Cops and Robbers scene.

Staff on tag can also use chat shortcuts handled by `WorldEvent_Control`:

- `:contraband` forces Contraband at the staff member's current location.
- `:copsrobbers` forces Cops and Robbers at the staff member's current location.

## Operational Notes

- Only one world event should be active at a time. `eventActive` blocks forced starts while an event is live.
- Events announce through the world event GUI and may also use player `addMessage()` instructions.
- Event classes are temporary level NPCs created with `putnpc2()` and cleaned up when the event ends.
- Map markers are stored in `serverr.mapevent` and event-specific marker variables.
- Stale event objects can usually be cleared through the event's stop function rather than manually deleting NPCs.

## Related SOPs

- [Contraband Shipment](Contraband.md)
- [Cops and Robbers](CopsAndRobbers.md)
