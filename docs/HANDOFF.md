# Kingdom Come Craft — design handoff

Status: design interview in progress. Nothing built yet.

## Agreed so far
- One sentence: Minecraft Java looks completely vanilla until a mob turns hostile; then it fights with
  Kingdom Come: Deliverance II combat, and the player fights by the same rules.
- Host (role "primary"): Minecraft: Java Edition, on Melty's portable Prism Launcher instance with Fabric.
- Companion (role "companion"): Kingdom Come: Deliverance II (`{game:kingdom-come-deliverance-2}`).
  The mod reads weapon/armor stats, combat data and animations from the player's own copy at runtime.
  No KCD II files ever go in the upload or this repo.
- Solo for v1; keep the design ready for multiplayer later.
- First minute: normal world, no menu changes, new blocks or special spawn; the first hostile mob
  switches to a KCD II stance.
- v1 must have: KCD II melee for player and humanoid hostiles (stance, directional swings, block,
  perfect block, riposte, stamina); hostile switch; weapon-type -> vanilla Minecraft model mapping with
  stats/moveset from KCD II data; bows/crossbows with KCD II handling; armor coverage + hit-location
  damage; bipedal gag (polar bear + a couple of other quadrupeds stand up when hostile).
- Later: two-legged Ender Dragon, then multiplayer.
- Account risk: none stated by the user (Denuvo is copy protection, v1 is solo). Confirm with game_info.

## Work happens on the user's PC
The user chose to run Claude Code locally on the PC that has both games, so the agent can read the
installs directly and test in the running game.

## First steps for the local session
1. Connect to Melty (the user re-pastes the Melty Publish prompt; the token is never written to files).
   Call list_my_mods, search_games (confirm the `kingdom-come-deliverance-2` slug), game_info on
   minecraft-java and KCD II, search_mashups for both, mashup_info skycraft.
2. Locate both installs (Steam/GOG/Epic library folders; Prism/Minecraft).
3. Animation feasibility spike (gates the rest of the design): find KCD II's animation data in its
   .pak archives (CryEngine .caf/.dba/.chrparams expected), try to decode one clip and map its
   skeleton onto Minecraft's biped parts. Report exactly what fails, if anything. No look-alike
   substitutes.
4. Confirm KCD II table names for weapons/armor (KCD I used Libs/Tables/... melee_weapon.xml,
   weapon.xml, armor.xml; verify for II).
5. Then: JSON sheets (weapons, armor, damage zones, mob combat profiles, bipedal mob models,
   hooks into Minecraft), preflight, build.

## Toolkit
universal-modder: https://github.com/rehan-remade/universal-modder (skills/mod-any-game/SKILL.md).
