# IGNITE Summit VR Exhibit

An immersive WebXR virtual reality tour of the CAPS Building, designed for the IGNITE Summit. Built with [A-Frame](https://aframe.io/) and deployable via any static host — no server required.

**🌐 Live Demo:** [https://sohamshekhar123.github.io/ignite-summit-vr](https://sohamshekhar123.github.io/ignite-summit-vr)

---

## Features

- 🎯 **Point-of-Interest (POI) system** – glowing markers with info panels and narration audio
- 🕹️ **Desktop** – WASD movement + mouse look + click markers
- 📱 **Mobile** – touch to look around, tap markers to activate, gaze fuse cursor
- 🥽 **VR Headset (Quest etc.)** – teleport locomotion via trigger buttons
- ⚡ **Performance-aware** – mobile auto-disables antialiasing, capped texture size

---

## Adding the building scan

Replace the placeholder with your photogrammetry or scanned model:

1. Export your scan as a **GLB file** (binary GLTF)
2. Drop it into `assets/` and name it exactly **`model.glb`**
3. Commit and push — GitHub Pages will update automatically

> **Tip:** Keep the GLB under ~50 MB for fast mobile loading. Use [gltf-transform](https://gltf-transform.donmccurdy.com/) to optimize geometry and textures.

---

## Adding narration audio

1. Record or generate MP3 narration files for each POI
2. Drop them into `assets/audio/` following this naming convention:

| File | POI |
|------|-----|
| `poi-1.mp3` | Main Entrance |
| `poi-2.mp3` | Innovation Lab |
| `poi-3.mp3` | Collaboration Space |
| `poi-4.mp3` | Studio |
| `poi-N.mp3` | Any new POI you add |

3. Commit and push — no code changes needed for existing POIs

> **Audio format:** MP3 is universally supported across all browsers and headsets.

---

## Adding new POIs

Open `index.html` and add a new entity inside the `<a-scene>` block:

```html
<a-entity
  id="poi-5"
  poi-marker="
    title: Workshop Room;
    description: Hands-on fabrication and prototyping space.;
    audio: audio-poi-5;
    color: #2ecc71"
  position="3 1.5 -8">
</a-entity>
```

Then add the corresponding audio element inside `<a-assets>`:

```html
<audio id="audio-poi-5" src="assets/audio/poi-5.mp3" preload="none" crossorigin="anonymous"></audio>
```

And drop your `poi-5.mp3` file into `assets/audio/`.

### POI marker schema reference

| Property | Type | Description |
|----------|------|-------------|
| `title` | string | Heading shown in the info panel |
| `description` | string | Body text shown in the info panel |
| `audio` | string | ID of the `<audio>` element in `<a-assets>` |
| `color` | color | Accent color of the glowing sphere |

---

## File structure

```
ignite-summit-vr/
├── index.html          ← Complete single-file WebXR app
├── assets/
│   ├── model.glb       ← Drop your building scan here
│   └── audio/
│       ├── poi-1.mp3   ← Narration for each POI
│       ├── poi-2.mp3
│       ├── poi-3.mp3
│       └── poi-4.mp3
└── README.md
```

---

## Local development

No build step needed — just serve the folder:

```bash
# Using Python (built-in)
python3 -m http.server 8080

# Using Node
npx serve .
```

Then open [http://localhost:8080](http://localhost:8080).

---

## Tech stack

| Library | Version | Purpose |
|---------|---------|---------|
| [A-Frame](https://aframe.io/) | 1.5.0 | WebXR / 3D scene |
| [aframe-extras](https://github.com/c-frame/aframe-extras) | 7.2.0 | Locomotion & movement controls |

---

## License

MIT © IGNITE Summit
