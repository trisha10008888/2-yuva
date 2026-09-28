# ROOMLY 📍

**Find a room. Find your space.**
Real-time free-classroom finder for the IST building at SRM Institute of Science and Technology, Tiruchirappalli.

Students waste free periods walking floor to floor, peeking into rooms, and getting kicked out ten minutes later when a lecture starts. Roomly reads the college timetables and tells you exactly which rooms are empty, for how long, and lets you call your squad there in one tap.

> "Google Maps for empty classrooms, powered by timetable intelligence."

---

## Features

### Phase 1: Smart search
- **Floor-by-floor availability.** Every room from 10 SEEE timetables is checked against the bell schedule and grouped by floor.
- **AI room finder.** Type a sentence like *"I need an AC room on the ground floor for me and my team for the next 2 hours"*. Roomly works out the floor, group size, duration and AC, then returns matching rooms. It also understands periods ("next period", "P6 to P8") and mixed Tamil/Hindi/English.
- **Filters and sorting.** Floor, capacity, AC, projector, whiteboard, lab, quiet room and time window. Sort by best match, nearest, longest availability or capacity.
- **Smart empty state.** When nothing matches perfectly, Roomly shows the closest rooms (with what each one misses). It can also build a plan that hops between rooms so you never get kicked out.

### Phase 2: 3D map, countdown and squad
- **3D building map (Ground to 7th floor).** Rooms are coloured by availability (available, ending soon, occupied, unknown). Hover for a tooltip; tap for details.
- **Live countdown.** A second-by-second timer shows how long a room stays free before the next class arrives.
- **Claim Room.** Mark a room as your squad's, with a pin on the map.
- **Call the Squad.** Opens WhatsApp with a pre-filled message:
  `📍 Heading to IST 416 (4th floor, south wing). It's free until 3:10 PM. Come fast!`
- **Directions.** Step-by-step route from the main stairs.

### Extras
- **My Rooms:** your claimed room and recently viewed rooms.
- **Squad:** team members and their sections, with a "When is everyone free?" planner that finds shared gaps and rooms.
- **Activity:** a log of searches, claims and calls.
- **Time preview:** see availability at any day and time. Countdowns run from that moment, which is handy for demos.
- Light and dark mode, and a mobile layout with bottom navigation and bottom-sheet room details.

---

## Run it locally

No build step and no install. It's plain HTML, CSS and JavaScript.

1. Clone or download this repo.
2. Open the folder in VS Code.
3. Install the **Live Server** extension, right-click `index.html`, and choose **Open with Live Server**.
   You can also double-click `index.html` to open it in a browser.

An internet connection is needed for the Google Font and the three.js library, which load from a CDN.

## Deploy on GitHub Pages

1. Create a new GitHub repository (for example `roomly`) and push these files:
   ```bash
   git init
   git add .
   git commit -m "Roomly: free classroom finder"
   git branch -M main
   git remote add origin https://github.com/<your-username>/roomly.git
   git push -u origin main
   ```
2. On GitHub, go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, then **main** / **(root)**, and click **Save**.
4. After a minute, the site is live at `https://<your-username>.github.io/roomly/`.

---

## Project structure

```
roomly/
├── index.html      # Page layout: sidebar, pages, map stage, drawer
├── css/
│   └── styles.css  # Design system (light + dark), layout, components
├── js/
│   ├── data.js     # The 10 timetables, rooms, bell schedules, availability engine, text parser
│   ├── app.js      # UI: search, results, room details, claim, WhatsApp, pages, live countdown
│   └── map3d.js    # 3D IST building (three.js): floors, colours, tooltips, selection
└── README.md
```

## How availability is calculated

- **Timetables.** The 10 SEEE timetables are I-year (ECE-A, ECE-B & EEE, ECE-DS, Biotech-B & BME), II BME, II ECE-DS A and B, III BME, III ECE-A, B and DS, and IV ECE-A and B.
- **Where each class sits.** A slot letter (A, B, C…) means the class is in the section's home room. A cell like `G-625` or `LAB-108/309` means the class moved to that room, which frees the home room.
- **When a room is free.** Every class blocks its room for its own bell times. A room is free when no timetable books it.
- **Two bell schedules.** The 2026–27 sheets run 9:00–4:50, and the I-year sheet runs 9:00–5:05.
- **Floors.** The floor comes from the room number: IST 0xx is the ground floor, 1xx the first floor, and so on.

### Assumptions (please verify)
- **Room details.** Seats, AC, projector and whiteboard are **estimates**, because the timetables don't list them. Update the `ROOMS` table at the top of `js/data.js` with real details.
- **Building layout.** The 3D building repeats the hand-drawn 4th-floor layout on every floor.
- **I-year sheet.** The I-year timetable provided is labelled 2024–25. Replace it with the current one in `SECTIONS`.
- **Saved data.** Claims, squad and activity are saved in the browser (localStorage) on that device. Sharing claims live between students would need a backend such as Firebase or Supabase.
- **AI search.** Inside claude.ai, Roomly asks Claude to read your sentence. Anywhere else, a built-in parser (rule-based text understanding) handles it, and that works offline.

## Tech stack

- HTML, CSS and vanilla JavaScript (no framework, no build step)
- [three.js](https://threejs.org/) r128 for the 3D map (OrbitControls and CSS2DRenderer)
- Manrope font from Google Fonts
- WhatsApp "click to chat" links (`https://wa.me/?text=…`)

---

Made for the free-class-tracker hackathon at SRM IST Tiruchirappalli.
