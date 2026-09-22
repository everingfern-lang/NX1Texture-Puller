A read-only image/texture extractor for NX1 / Call of Duty: Future Warfare FastFiles.
 What it extracts
- Map textures from one map or every map
- Every multiplayer map in one run
- Full-game image textures
- Detected weapon textures
- A strict, categorized `MULTIPLAYER_WEAPONS_BY_GUN` library
- CSV manifests and deduplicated image indexes
The tool does **not** modify the game files.
 Portable drive / folder support
Double-click:
`NX1_ASSET_MENU.bat`
On first launch, choose:
1. Your NX1 game folder — it may be on C:, D:, E:, F:, an external drive, etc.
2. Your output folder — this may be on a different drive.
Those choices are saved locally in `nx1_paths.json`. Use menu options **6** and **7** at any time to switch drives or folders.
The settings file is intentionally not meant to be committed to GitHub because it contains a user's local paths.
 Menu
- `1` Pull every multiplayer map texture
- `2` Pick one multiplayer map
- `3` Pull every map texture
- `4` Pick one map
- `5` Pull the full game and build multiplayer weapon texture libraries
- `6` Switch NX1 game drive/folder
- `7` Switch output drive/folder
- `8` Show current locations
- `9` Open output folder
 Building on Windows
Double-click:
`build_windows_fixed.bat`
The builder:
- uses CMake from PATH if available;
- otherwise locates Visual Studio with Microsoft's `vswhere`;
- uses Visual Studio's actual installation path even when Visual Studio is installed on a non-C: drive;
- locates vcpkg from `VCPKG_ROOT`, Visual Studio, or PATH.
Required Visual Studio components:
- Desktop development with C++
- C++ CMake tools for Windows
- Windows 10/11 SDK
- vcpkg package manager
The project uses zlib through vcpkg.
  Output layout
If your chosen output base is `D:\NX1_Extracted`, outputs look like:
- `D:\NX1_Extracted\NX1_Map_Assets\mp_nx_meteor\...`
- `D:\NX1_Extracted\NX1_Map_Assets\mp_nx_pitstop\...`
- `D:\NX1_Extracted\NX1_Images\MULTIPLAYER_WEAPONS_BY_GUN\AK47\...`
- `D:\NX1_Extracted\NX1_Images\multiplayer_weapon_textures_by_gun.csv`
 GitHub
This package is designed to be shared as source. Do not commit:
- `build-win/`
- `nx1_paths.json`
- extracted DDS/image output
- local game files
No NX1 game files are included in this repository/package
  v0.6.0 weapon filtering
Weapon extraction is now deliberately strict. Loose keyword matches are no longer
enough to place an image in the weapon library. The puller prefers explicit
weapon-material prefixes (for example `mtl_weapon_...`) and boundary-aware gun IDs.
Weapon textures are grouped by detected gun:
`NX1_Images/MULTIPLAYER_WEAPONS_BY_GUN/<WEAPON_NAME>/`
The CSV includes the detected weapon, match type, and confidence. Shared optics
or attachments that cannot be safely assigned to one gun go under
`SHARED_ATTACHMENTS` rather than being mislabeled.
