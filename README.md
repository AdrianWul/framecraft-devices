# Framecraft

Browser-based 3D device animation editor built with React, Three.js, and Vite.

Created by **Adrian Wulfrath**  
Special thanks to **Jordan Jimenez**

## Features

- Real-time 3D device composition and camera controls.
- Image and video playback on device screens.
- Independent screen flip, rotation, fit, and scale adjustments.
- Camera, lighting, transform, and depth-of-field animation.
- Camera Rotate X control from -85° to 85° for dramatic but stable overhead and underside angles.
- Movable and resizable timeline clips with an expandable Transform track for
  individually selectable and retimeable property keyframes.
- Per-transition easing presets and soft, easy-release center snapping guides for camera positioning.
- Responsive controls with a categorized, animated mobile workspace that keeps the canvas visible.
- Seven-step interactive tutorial covering setup, media, mockups, timeline animation, and export.
- Pink-to-magenta animated stroke treatment on the Tutorial button.
- Image export plus WebM video export at 30 FPS, with 60 FPS enabled only for detected 60 FPS sources.
- Frame-by-frame WebM rendering with fixed timestamps, completed-frame progress, and cancellation.
- Coalesced, precise paused-video scrubbing and new-frame-only screen texture updates.
- Independent shot scenes and local keyframes, with real cuts and crossfades in preview and export.
- Desktop inspector accordions; unchanged mobile category navigation.
- Compact linked/independent screen scaling, individual slider resets, and per-section Reset All.
- One shared WebGL renderer across shots, with context-loss notification and preview recovery.
- Geometry-aware iPhone Duo screen fitting and isolated device housing finish materials.
- Portable `.framecraft.json` project save files with embedded media.

## Using the editor

1. Select a device from the Mockup section.
2. Load a PNG, JPG, WebP, MP4, or WebM file.
3. Adjust the screen orientation with Flip H, Flip V, Rotate, and Screen Scale.
4. Position the camera by dragging the canvas, using Space + drag to pan, and
   scrolling to zoom.
5. Add keyframes from the inspector or the Transform, Camera, Lighting, and
   Depth of field lanes in the timeline. Select Transform to expand its individual
   property keyframes; selecting another track collapses it.
6. Use the save icon to download a `.framecraft.json` project that can be opened
   again later.
7. Use Export to render an image or WebM animation.

### Video playback and export

Video export requires WebCodecs (use current Chrome or Edge over HTTPS or
localhost). Frames are decoded and rendered individually rather than captured
in real time; slower rendering does not skip output timestamps. Progress counts
completed frames, with finalization before download. Cancel render or Escape
restores the paused playhead without downloading a partial file.

Exports remain silent WebM: 30 FPS by default, or 60 FPS for detected 59.94/60 FPS
sources. Both videos must qualify in dual-video compositions. MP4 is import-only.
Paused scrubbing uses the latest requested position without the old 120 ms
threshold; long-GOP source videos may still require decoding time.

### Shots, screen scaling, and resets

Hover a shot card (or swipe left on touch) to reveal its delete button; deletion
requires a click/tap on the trash icon. Hold the shot name for 350 ms to drag it
up/down. Neighboring rows move aside and a dashed line marks the destination.
Release to reorder, or Escape to cancel. With the keyboard, Space lifts the shot,
Up/Down move it, and Enter/Space drops it. Duration is edited separately at the right.

Screen scale can link X/Y (Uniform) or adjust each axis separately (Non-uniform).
Each slider has a reset icon next to its value. Camera, Transform, Appearance,
Lighting, and Depth of field also have Reset All for their sliders.
Animated resets pause playback and add or update a default-value keyframe at the
current shot-local time, preserving other keys and existing easing. Unanimated
controls return to their base defaults without adding keys unless recording.
Reset All leaves the device finish, HDR, focus shape, and other shots unchanged.

Projects now save as version 2 with all shot scenes and embedded media.
Version 1 files are migrated on load. Moving a shot carries its local keyframes;
each outgoing shot's transition button selects a cut or a half-second dissolve
at the next shot's start without shortening either shot.

## Development

```powershell
npm install
npm run dev
```

## Production build

```powershell
npm run build
```

Publish the complete `dist` directory to GitHub Pages, Netlify, Cloudflare
Pages, Vercel, or another static HTTP host. No database or application server
is required.

The production build uses a standalone `index.html` with its JavaScript and CSS
embedded. The ready-to-upload files are also copied to `UPLOAD_TO_WEB`.

## Device library

Framecraft loads its production GLB assets from:

<https://adrianwul.github.io/framecraft-devices/>

Repository:

<https://github.com/AdrianWul/framecraft-devices>

The URL can be replaced at build time:

```powershell
$env:VITE_DEVICE_LIBRARY_URL = 'https://example.com/devices/'
npm run build
```

Each model keeps its original attribution and license in the device repository.
Some included models prohibit commercial use.

### Adding another device

1. Export or optimize the model as a self-contained `scene.glb`.
2. Create `devices/<device-id>/` in the device repository.
3. Add `scene.glb` and the original `license.txt`.
4. Add its URL, screen material name, author, source, and license to
   `manifest.json`.
5. Register the device and its display transform in Framecraft. The screen mesh
   must have an identifiable material so the editor can replace its texture.

## Credits

- Design and development: [Adrian Wulfrath](https://github.com/AdrianWul)
- Special thanks: Jordan Jimenez
- 3D device authors and licenses are credited in the application and in the
  [device library](https://github.com/AdrianWul/framecraft-devices).
