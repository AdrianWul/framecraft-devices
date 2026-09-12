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
- Visible render progress during WebM video capture.
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
