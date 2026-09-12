# Framecraft Devices

Versioned 3D device assets used by Framecraft.

## Public asset URLs

GitHub Pages base URL:

`https://adrianwul.github.io/framecraft-devices/`

Each device is stored under `devices/<device-id>/`. The library metadata is
available in [`manifest.json`](./manifest.json).

## Adding a device

1. Add the source glTF package locally.
2. Optimize it to `devices/<device-id>/scene.glb` and keep the original
   `license.txt` beside it. GLB keeps geometry and textures in one web-ready file.
3. Add the device metadata and screen material name to `manifest.json`.
4. Preserve the required attribution and confirm that the license permits the
   intended use.

## Licensing

Every device retains its original `license.txt`. The iPad Pro and iPhone Duo
assets are licensed for non-commercial use only. See the individual folders
and `manifest.json` before publishing or monetizing a project that uses them.
