# Irondust: Wasteland Mech Wars

A 3D browser game about building custom war mechs and battling in an abandoned wasteland. It's a single `index.html` file with no build step, made with three.js.

**Play:** enable GitHub Pages for this repo (Settings → Pages → Deploy from branch → `main` / root) and open the site URL.

## Features
- **Garage:** 7 chassis (walkers, quad, tread tank, hover skimmer, Basilisk serpent), 20+ arm weapons, melee weapons, back-mounted weapons, special systems, paint colours and patterns.
- **Progression:** earn scrap from kills, salvage and supply drops to unlock parts. Progress is saved in your browser.
- **Physics:** momentum-based, mech-to-mech collisions and ramming, toppling and getting back up, jetpack flight.
- **Raider AI** opponents with three skill levels.
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

## Note on online play
Live multiplayer and the admin panel use features that only exist when the game runs as a Claude artifact. On GitHub Pages the game runs in offline mode against raider AI. Adding hosted multiplayer would need a realtime backend such as Supabase Realtime.
