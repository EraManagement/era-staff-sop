# Cops and Robbers SOP

Cops and Robbers is a world event where a police cruiser scene spawns on the overworld, NPC cops and robbers fight each other, and players influence the fight by helping either side. The event is controlled by `classes/worldevent_copsrobbers.gs2` and `classes/worldevent_copsrobbers_controller.gs2`.

## Staff Start Commands

- `/npc copsrobbersscene` starts a random Cops and Robbers scene.
- `/npc clearcopsrobbersscene` clears the active scene.
- `:copsrobbers` starts the event at the staff member's current position while on staff tag.

The event will not start if another world event is already active.

## Event Flow

When the event starts, it spawns:

- A hidden scene controller
- A police cruiser prop
- Siren and light effects
- Two cop faction NPCs
- Three robber faction NPCs

The event broadcasts a global message and points players to the cruiser with a HUD/map marker.

## Player Objective

Players choose a side by taking meaningful action in the scene. Damage contributions are tracked separately for cops and robbers.

Era Police members are forced onto the cops side. Other players can help either side, but their first meaningful action locks them to that side for a short time.

Side lock details:

- Side lock duration: 60 seconds
- Side lock warning cooldown: 8 seconds
- Helper pressure radius: 28 tiles around the scene

## Win Conditions

The scene controller checks live faction NPCs:

- Cops win if all robbers are dead and at least one cop is alive.
- Robbers win if all cops are dead and at least one robber is alive.
- The event draws if both sides are eliminated.
- The event expires after 12 minutes if not resolved.

When the event ends, the top event class cleans up all scene NPCs, clears HUD state, clears map markers, and calls `WorldEvent_Control.onStopEvents()`.

## Dynamic Balance

The controller counts nearby live helpers for each side. If one player side has an advantage, reinforcement NPCs can spawn for the other side.

Configured reinforcement behavior:

- Helper advantage threshold: 1
- Reinforcement cooldown: 7 seconds
- Maximum cop reinforcements: 4
- Maximum robber reinforcements: 4

Robber route escort backup can also spawn under pressure, especially when players helping the cops create a strong advantage.

## Rewards

Participation reward:

- Minimum contribution: 25 damage
- `$1750`
- No guaranteed Event Coin from participation

Winning side helper reward:

- Minimum contribution: 25 damage on the winning side
- Base payout: `$4000`
- Base Event Coins: `2`

The winning side payout can scale down if the winning side had a large helper advantage. The payout does not drop below `$500` or below `1` Event Coin.

Losing side bonus:

- Losing-side participants have an 18% chance to receive `1` Event Coin.

## Staff Testing Commands

Additional test commands exist in `Remote-NPC` for development and QA:

- `/npc factionbaddies`
- `/npc factionbaddies <cop_count> <robber_count>`
- `/npc clearfactionbaddies`

These spawn and clear faction baddies near the staff member's current position. They are for testing NPC behavior, not for normal hosted events.

## Troubleshooting

- If the scene does not spawn, check whether another world event is active.
- If forced random spawns fail, the chosen location may not pass road/walkability checks.
- If players report being locked to the wrong side, check their guild and recent contribution side.
- If event objects remain after cleanup, use `/npc clearcopsrobbersscene`.
- If rewards are missing, confirm the player reached the 25 damage contribution threshold.

## Source Reference

- `npcs/WorldEvent_Control.gs2`
- `npcs/Remote-NPC.gs2`
- `classes/worldevent_copsrobbers.gs2`
- `classes/worldevent_copsrobbers_controller.gs2`
- `classes/worldevent_baddy_copfaction.gs2`
- `classes/worldevent_baddy_robberfaction.gs2`
- `weapons/WorldEvent%2FCopsRobbers HUD.gs2`
