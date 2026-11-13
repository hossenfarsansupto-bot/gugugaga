# Cosmic Saga 🚀

> **Interactive NASA History Experience**  
> Explore retired space exploration hardware and pivotal science missions across the Moon, Mars, and Deep Space with your android feline guide, **Felice** (`FELI LIC ZRSNT67`).

---

## 🌟 Overview

**Cosmic Saga** is an educational, interactive web experience built with React, TypeScript, and Vite. Players journey across the Solar System aboard an interstellar observation ship, visiting legendary human-made exploration hardware left behind on alien worlds and drifting through deep space.

Key destinations and missions covered:
- 🌕 **The Moon**:
  - *Lunar Laser Ranging Retroreflectors* (Apollo 11, 14, 15, Lunokhod 1 & 2)
  - *ALSEP* (Apollo Lunar Surface Experiments Package)
- 🪐 **Mars**:
  - *Viking 1 & 2* (First successful long-term landers & atmospheric biology)
  - *Sojourner Rover & APXS* (Pathfinder mission and alpha particle X-ray spectrometry)
  - *Phoenix Mars Lander* (TEGA, MECA & MET arctic polar station)
- ✨ **Deep Space & Interstellar**:
  - *Pioneer 10 & 11* (Asteroid belt transit, Jupiter/Saturn flybys, iconic Golden Plaque)
  - *Voyager 1 & 2* (Grand Tour, Pale Blue Dot, Golden Record, interstellar space)
  - *Deep Space 1 & New Horizons*
- 🚨 **Supernova Emergency Climax & Finale**:
  - Emergency Threat Level 7 radiation event with improvised scrap shielding, hyperdrive turnaround, and closing credits tribute to Félicette (the first cat in space).

---

## ✨ Features

- 🛸 **Cockpit & EVA Interactive Modes**:
  - Dynamic 2D canvas simulation with realistic planetary surfaces (Moon & Mars), starlight fields, rover exploration, and hyperdrive warp effects.
  - Cockpit view with interactive *Astro-Pad* navigation console.
- 🐱 **Felice the Android Guide**:
  - Expressive character animations, customizable voiceover presets (*Child Voiceover* & *Warm Storyteller*), neural audio narration clips, and Web Speech API fallback.
  - In-dialogue pause and mute controls.
- 🚨 **Dynamic Sci-Fi Sound Effects & Alarms**:
  - Pure Web Audio API synthesizers for UI clicks, page turns, ambient planetarium drones, and an *Among Us*-style red-alert sabotage klaxon alarm during radiation spikes.
  - Dedicated **Master Volume** slider (`0%`–`100%`) with persistent audio scaling in settings.
- ⚙️ **Accessibility & Customization**:
  - Text sizing controls (`Small`, `Normal`, `Large`).
  - Adjustable typing speed (`Normal`, `Fast`, `Instant`).
  - Reduced Motion mode for sensitive users.
  - Automatic state persistence via `localStorage` with save-state resumption.
- 📦 **Offline-Ready & Static Hosting**:
  - Bundled as a 100% static, client-side application ready for GitHub Pages, Cloudflare Pages, Firebase Hosting, or Netlify.

---

## 🛠️ Tech Stack

- **Framework**: React 19 + TypeScript
- **Bundler & Dev Server**: Vite 6
- **Audio Engine**: Web Audio API (offline-safe synthesized tones & loops) + HTML5 Audio / Web Speech API
- **Visuals & Animation**: Canvas 2D, SVG vector illustrations, CSS Keyframes & Glassmorphism UI
- **Typography**: Custom NASA-inspired techno font (`CosmicTech.ttf`)

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (version 18 or higher recommended)
- `npm` (comes with Node.js)

### Installation

