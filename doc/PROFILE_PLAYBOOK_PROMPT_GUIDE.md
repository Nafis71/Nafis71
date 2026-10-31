# The Profile Playbook: Animated GitHub Profile Specification & Agent Prompt Guide

> **Instructions for the AI Agent:**
> You are acting as an expert creative front-end engineer and SVG designer. When given this document alongside a user's details and photos, your task is to design, generate, and deliver a production-ready, modular, animated GitHub profile README matching the high-fidelity cyberpunk/developer aesthetic described below.
> 
> Strictly adhere to all rules, SVG safety constraints, motion timings, and package verification procedures.

---

## 1. Quick Master Input Template (Fill Before Running)

Replace every placeholder inside brackets `[...]` before asking the agent to generate your profile:

```text
[USER_DETAILS]
Name: [FULL NAME]
GitHub Username: [USERNAME]
Role / Company: [CURRENT ROLE @ COMPANY] (Specify On-site, Hybrid, or Remote)
Location: [CITY, COUNTRY]
Elevator Pitch: [1-2 SENTENCES DESCRIBING CORE ENGINEERING PHILOSOPHY]
Cycling Roles (Hero): [ROLE 1] | [ROLE 2] | [ROLE 3] | [ROLE 4]
Core Engineering Capabilities:
  - 1: [TITLE] -> [1 SENTENCE DESCRIPTION]
  - 2: [TITLE] -> [1 SENTENCE DESCRIPTION]
  - 3: [TITLE] -> [1 SENTENCE DESCRIPTION]
Tech Ecosystem (Orbits & Chips):
  - Primary Core (Center): [MAIN TECH, e.g. Flutter / React / Go / Rust]
  - Orbiting Techs: [4-6 TECHNOLOGIES, e.g. Dart, Bloc, Riverpod, Postgres, Redis]
  - Categorized Stack Chips:
      * Languages: [LIST]
      * State / Architecture: [LIST]
      * Backend & Persistence: [LIST]
      * Dev Tools / AI: [LIST]
Lifestyle & Passions Carousel (3 Slides):
  - Slide 1: [TAG, e.g. 01 / CRAFT] | [TITLE] | [3 LINES OF TEXT] | [FOOTER NOTE]
  - Slide 2: [TAG, e.g. 02 / HABIT] | [TITLE] | [3 LINES OF TEXT] | [FOOTER NOTE]
  - Slide 3: [TAG, e.g. 03 / AI ACCEL] | [TITLE] | [3 LINES OF TEXT] | [FOOTER NOTE]
Verified ID & Telemetry (4 Dashboard Cards):
  - Card 1: [TITLE] -> [VALUE] -> [SUBTEXT]
  - Card 2: [TITLE] -> [VALUE] -> [SUBTEXT]
  - Card 3: [TITLE] -> [VALUE] -> [SUBTEXT]
  - Card 4: [TITLE] -> [VALUE] -> [SUBTEXT]
Social Links:
  - LinkedIn: [URL]
  - GitHub: [URL]
  - LeetCode / Portfolio / Twitter: [URL]
  - Other: [URL]
Character Photo: [ATTACH A CLEAR USER PHOTO]
```

---

## 2. Art Direction & Theme Specification

Every generated asset must adhere to this cohesive palette:

| Element | Hex Color | Role / Description |
| :--- | :--- | :--- |
| **Deep Background** | `#070b16` to `#0a1020` | Dark cyber-navy gradient backdrop |
| **Electric Accent** | `#247bff` | Primary focus, borders, active nodes, neon glow |
| **Crimson Accent** | `#ff354f` | Secondary highlight, badges, alert dots, contrast rim |
| **Cyan Glow** | `#00e5ff` | Tertiary highlight, fast progress tracks, special chips |
| **Off-White Text** | `#f8fafc` / `#e2e8f0` | High-contrast display typography |
| **Muted Text** | `#8b9bb4` / `#64748b` | Subtitles, secondary telemetry, monospace logs |

---

## 3. Step 1: Character Asset Generation

The system requires two transparent PNG images (`assets/id.png` and `assets/right_pointing.png`).

### Prompt 1: The Stylized Portrait (`assets/id.png`)
```text
Transform my attached photo into a premium semi-realistic illustrated bust portrait of this person. Preserve recognizable facial features, hairstyle, facial hair/glasses, and skin tone. Give a confident, approachable expression dressed in stylish dark streetwear, with subtle electric-blue (#247bff) and crimson (#ff354f) rim light. Frame from the chest up with the full head visible. Use a genuinely transparent background with pure alpha (PNG), not a drawn checkerboard or solid backdrop. No badges, logos, or extra text. Export high-resolution PNG.
```

### Prompt 2: The Right-Pointing Character (`assets/right_pointing.png`)
```text
Using the stylized portrait as the identity reference, create the same person in the same streetwear outfit, shown from the waist up, positioned on the left side and pointing toward the viewer's RIGHT with a natural, confident hand pose. Leave ample breathing room around the head and pointing hand (no cropping). Match hair, face, and electric-blue/crimson rim lighting. Use a genuinely transparent alpha background (PNG), no solid backdrop, no checkerboard pattern. No text, logos, or extra badges. Export high-resolution PNG.
```

> [!CAUTION]
> **Check Alpha Transparency:** If the AI generator bakes in gray/white checkerboard squares, you must run background thresholding / edge cutout to ensure pure alpha (`A = 0`) before embedding.

---

## 4. Step 2: GitHub-Safe SVG Construction Rules

GitHub's image proxy (`camo.githubusercontent.com`) strictly sanitizes SVGs. You **MUST** follow these rules:

