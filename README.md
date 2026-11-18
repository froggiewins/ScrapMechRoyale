# Irondust: Wasteland Mech Wars

A 3D browser game about building custom war mechs and battling in an abandoned wasteland. It's a single `index.html` file with no build step, made with three.js.

**Play:** enable GitHub Pages for this repo (Settings → Pages → Deploy from branch → `main` / root) and open the site URL.

## Features
- **Garage:** 7 chassis (walkers, quad, tread tank, hover skimmer, Basilisk serpent), 20+ arm weapons, melee weapons, back-mounted weapons, special systems, paint colours and patterns.
- **Progression:** earn scrap from kills, salvage and supply drops to unlock parts. Progress is saved in your browser.
- **Physics:** momentum-based, mech-to-mech collisions and ramming, toppling and getting back up, jetpack flight.
- **Online multiplayer** via Supabase Realtime, plus **raider AI** opponents with three skill levels.
- **World:** a ruined city map with dust storms, supply drops, time of day and destructible-looking wreckage.
- **Graphics:** post-processing (bloom and colour grading) with Low / Medium / High quality settings.

## Controls
| Key | Action |
|---|---|
| WASD | Move |
| Mouse | Aim |
| Left / Right mouse | Fire left / right arm |
| Q or middle mouse | Back weapon |
| Shift | Boost |
| Space | Hop / hold for jetpack thrust / stand up after toppling |
| F | System (shield, jetpack, repair, missiles, EMP) |
| R | Vent heat |
| Tab | Scoreboard |
| Esc | Pause |

## Online play
Online multiplayer uses **Supabase Realtime** (broadcast and presence channels; no database tables needed). Everyone who opens the site joins the same live battle. The garage has 3 sectors, which are separate rooms. Each player's game calculates the damage their own mech takes, and kills are credited across players.

The project URL and publishable key are in `index.html`. Publishable keys are designed to be public. If online play shows **OFFLINE**, check that Realtime is enabled for the Supabase project, and that public (non-private) channels are allowed under Realtime settings.

If Supabase can't be reached, the game falls back to solo battles against raider AI.

## Anti-cheat
There's no game server (only Supabase Realtime relays messages), so every player's browser checks the other players:
- **Sealed code:** the game runs inside a closure with no debug handle, so its state, scrap and weapon stats can't be edited from the browser console. Game data is frozen.
- **Save data is signed:** editing scrap or unlocks in localStorage resets progress. Scrap gains are also capped per minute.
- **Weapon checks:** shots are only accepted from weapons in the sender's loadout, at the weapon's real fire rate, and from near the sender's position.
- **Movement checks:** teleporting, impossible speed, flying out of bounds and impossible armor values are detected.
- **Damage checks:** each player's game works out the damage it takes, using its own copy of the weapon stats. Players whose armor never drops after taking a lot of confirmed hits are flagged.
- **Kill and pickup checks:** kills are only credited if you actually hit that player in the last few seconds. Supply-drop claims must come from near the crate.
- **Flood guard:** players sending too many messages have the extras dropped.
- **Consequences:** offenders build up strikes and get flagged (⚠ next to their name). A flagged player's attacks are ignored, so they can't hurt anyone.

Limits: a determined cheater can still modify their own copy of the page (for example, to stop taking damage on their own screen). Because each player's game decides what hits it, this mostly can't hurt other players. Fully server-authoritative anti-cheat would need a game server.