1. Clone or download the repository:
   ```bash
   git clone https://github.com/<your-username>/cosmic-saga.git
   cd cosmic-saga
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the local development server:
   ```bash
   npm run dev
   ```
   Open [http://localhost:5173/](http://localhost:5173/) in your browser.

---

## 📜 Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Launches the local Vite development server with hot module replacement (HMR). |
| `npm run build` | Type-checks with `tsc` and compiles the production static bundle into `dist/`. |
| `npm run preview` | Runs a local HTTP preview server for the compiled files in `dist/`. |
| `npm run validate-content` | Validates all 14 scene JSON definitions against the narrative flow schema. |
| `npm run test:flow` | Runs simulated end-to-end player path verification checks across all destination scenes. |

---

## 🌐 Deploying to GitHub Pages

The compiled output in `dist/` uses relative paths (`./`) and includes `.nojekyll`, making it ready to host on GitHub Pages:

### Method 1: Deploy from Branch (`/root` or `/docs`)
1. Build the production files:
   ```bash
   npm run build
   ```
2. Push the contents of the `dist/` directory to a branch (e.g. `gh-pages` or the root of a deployment repository).
3. In your GitHub repository:
   - Go to **Settings** → **Pages**.
   - Under **Build and deployment > Source**, select **Deploy from a branch**.
   - Select your deployment branch and `/ (root)`, then click **Save**.

### Method 2: GitHub Actions
If you push the source code to GitHub, configure **Settings > Pages > Source** to **GitHub Actions**, and add `.github/workflows/deploy.yml`:
```yaml
name: Deploy Cosmic Saga to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

---

## 📁 Project Structure

```text
cosmic-saga/
├── public/                 # Static public assets (audio, media, fonts, images)
│   ├── audio/kid/          # Recorded character voiceover clips
│   ├── media/              # NASA mission photos, archival videos, and diagrams
│   ├── images/             # Surface illustrations & logos
│   └── fonts/              # Custom CosmicTech typography
├── src/
│   ├── components/         # React UI modules (Cockpit, AstroPad, EVA, DialogueBox, etc.)
│   ├── content/
│   │   ├── scenes/         # JSON-driven mission scripts & node flows
│   │   ├── flow.ts         # Global story graph & progression rules
│   │   └── nasaMediaCatalog.ts # Mission media metadata & NASA citations
│   ├── engine/
│   │   ├── storyState.tsx  # React Context store & reducer
│   │   ├── soundEffects.ts # Web Audio API procedural synthesizers
│   │   ├── useSpeech.ts    # TTS narration & neural clip playback
│   │   └── persistence.ts  # LocalStorage save-state manager
│   ├── styles/             # Modular CSS design system & CRT animations
│   ├── types.ts            # TypeScript interface definitions
│   └── main.tsx            # Application entrypoint
├── scripts/                # Validation & simulation test suites
├── dist/                   # Compiled production static output
├── index.html              # HTML shell
├── package.json
└── vite.config.ts
```

---

## 👥 Project Team & Contributors

| Role / Responsibility | Team Member(s) |
|---|---|
| **Coordination & Management** | Md Tayebur Rahim |
| **Project Supervision** | Md Tayebur Rahim |
| **Inspiration & Structuring** | Md Tayebur Rahim, Zeba Anika, Tahsin Tabrij Nadeed |
| **Story Writing** | Tahsin Tabrij Nadeed |
| **Dialogues & Interaction Design** | Tahsin Tabrij Nadeed |
| **Character Design** | Tahsin Tabrij Nadeed |
| **Core Research & Analysis** | Tahsin Tabrij Nadeed, Zeba Anika, Hossen Farsan Supto |
| **Data Analysis** | Zeba Anika |
| **Frontend Development** | Mahbubur Rahman Ridoy, Hossen Farsan Supto |
| **Backend Development** | Hossen Farsan Supto, Mahbubur Rahman Ridoy |
| **UI/UX Design** | Hossen Farsan Supto, Mahbubur Rahman Ridoy, Tahsin Tabrij Nadeed |
| **AI Content Generation & Filtering** | Zeba Anika, Hossen Farsan Supto |
| **Voiceover & Additional Graphics** | AI Generated |

---

## 📚 Credits & Attributions

- **Historical Mission Data & Media**: Curated from public-domain NASA and JPL archives (Apollo, Viking, Mars Pathfinder, Phoenix, Pioneer, and Voyager programs).
- **Tribute**: Dedicated to **Félicette**, the pioneering French space cat launched in 1963 aboard the Véronique AGI 47 sounding rocket.
- **Engine Design**: Interactive educational adventure game engine powered by React and Vite.

---

## 📖 References & Data Sources

