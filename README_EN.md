# How to Add a Custom Unit to Your Map

This guide explains how to integrate a unit from the **Tal'darim Forces Data Library** into your StarCraft II map.

---

## Prerequisites

- Download the latest data library archive:  
  https://www.curseforge.com/sc2/assets/data-library-taldarim-forces/files/7876212
- You need the SC2 Editor opened with your map.

---

## Step 1 — Extract Your Map into Components

1. In the SC2 Editor, go to **File → Save As...**
2. In the dialog, set the file type to **"StarCraft II Component Folder"**.
3. Give it a name **different** from your original map file and save.

> This creates a folder structure where you can freely add and edit data files.

## Step 2 — Open the Component Folder

Navigate to the folder you just saved. This is your map's root folder — all subsequent steps happen inside it.

## Step 3 — Copy All XML Files from the Unit's Archive

Each unit's archive is **self-contained** — alongside the unit's own XML file, it includes all the required base files (`base.xml`, `protoss.xml`, `terran.xml`, `zerg.xml`). This ensures that updates to the base files won't break units you've already added.

Go to `Base.SC2Data/GameData/` inside your map folder.  
Copy **all** `.xml` files from the unit's archive into this folder.

> You can keep the folder structure from the archive (e.g. `GameData/Taldarim/Ascendant/Ascendant.xml`).

To see which base files a specific unit needs, check the `<!-- Requires: -->` lines at the top of its XML file:

```xml
<!-- Requires: Unit:Generic_Unit_Ground[base.xml] -->
<!-- Requires: DataCollectionUnit:Weapon_Base[base.xml] -->
```

The file name in brackets (here `base.xml`) is the required base file. All of them are already included in the archive.

> **Note:** If you are adding multiple units and their archives contain base files with the same names, use the version from the archive of the unit you are adding last. Base files from different units are compatible with each other but may differ in version.

## Step 4 — Register Files in GameData.xml

Inside the `Base.SC2Data/` folder, create (or edit) `GameData.xml`. Add a `<Catalog>` line for every file you copied — both the base files and the unit file:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Includes>
    <Catalog path="GameData/base.xml"/>
    <Catalog path="GameData/protoss.xml"/>
    <Catalog path="GameData/terran.xml"/>
    <Catalog path="GameData/zerg.xml"/>
    <Catalog path="GameData/Taldarim/Ascendant/Ascendant.xml"/>
</Includes>
```

> Replace the last path with the actual path to your unit's XML file.  
> Only register the base files you actually copied — not all units require all four.

## Step 5 — Copy Asset Folders

Copy all `Assets` folders from the archive into the **root** of your map folder.  
These contain the 3D models, textures, and sounds used by the unit.

## Step 6 — Merge Localization Text

Open the localization text files from the archive (e.g. `ruRU.SC2Data/GameStrings.txt`) and copy their contents into the corresponding files in your map:

| Archive file | Your map file |
|---|---|
| `ruRU.SC2Data/GameStrings.txt` | `ruRU.SC2Data/LocalizedData/GameStrings.txt` |
| `enUS.SC2Data/GameStrings.txt` | `enUS.SC2Data/LocalizedData/GameStrings.txt` |

> If your map doesn't have these files yet, create them.

## Step 7 — Copy Localized Asset Folders

Copy the localized asset folders (e.g. `ruRU.SC2Assets`, `enUS.SC2Assets`) from the archive into the **root** of your map folder.

---

## Quick Checklist

- [ ] Map extracted as a Component Folder
- [ ] All XML files from the unit's archive (including base files) copied to `Base.SC2Data/GameData/`
- [ ] All files registered in `Base.SC2Data/GameData.xml`
- [ ] `Assets` folders copied to map root
- [ ] Localization text merged into `GameStrings.txt`
- [ ] Localized asset folders (`*.SC2Assets`) copied to map root
