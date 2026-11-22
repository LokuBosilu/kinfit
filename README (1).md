# Kinfit landing page

Marketing landing page for **Kinfit**, a phone-camera movement checker and coaching aid that corrects exercise form during a set, stops the set when movement looks unsafe, and sends a trainer only the moments that need a look.

This is the Coursework 1 deliverable **B8 (landing page marketing website)** for the Agile Team Project, **Group CS 60**, Informatics Institute of Technology (IIT), University of Westminster.

> Kinfit is an exercise movement checker and coaching aid. It is **not** a medical or diagnostic device. The site shows a design prototype and concept animation, not the working app.

- Live site: _add the URL after deploying_
- Repository: https://github.com/LokuBosilu/Kinfit
- Contact: kinfit.team@gmail.com

---

## 1. What is in this folder

```
.
├── index.html              The whole page: markup, styles and scripts in one file
├── favicon.ico             Browser tab icon (16, 32 and 48 px)
├── site.webmanifest        Name, icons and theme colour for "Add to Home screen"
├── README.md               This file
└── assets/
    ├── three.min.js            Three.js r128, the 3D library used by the hero (self-hosted)
    ├── kinfit-logo-light.png   Full logo for dark backgrounds (nav bar, loader, footer)
    ├── kinfit-logo.png         Full logo in full colour, for light backgrounds and documents
    ├── kinfit-mark-light.png   K symbol only, for dark backgrounds
    ├── kinfit-mark.png         K symbol only, full colour
    ├── favicon-16x16.png       Small tab icon
    ├── favicon-32x32.png       Tab icon
    ├── apple-touch-icon.png    iPhone home-screen icon (180 px)
    ├── android-chrome-192x192.png   Android home-screen icon
    ├── android-chrome-512x512.png   Android icon, large
    └── og-image.png            1200x630 preview image for link sharing
```

`index.html` must stay next to the `assets` folder. It loads the logos, icons and the 3D script from there, so deploying `index.html` on its own breaks the logo and the hero animation.

### Files that are not part of the website

If these are in your working folder, do not deploy them:

| File | What it is |
|---|---|
| `kinfit-landing-3d-hero.html` | An earlier version of the page, replaced by `index.html` |
| `kinfit-landing-structure.html` | The first text-only draft of the page copy |
| `DitherReveal.tsx` | An unused hero background component |
| `Kinfit_Landing_Page_Copy.docx` | The page copy as a Word document, with notes on what was changed |
| `kinfit-flow-video-prompts.md` and `flow-references/` | Prompts and reference images for making the demo video in Google Flow |

---

## 2. Page structure (`index.html`)

Sections appear in this order. Each has an `id`, which the navigation links point to.

| Order | Section | `id` | What it holds |
|---|---|---|---|
| 0 | Loading screen | `kf-loader` | Branded screen shown while the page loads |
| 1 | Navigation | | Logo, section links, "Join the Waitlist" button, mobile menu |
| 2 | **Hero** | `hero` | Badge, headline, sub heading, two buttons, trust line and the 3D concept animation |
| 3 | Demo | `demo` | The video walkthrough (a YouTube embed) and three step cards |
| 4 | Join the waitlist | `waitlist` | Sign-up form and privacy notice |
| 5 | Scenarios | `scenarios` | Three illustrative situations (Dilani, Nimal, the trainer) and a trainer quote |
| 6 | How it works | `how-it-works` | Three features, each with an illustration |
| 7 | Modes | `modes` | Mode A (active gym member) and Mode B (supervised exercise) |
| 8 | Where Kinfit fits | `where-we-fit` | Comparison with existing product types |
| 9 | Pilot | `pilot` | What the pilot will measure |
| 10 | FAQ | `faq` | Six questions as accordions |
| 11 | Closing call to action | `closing-cta` | Second waitlist button |
| 12 | Team | `team` | Five team members and roles |
| 13 | References | `references` | Harvard-style sources |
| 14 | Footer | | Non-medical disclaimer, contact links, copyright |

---

## 3. How the main parts work

### Hero and the 3D animation
- A 3D stick-figure skeleton does a squat in a loop of about 9 seconds, drawn with **Three.js** on a canvas.
- On even loops the knees cave inward, the joints turn amber and a "Knees out!" cue appears. The knees are corrected, then a "flagged moment queued" message shows and the **Flagged** counter goes up. On odd loops the rep is clean ("Good form").
- The pointer moves the camera slightly. The animation pauses when the hero is off screen.
- **Fallbacks, in order:** if WebGL is unavailable, the same animation is drawn in 2D on the canvas. If Three.js fails to load, the animation panel hides and the text remains. With "reduce motion" switched on, one still frame is shown instead of a loop.
- The caption under it says "Concept animation, not footage of the working app." Keep that caption.
- The script is `assets/three.min.js`. If the animation is missing, open the browser console (F12), where the page logs the cause.