The following research and scientific literature directly informed the mission data, telemetry parameters, and historical storytelling scripts.

### 1. Lunar Laser Ranging Retroreflector

#### NASA Sources
- [The Apollo Experiment That Keeps on Giving – NASA](https://www.nasa.gov/missions/apollo/apollo-11/the-apollo-experiment-that-keeps-on-giving/)
- [Apollo 11 Retroreflector – International Laser Ranging Service](https://ilrs.cddis.eosdis.nasa.gov/missions/satellite_missions/current_missions/ap11_reflector.html)
- [Lunar Laser Ranging Retroreflector Technical Document](https://www.nasa.gov/wp-content/uploads/static/history/alsj/LRRR-94-0193.pdf)
- [Laser Beams Reflected Between Earth and Moon Boost Science – NASA](https://www.nasa.gov/missions/laser-beams-reflected-between-earth-and-moon-boost-science/)
- [NASA SP-289 – Lunar Science and Exploration](https://www.lpi.usra.edu/lunar/documents/NASA%20SP%20289.pdf)

---

### 2. Apollo Lunar Surface Experiments Package (ALSEP)

#### NASA Sources
- [50 Years Ago: First Apollo Lunar Surface Experiment Package Accepted – NASA](https://www.nasa.gov/history/50-years-ago-first-apollo-lunar-surface-experiment-package-accepted/)
- [Apollo Program History – NASA SP-4009, Volume 4](https://www.nasa.gov/wp-content/uploads/2023/03/sp-4009vol4.pdf)
- [NASA Technical Reports Server – ALSEP Research](https://ntrs.nasa.gov/citations/20180008613)

#### External Sources
- [ALSEP Overview – Lunar and Planetary Institute](https://www.lpi.usra.edu/lunar/ALSEP/)
- [ALSEP Technical Document – Final Summary, Revision B](https://www.lpi.usra.edu/lunar/ALSEP/pdf/FSFM_RevB.pdf)

---

### 3. Viking 1 & Viking 2

#### NASA Sources
- [Viking Mission Overview – NASA](https://science.nasa.gov/mission/viking/)
- [Viking Spacecraft and Science – NASA](https://science.nasa.gov/mission/viking/spacecraft-and-science/)
- [Viking 1 Spacecraft Information – NASA PDS](https://pds.nasa.gov/ds-view/pds/viewContext.jsp?identifier=urn%3Anasa%3Apds%3Acontext%3Ainstrument_host%3Aspacecraft.vl1&version=1.2)
- [Viking Mission – NASA National Space Science Data Center](https://nssdc.gsfc.nasa.gov/planetary/viking.html)
- [NASA Technical Report – Viking Research](https://ntrs.nasa.gov/api/citations/20020052429/downloads/20020052429.pdf)

#### External Sources
- [Scientific Research Paper – AGU Publications](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1002/2017ea000306)

---

### 4. Sojourner Rover & APXS

#### NASA Sources
- [Sojourner's APXS at Work – NASA](https://science.nasa.gov/resource/sojourners-apxs-at-work/)
- [Sojourner's APXS Wedge – NASA](https://science.nasa.gov/resource/sojourners-apxs-wedge/)

---

### 5. Phoenix Mars Lander (TEGA, MECA & MET)

#### NASA Sources
- [Phoenix Mission Overview – NASA](https://science.nasa.gov/mission/mars-phoenix/)
- [Phoenix Meteorological Station (MET) Data Archive – NASA PDS](https://pds-atmospheres.nmsu.edu/data_and_services/atmospheres_data/phoenix/met.html)
- [MET Instrument Information – NASA PDS](https://pds.nasa.gov/ds-view/pds/viewContext.jsp?identifier=urn%3Anasa%3Apds%3Acontext%3Ainstrument%3Amet.phx&version=1.2)
- [Telltale Instrument Information – NASA PDS](https://pds.nasa.gov/ds-view/pds/viewContext.jsp?identifier=urn%3Anasa%3Apds%3Acontext%3Ainstrument%3Att.phx&version=1.0)
- [TEGA Instrument Information – NASA PDS](https://pds.nasa.gov/ds-view/pds/viewContext.jsp?identifier=urn%3Anasa%3Apds%3Acontext%3Ainstrument%3Atega.phx)

#### External Sources
- [Davy et al. (2010) – Temperature Measurements](https://doi.org/10.1029/2009JE003444)
- [Taylor et al. (2010) – Pressure Measurements and Seasonal Variations](https://doi.org/10.1029/2009JE003422)
- [Holstein-Rathlou et al. (2010) – Wind Observations](https://doi.org/10.1029/2009JE003411)
- [Taylor et al. (2008) – Temperature, Pressure, and Wind Instrumentation in the Phoenix Meteorological Package](https://doi.org/10.1029/2007JE003015)

---

### 6. Voyager 1 & Voyager 2

#### NASA Sources
- [Voyager Mission Overview – NASA](https://science.nasa.gov/mission/voyager/)
- [Voyager Mission – NASA/JPL](https://voyager.jpl.nasa.gov/)
- [Voyager Spacecraft Instruments – NASA/JPL](https://voyager.jpl.nasa.gov/mission/spacecraft/instruments/)
- [Voyager: The Interstellar Mission – NASA](https://voyager.gsfc.nasa.gov/)
- [Voyager Mission History – NASA SP-4219](https://history.nasa.gov/SP-4219/Contents.html)
- [Voyager Mission Design and Performance – JPL DESCANSO](https://descanso.jpl.nasa.gov/DPSummary/Descanso4--Voyager_new.pdf)
- [NASA Planetary Data System](https://pds.nasa.gov/)
- [NASA Voyager Mission Blog](https://science.nasa.gov/blogs/voyager/)
- [Voyager 1 Fires Up Thrusters After 37 Years – NASA/JPL](https://www.jpl.nasa.gov/news/voyager-1-fires-up-thrusters-after-37-years/)

#### External Sources
- [Science Journal – Research Paper (Interstellar Plasma Wave Density)](https://www.science.org/doi/10.1126/science.1236408)
- [Science Journal – Research Paper (Magnetic Field at the Heliopause)](https://www.science.org/doi/10.1126/science.1241681)
- [Voyager Plasma Wave Research – University of Iowa](https://space.physics.uiowa.edu/voyager/)
- [Sounds of Earth – United Nations Golden Record](https://www.un.org/ungifts/golden-record-sounds-earth)

---

### 7. Pioneer 10 & Pioneer 11

#### NASA Sources
- [Pioneer 10 Mission Overview – NASA](https://science.nasa.gov/mission/pioneer-10/)
- [Pioneer 11 Mission Overview – NASA](https://science.nasa.gov/mission/pioneer-11/)
- [Pioneer Program – NASA](https://www.nasa.gov/pioneer/)
- [Pioneer Mission History – NASA SP-349](https://history.nasa.gov/SP-349/sp349.htm)
- [Pioneer Mission History – Chapter 3](https://history.nasa.gov/SP-349/ch3.htm)
- [Pioneer Mission History – Chapter 4](https://history.nasa.gov/SP-349/ch4.htm)
- [Pioneer Mission History – Chapter 6](https://history.nasa.gov/SP-349/ch6.htm)
- [Pioneer Flyby Data – NASA PDS Atmospheres Node](https://pds-atmospheres.nmsu.edu/data_and_services/atmospheres_data/PIONEER/pioneer_flyby.html)
- [NASA Technical Report – Pioneer 10 Research](https://ntrs.nasa.gov/citations/19760020178)
- [NASA Technical Report – Pioneer 11 Research](https://ntrs.nasa.gov/citations/19810002589)
- [NASA Radioisotope Power Systems](https://rps.nasa.gov/)
- [NASA Planetary Plasma Interactions Node – PDS](https://pds-ppi.igpp.ucla.edu/)

#### External Sources
- [Pioneer Anomaly Research – Physical Review Letters](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.108.241101)
- [Pioneer 10/11 Backup Spacecraft – Smithsonian National Air and Space Museum](https://airandspace.si.edu/collection-objects/pioneer-10-11-backup-spacecraft/nasm_A19770260000)

---

## 📄 License

This project is created for educational and interactive storytelling purposes. Mission imagery, transcripts, and telemetry diagrams are adapted from public NASA science data.
