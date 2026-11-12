# Dead Acre

A 2D zombie apocalypse survival game that runs in the browser and installs like an app. Scavenge, craft weapons and armor, build a base, drive across a big map, hunt minibosses for special weapons, and survive until the helicopter comes.

Built to be played on a phone (portrait or landscape). No build step: the whole game is one `index.html`.

## Features

- **Survive the nights.** Gather wood, stone, and scrap by day. Zombies swarm at night, and each night is bigger than the last.
- **Craft and build.** 18 recipes (weapons, armor, medkits, grenades, molotovs) and 11 building pieces (walls, turrets, spikes, mines, gates, storage, workshop, beacon). A workshop upgrades weapons, turrets, walls, armor, and your backpack.
- **Zombie variety.** Walkers, runners, tanks, spitters, and brutes, each in three looks, with grittier pixel art and walk animations.
- **A big map.** About 6,600 x 7,200 px with curved and straight roads, a town, a lakeside town and pond, farms, cabins, a marina, a lighthouse, bunkers, labs, and a military base. Drive cars, trucks, and bikes.
- **The Dead Zone.** A fenced, much harder area in the east with toxic clouds, tougher zombies, and the best loot.
- **Minibosses.** Five named elites each drop a unique weapon: Siege Cannon, Butcher Cleaver, Inferno, Arc Rifle, and Tidal Spear. Markers show on the minimap and as screen-edge arrows.
- **Story and NPCs.** A main storyline ("Signal") with side quests, a medic, a radio operator, a trader, and survivors you can rescue and put to work.
- **Saving.** Three save slots, autosave every 20 seconds, and a main menu with Continue, Load Game, and New Game.

## Controls

| Action | Touch | Keyboard |
|---|---|---|
| Move | Left joystick | WASD or arrow keys |
| Mine, open, talk, drive | Use button | E or Space |
| Throw grenade or molotov | Throw button | Q |
| Use a medkit | Heal button | H |
| Bag | Bag button | I |
| Craft, Build, Menu | Icon buttons | click |

Weapons fire automatically at the nearest zombie. In Build mode, tap or drag on the ground to place pieces, and use the Remove tile to salvage.

## Play

Open `index.html` in a modern browser, or serve the folder (some features, like the service worker, need `http://` or `https://`):

```bash
npm start            # or: python3 -m http.server 8080
# then open http://localhost:8080
```

## Install as an app (PWA)

Once the game is hosted on `https://` (for example on GitHub Pages):

- **Android (Chrome):** menu, then *Install app* or *Add to Home screen*.
- **iPhone / iPad (Safari):** Share button, then *Add to Home Screen*.
- **Desktop (Chrome / Edge):** click the install icon in the address bar.

It then launches fullscreen, works offline, and keeps your saves.

## Deploy to GitHub Pages

1. Create a new GitHub repository (for example `DeadAcre`) and push this folder to the `main` branch.
2. In the repository, open **Settings, then Pages**, and set **Source** to **GitHub Actions**.
3. Push to `main`. The workflow in `.github/workflows/pages.yml` runs the tests and publishes the game.
4. Your game will be at `https://<your-username>.github.io/<repo-name>/`.

All paths in the game are relative, so it works under a repository subpath.

## Saves

Saves use the browser's `localStorage` on the device and browser where you play. They do not sync between devices, and clearing site data erases them. If the browser blocks storage, the main menu shows a warning.

When you publish a new version, bump `CACHE` in `sw.js` (for example `dead-acre-v2`) so installed copies pick up the update.

## Project layout

```
index.html              the whole game (HTML, CSS, JavaScript)
manifest.webmanifest    PWA manifest
sw.js                   service worker (offline + install)
icons/                  app icons
tests/                  headless tests and a balance simulator
.github/workflows/      GitHub Pages deploy
```

## Tests

The tests load the game script from `index.html`, stub the browser, and exercise the systems (crafting, building, saving, quests, world generation, special weapons, and more). They need Node 18 or newer.

```bash
npm test             # run all cases
npm run sim          # scripted bots play full games to check balance
RUNS=10 MAXN=12 npm run sim
```

## Wrap it as a native app (optional)

The PWA install is the simplest route. To publish to an app store you can wrap the same files:

- **PWABuilder:** go to pwabuilder.com, enter your hosted URL, and download an Android or iOS package.
- **Capacitor:** `npm i @capacitor/core @capacitor/cli`, then `npx cap init`, set the web folder to this project's files, and `npx cap add android` or `ios`.

These routes are not set up or tested in this repository.

## License

MIT. See `LICENSE`.