### Loading screen
- Navy full-screen overlay with the logo, soft rings and a progress bar.
- It leaves when the page has parsed and the nav logo has loaded, after at least about one second. It does not wait for the YouTube embed. A 6 second limit and a separate 8 second timer guarantee it never gets stuck.
- Scrolling is locked only while it shows. With JavaScript off it never appears.

### Waitlist form
- Fields: full name, email, and "I am a…" (personal trainer, gym member, someone exercising under a doctor's or trainer's advice, clinician or physiotherapist).
- On submit, the page sends the three fields as JSON to a **Google Apps Script web app**. The page's code comments say this script writes the entries to a Google Sheet, but the script itself is not in this repository, so keep a copy of it somewhere your team can find it. The page shows a success or error message under the form.
- **Known limitation:** the request uses `no-cors` mode, so the browser cannot read the server's reply. The success message appears even if the script rejected the data. After every change to the script, submit a test entry and check the sheet.

### Other behaviour
- **Navigation:** turns into dark glass when you scroll, underlines the current section, and the mobile menu closes after you pick a link.
- **Scroll reveal:** sections fade in as they enter the screen.
- **FAQ and references:** open and close without any library.
- **Responsive:** tested from a 320 px phone to a 3440 px monitor, upright and sideways. Wide tables stack into cards on small screens.
- **Accessibility:** skip link, proper heading order, labelled form fields, visible focus outlines, alt text on logos, reduced-motion support, decorative effects hidden from screen readers.
- **SEO and sharing:** page title, meta description, favicon set, Open Graph and Twitter card tags, web manifest.

---

## 4. Run it on your computer

1. Keep `index.html` and the `assets` folder together.
2. Double-click `index.html`, or serve the folder (recommended):
   ```bash
   python -m http.server 8000
   ```
   then open http://localhost:8000.

No install or build step is needed. The page uses no framework and no package manager.

## 5. Deploy on Vercel

1. Put the contents of this folder in the GitHub repository (`index.html` at the top level).
2. In Vercel, choose **Add New, Project** and import the repository.
3. Framework preset: **Other**. Leave the build command and output directory empty. It is a static site.
4. Deploy. Vercel serves it over HTTPS automatically.
5. Add your own `.lk` or `.com` domain under the project's **Domains** settings (B8 requires your own domain).
6. Open the live link on a phone and check the hero, the form and the video.

---

## 6. How to change things

| To change | Where |
|---|---|
| Any text | Edit it in `index.html`. Each section is marked with a comment block |
| Colours | The `:root { … }` block at the top of the `<style>` tag (`--navy-*`, `--blue`, `--green`, `--amber`) |
| Logo | Replace the files in `assets/` and keep the same names |
| Demo video | Change the `src` of the iframe with class `proto-embed` in the `demo` section |
| Waitlist destination | The `action` of the form `waitlist-form` |
| Team members | The `team-grid` list in the `team` section |
| Sources | The `references` section and the in-text citations in `scenarios` |

---

## 7. Outside services the site uses

The privacy notice must match this list.

| Service | Used for | When it receives data |
|---|---|---|
| Google (Apps Script and Google Sheets) | Stores waitlist sign-ups | When someone submits the form |
| YouTube | The demo video embed | When the page loads |
| Vercel | Hosting | Every visit (standard server logs) |
| GitHub | Hosts the source code | Not involved when visitors browse |

Three.js is hosted with the site, and the page uses system fonts, so no other outside service is contacted.

---

## 8. Known issues and to-do

- [ ] The privacy notice names "Google Forms and Vercel". The form actually uses a Google Apps Script and Google Sheet, and the page loads a YouTube embed. Update the notice so it names what is really used.
- [ ] Consider changing the embed address from `youtube.com` to `youtube-nocookie.com` and adding `loading="lazy"` to the iframe, so the page loads faster and sets fewer tracking cookies.
- [ ] Once the domain is live, make the `og:image` address absolute (`https://YOURDOMAIN/assets/og-image.png`) and add `og:url`. Social sites need the full address to show the preview.
- [ ] Replace the drawn illustrations in "How it works" with real screenshots from the Figma prototype, using the alt text in the HTML comments above each one.
- [ ] Make sure the caption under the demo video says it is a concept walkthrough, not the working app.
- [ ] Check the live site on a real phone (Chrome and Safari), upright and sideways.

---

## 9. Credits and licences

- 3D animation: [Three.js](https://threejs.org/) r128, MIT licence. Keep the licence header at the top of `assets/three.min.js`.
- Logo, icons and copy: Team CS 60.
- Research sources are listed in the page's References section.

© 2026 Kinfit (ATP Group CS 60, Informatics Institute of Technology). All rights reserved.