1. ❌ **NO `<foreignObject>`** (GitHub strips this entirely).
2. ❌ **NO JavaScript / `<script>`** tags or inline event handlers.
3. ❌ **NO External Network Fetches** (Do not link external web fonts, images, or stylesheets; they will be blocked).
4. ✅ **Embedded Base64:** Embed `id.png` and `right_pointing.png` as inline Base64 `data:image/png;base64,...` inside `<image href="...">`.
5. ✅ **CSS + SMIL Only:** Animations must be implemented via pure CSS `@keyframes` and/or native SMIL `<animate>` tags.
6. ✅ **Namespaced IDs:** Give all gradient and filter IDs unique names to avoid cross-SVG collisions when rendered together.

---

## 5. The 5 Core SVG Components to Generate

Save each SVG in the `assets/` folder:

### 1. `assets/hero.svg` (ViewBox: 850x360)
- **Top Pill:** Glowing green pulse status (e.g. `STATUS: AVAILABLE`).
- **Display Title:** Name reveal with rising mask transition.
- **Role Cycler:** Terminal typing cursor (`> `) cycling through 4 roles using CSS/SMIL opacity intervals.
- **Pitch:** 2-line developer philosophy and value proposition.
- **Metadata Badges:** Company tag with briefcase icon + Location tag with pin icon.
- **ID Card Frame:** Embedded `id.png` avatar on the right with cyber-gradient borders.

### 2. `assets/about-life.svg` (ViewBox: 850x360)
- **Left Panel (Capabilities):** 3 core architecture items with checkmarks and descriptive text.
- **Right Panel (Carousel):** 3 rotating slides changing every 4 seconds (12s total loop).
- **Synchronized Progress Tracks:** 3 segmented horizontal progress bars above the carousel filling in sync with each active slide.
- **Clean Layout:** Ensure slides are positioned below the progress tracks to prevent text overlap.

### 3. `assets/stack.svg` (ViewBox: 850x420)
- **Central Core:** Pulsing hub featuring the primary tech stack icon/logo.
- **Planetary Orbits:** 3 tilted dashed elliptical rings rotating with different speeds and directions (`rot1`, `rot2`, `rot3`).
- **Counter-Rotation:** Every orbiting planet node must have an inverse counter-rotation (`crot`) so text/icons remain perfectly upright at all times.
- **Categorized Stack Chips:** Neatly aligned chip columns on the right (Languages, Architecture, Backend/DB, AI/Tools).

### 4. `assets/id-dashboard.svg` (ViewBox: 850x480)
- **Physics Pendulum Lanyard:** Hanging badge with strap and metallic clasp. Uses damped pendulum keyframe timing (drops into place, settles, then maintains a continuous subtle `+/-1.7°` harmonic sway).
- **Holographic Light Sweep:** Diagonal linear gradient beam sweeping across the badge.
- **ID Details:** Avatar, name, handle, role, and simulated high-res barcode.
- **Telemetry Grid:** 4 structured metric cards showing core stack, architecture philosophy, databases, and problem-solving stats.

### 5. `assets/connect.svg` (ViewBox: 850x420)
- **Pointing Character:** Embedded `right_pointing.png` on the left pointing directly toward the right column.
- **Social Connect Cards:** 4 generously spaced cards (LinkedIn, GitHub, LeetCode, etc.) with brand icons and nudging arrow animations.
- **Embedded Links:** Wrap each card group in SVG `<a href="..." target="_blank">` tags for direct clickable redirects.

---

## 6. Step 3: Root `README.md` Assembly

Wire all generated SVGs in the repository root `README.md`:

```markdown
# ⚡ [NAME] (@[USERNAME])

<div align="center">

![Intro](./assets/hero.svg?v=1)

![About](./assets/about-life.svg?v=1)

![Stack](./assets/stack.svg?v=1)

![ID](./assets/id-dashboard.svg?v=1)

![Connect](./assets/connect.svg?v=1)

</div>

---

### 🌐 Direct Channels & Social Links

*Note: Since links inside SVG images can be blocked by GitHub's image proxy, click below to open directly:*

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-[NAME]-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)]([LINKEDIN_URL])
[![GitHub](https://img.shields.io/badge/GitHub-[USERNAME]-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/[USERNAME])
[![Portfolio](https://img.shields.io/badge/Portfolio-[NAME]-FFA116?style=for-the-badge&logo=codepen&logoColor=white)]([PORTFOLIO_URL])

</div>

---

### 💼 Engineering Background & Highlights

- 🏢 **Current Role:** [ROLE] @ **[COMPANY]** ([LOCATION_TYPE])
- 🎯 **Primary Focus:** [CORE_SPECIALTY]
- ⚡ **State Management / Architecture:** [FRAMEWORKS & ARCHITECTURE]
- 🌐 **Web & Backend:** [FULLSTACK_STACK]
- 🗄️ **Databases & Caching:** [DATABASES]
- 🤖 **AI Acceleration:** [PROMPT_ENGINEERING_DETAILS]
```

---

## 7. Step 4: Verification & Delivery Checklist

Before handing the profile to the user:

1. **Light / Dark Mode Check:** Open `preview.html` and verify the SVGs look contrast-rich on both pure black (`#0d1117`) and pure white (`#ffffff`) backgrounds.
2. **Cache-Busting:** Ensure all image links in `README.md` end with `?v=1`. (If updating later, bump to `?v=2`).
3. **Packaging:** Create `preview.html` for local visual testing and optionally pack `profile-package.zip` containing `README.md` and `assets/`.
4. **Git Push:** Stage and commit:
   ```bash
   git add README.md assets preview.html
   git commit -m "feat: launch Profile Playbook animated GitHub profile"
   git push origin main
   ```
