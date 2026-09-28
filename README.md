# Curios of Nancy — The Great Heritage Quest

A team-building game about Nancy's **culinary, artistic and cultural heritage**, made with [GDevelop](https://github.com/4ian/GDevelop).
2 to 6 teams share one phone, tablet or big screen. Teams take turns choosing stations on a real map of Nancy, play short challenges, level up, befriend the "Curios" (spirits of Nancy's heritage) and work together towards a shared goal. The game is in English and adapts to phones and tablets, in portrait or landscape.

**Play it:** open `docs/index.html` through any web server, or publish the `docs/` folder with GitHub Pages (see below).
**Edit it:** open `game/game.json` in GDevelop 5.

## How a game works

| Step | What happens |
|---|---|
| **Setup** | 2–6 teams, names and mascots, and a game length: Quick (6 stations, ≈15 min), Standard (9, ≈25 min) or Grand Tour (12, ≈35 min). |
| **Expedition map** | The active team picks one of 12 stations on the map of Nancy. There are three trails: **Culinary**, **Artistic** and **Cultural**. |
| **Challenge** | A briefing, a 1–3 minute mini-game, then the results and a heritage fact about the place. |
| **Levels & perks** | Points are XP. Teams level up from Explorers to Stanislas' Own and earn **Mira's Help** (hints, extra throws, more time) and **Double Down** (×2 on the next challenge). |
| **Curios** | Master a station and your team befriends its Curio: Macarette, Gallébrille, Stanislion… |
| **Golden Gates** | Every point from every team fills a shared meter. Reach the goal together for the bonus ending. |
| **Grand Finale** | An all-team buzzer round, then the podium, an award for every team, and debrief questions. |

### The 8 challenge types

| Challenge | Who plays | Heritage |
|---|---|---|
| Heritage Quiz | active team — others can **steal** a missed question | sweets, Art Nouveau, festivals |
| Buzzer Battle | **all teams**, first to buzz answers (keys 1–6 on a keyboard) | culinary, history |
| Where in Nancy? | **all teams** secretly pin landmarks on an unlabelled map of Nancy | heritage sites, Art Nouveau sites |
| Recipe Relay | active team picks the authentic ingredients | quiche lorraine, potée lorraine |
| Macaron Toss | active team, **every teammate throws once** (timing game) | Maison des Sœurs Macarons |
| Art Nouveau Match | active team, memory pairs: artist ↔ craft | Gallé, Majorelle, Daum, Gruber… |
| Stained-Glass Puzzle | active team rebuilds a window | Musée des Beaux-Arts |
| Timeline of Lorraine | active team orders 5 key dates | 1336 → 1983 |

### For the facilitator

The ☰ menu, available everywhere during a game, lets you:
- adjust scores (±50, e.g. for real-world bonus activities)
- skip a challenge
- jump to the Grand Finale
- turn sound on or off
- go full screen

The game **saves automatically**: if the browser is closed, "Resume expedition" picks up where you left off. See [FACILITATOR.md](FACILITATOR.md) for a run sheet.

## Project structure

```
game/game.json          GDevelop project (open this in GDevelop 5)
game/assets/            sprites, map, fonts, sounds used by the project
docs/                   exported HTML5 game (GitHub Pages serves this folder)
src/content.js          ALL game text: places, Curios, stations, questions, recipes, dates, awards
src/engine.js           responsive UI toolkit, state, scoring, levels, facilitator menu
src/challenges.js       the 8 mini-games
src/scenes/*.js         the 5 scenes: Title, Setup, Hub, Challenge, Finale
tools/                  build scripts (Node.js)
```

In GDevelop, the code lives in **JavaScript events**:
- The external events *Content*, *Engine* and *Challenges* hold the shared code.
- Each scene links to them, runs its own screen code, and also has a regular "At the beginning of the scene" event.

The global objects are `Paint` (shape painter), `TxtBody`, `TxtBold` and `TxtTitle` (texts), the `Curio`, `NancyMap`, `Glass`, `Macaron`, `CardBack` and `Crest` sprites, and `NameInput` (text input). The engine draws everything with them each frame and resizes the game resolution to the screen, so text stays sharp on any phone or tablet.

## Changing the content

Edit `src/content.js`, then rebuild. For example, add a question to `questions.culinary`: the first answer is the correct one, and answers are shuffled on screen. You can also edit the *Content* external events directly in GDevelop and export from there.

## Rebuilding

Requires Node.js 18+.

```bash
cd tools
npm install
npm run osm      # once: download OpenStreetMap data for the map
npm run assets   # draw sprites, map, glass tiles, sounds into game/assets
npm run build    # write game/game.json and export the HTML5 game to docs/
```

The build uses GDevelop's own core library and runtime, packaged by [gdcore-tools](https://github.com/arthuro555/gdcore-tools) (GDevelop 5.6.269). The saved project opens in GDevelop 5.6 and newer.

## Publishing on GitHub Pages

1. Push this folder to a GitHub repository.
2. On GitHub, open **Settings → Pages → Build and deployment**, choose *Deploy from a branch*, then *main* and */docs*.
3. The game is served at `https://<user>.github.io/<repo>/`. Share the link, or add it to a phone's home screen.

## Credits & licences

- Engine: [GDevelop](https://github.com/4ian/GDevelop) (MIT). The "Made with GDevelop" splash is kept.
- Map data © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors (ODbL), drawn without labels for the game.
- Fonts: Federo and Atkinson Hyperlegible (SIL Open Font License, see `game/assets/fonts/`).
- Curios artwork, sounds and code were made for this project.
- Heritage facts should be proofread by a local expert before commercial use.
