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

Reveal the left gear on a source card to edit its own fit, flip/rotation, and
screen scale. Primary and secondary screens are independent per shot/device;
older shared settings migrate without changing their initial appearance.
Empty screens use the supplied landscape image, embedded in `index.html`.
It respects each screen's Fit/Fill setting and never replaces imported media.

Effects opens in the right inspector; Devices restores the device controls.
Click the toolbar Effects icon again to return to Devices.
Camera keeps Distance and Zoom; FOV is no longer a visible slider. Existing
project FOV values/keyframes are preserved, including by camera slider resets.
Device color is opt-in for new scenes. Its toggle restores original shader colors
when off and remembers the custom selection. Older projects keep their prior colors.
The Mockup picker changes the device for every shot while retaining independent
sources, camera, animation, colors, and effects. Older mixed-device projects ask
before being converted to one device; cancelling leaves the current project intact.
Mockup also includes iPhone 18 Pro Max and MacBook Pro, with bundled GLB assets,
source fitting, video support, and opt-in housing color. MacBook media replaces
only its display, preserving the original keyboard, bezel, and camera notch.
HDR reflections are prepared outside model drawing and kept independent per shot.
Model attributions live in the Model credits link below the inspector.
Keep `device-credits.html` alongside the other site files.
Import media from Source and choose presets through Auto-motion; the duplicate
Media and Presets buttons have been removed.
The grid button beside Effects toggles the resolution badge and movement hints.
Effects contains a card stack with Bloom and Depth of field (moved from
the inspector). Use + to add an effect; each card has enable/disable, removal,
collapse, and reset controls. Removal preserves its values/keyframes for re-adding.
Bloom starts at Strength 0.54, Threshold 0.24, Radius 0.24 and is off until added.

Choose iPhone Duo 2 (marked with a clapperboard) in Mockup to scrub its open-close clip with Animation frame
(0-60). Record keyframes on the Mockup track; easing, resets, trim/reorder,
project save/load, PNG, and WebM retain the same shot-local animation.
Primary edits the inner screen; secondary edits the outer screen.
The bundled `devices` folder must remain alongside `index.html`.

The Fold model is [Apple iPhone Duo Fold Star White 2026 (Animated)](https://sketchfab.com/3d-models/apple-iphone-duo-fold-star-white-2026-animated-240492141edd4594ae13082a7fcbbb29)
by [extraakash](https://sketchfab.com/AakashMansukhani).
On September 12, 2026, the project owner confirmed express author permission
for public GitHub hosting and distribution with this site. The original
Sketchfab Standard metadata is retained; the asset is not generally relicensed.

Trim edges have larger hit targets and animated hover highlights. Crossfade is
inset inside the clip, away from its trim edges, including on short clips.
Select the small icon between keyframes to edit cubic Bezier easing using two draggable
pivots or x1, y1, x2, y2 (0-1, maximum two decimals). Curves are saved per interval
and used in preview/export; older easing is preserved until edited.

NEW UPDATES groups changes into Interface, Control, Canvas, and Timeline sections,
including effects, device colors, and cubic Bezier easing.
It reappears on refresh unless "Don't show again for this update" is
checked. That preference applies only to the current release. The purple/cyan
Updates button beside Tutorial reopens the list at any time.

Hover a shot card (or swipe left on touch) to reveal its delete button; deletion
requires a click/tap on the trash icon. The red SVG animates once per hover entry,
without looping, and respects reduced motion. Hold the shot name for 150 ms to drag it
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
