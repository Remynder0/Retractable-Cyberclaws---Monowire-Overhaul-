# GEMINI.md - Project Rules & CDPR Mod.io Standards

This document defines the strict architectural rules, coding conventions, and **CD Projekt RED (Patch 2.5 / mod.io)** compliance requirements for the **Edgerunner Netrunner Cyberclaws** project. Any AI assistant or contributor working on this repository must adhere to these guidelines.

---

## 1. Core Architectural Mandate ("Approach B")

* **Database Base:** Always use the **Monowire (`Items.AdvancedNanoWires*`)** as the foundational TweakDB record. Never create standalone custom cyberware IDs that require `ArchiveXL` or `Cyberware-EX` to equip.
* **Visual & Animation Rig:** Override the Monowire's entity, mesh, and attack animations with the **Mantis Blades (`a0_005_wa__mantis_blades`)** assets.
* **Skill Tree Integrity:** All perks in the **Intelligence** tree (specifically the left branch: *Finisher: Live Wire*, *Siphon*, and the *Relic Data Tunneling* Quickhack slot) must remain 100% functional without requiring custom UI `.inkwidget` edits.
* **Balance Philosophy (Roleplay & Immersion First):** Do not introduce overpowered (OP) stat multipliers. Damage output, attack speed, and RAM recovery rates must remain balanced against vanilla Legendary cyberware.

---

## 2. CD Projekt RED & Mod.io Technical Restrictions (Patch 2.5)

Because this mod targets the official **In-Game Mod Browser (mod.io)** across PC and consoles (PS5, Xbox Series X|S, Switch 2), the following technical constraints are **non-negotiable**:

### A. Forbidden Dependencies
* **NO Third-Party Script Extenders:** Do not use or require `RED4ext`, `Cyber Engine Tweaks (CET)`, `ArchiveXL`, `TweakXL`, `Codeware`, or `System-EX`.
* The mod must run purely on the native **Cyberpunk 2077 Patch 2.5 engine** and the official **REDmod** pipeline.

### B. 3D Asset & Archive Rules (`*.archive`)
* **Replacers Only:** Custom `.mesh`, `.rig`, `.app`, and `.ent` files inside the `.archive` must replace existing vanilla file paths. Adding brand-new custom file paths without `ArchiveXL` will fail to load on consoles.
* **Submesh Count Preservation:** When hiding the vanilla Mantis Blades geometry in Blender, **never delete a submesh object entirely**. Always leave at least one microscopic triangle (`Scale: 0.001`) hidden inside the wrist bone to preserve the exact submesh index count expected by the engine.
* **Strict Bone Weighting:** Claws must only be weighted (`1.000`) to existing vanilla distal phalanx bones (`*HandIndex3/4`, `*HandMiddle3/4`, etc.). Do not add custom bones to the `.rig`.

### C. TweakDB Formatting Rules (`tweaks/*.json`)
* **JSON Format Only in Production:** While `.yaml` may be used temporarily in `raw_assets/` for human readability, the `mod.io` cloud validator strictly rejects `.yaml` and `.tweak` files.
* All TweakDB modifications in the `build/` folder **must** be compiled into `.json` using:
  `redmod.exe cloud-validation -target-platform=windows -directory="..."`

### D. Redscript Rules (`scripts/*.redscripts`)
* Avoid custom scripts unless strictly necessary for animation/finisher hooks.
* If scripts are used, they **must** be pre-compiled alongside a `.redscripts.h64` binary cache using `validate-mod-scripts` before packaging.

---

## 3. Content, IP, and Legal Guidelines (CDPR QA Compliance)

Every mod uploaded to **mod.io** undergoes manual QA verification by CD Projekt RED before appearing in the in-game browser. To pass QA on the first submission:

1. **Naming & Branding:**
   * Do **not** use third-party copyrighted brand names or trademarks in the mod title, description, or textures.
   * Keep the public mod title generic and lore-friendly (e.g., *"Edgerunner Netrunner Cyberclaws"* or *"Retractable Cyberclaws - Monowire Overhaul"*).
2. **No AI-Generated Assets:**
   * CDPR strictly prohibits AI-generated textures, meshes, icons, or voice files on the official mod browser. All 3D models and materials must be handcrafted in Blender / WolvenKit.
3. **Age Rating & Content Safety:**
   * Do not include explicit/NSFW modifications or unauthorized shader alterations to character nudity.

---

## 4. Assistant Workflow Instructions

When assisting the developer on this repository:
* **Language:** All code, comments, commit messages, and documentation in the repository must be written in **English** (conversational support with the developer may remain in French).
* **Step-by-Step Guidance:** Remember the developer is learning Blender and WolvenKit from scratch. Provide exact menu paths, hotkeys, and exact vanilla file paths whenever discussing 3D edits or TweakDB keys.
* **Verification First:** Before suggesting any TweakDB property or Redscript hook, verify that it works natively in vanilla REDmod 2.5 without requiring `TweakXL` extensions.