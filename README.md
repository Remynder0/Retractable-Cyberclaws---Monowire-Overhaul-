# Retractable Cyberclaws - (Monowire Overhaul)

![Cyberpunk 2077](https://img.shields.io/badge/Cyberpunk_2077-Patch_2.5+-yellow.svg)
![Platform](https://img.shields.io/badge/Platform-PC_%7C_PS5_%7C_Xbox_Series_%7C_Switch_2-blue.svg)
![Distribution](https://img.shields.io/badge/Mod.io-Cloud_Validated-success.svg)

## Overview

**Retractable Cyberclaws** is a gameplay and visual overhaul mod for *Cyberpunk 2077* (designed for the Patch 2.5 In-Game Mod Browser via **mod.io**). Inspired by agile netrunner combat styles from Sasha Yakovleva in the music video [Let You Down](https://www.youtube.com/watch?v=BnnbP7pCIvQ). This project transforms the **Monowire (`NanoWires`)** into sleek, retractable fingertip **Cyberclaws** that utilize the **Mantis Blades** animation rig and lunge mechanics while preserving 100% of the **Intelligence Skill Tree** synergies.

---

## Core Architecture

This mod uses the **Monowire (`Items.AdvancedNanoWires*`)** as its database foundation and the Mantis Blade for animations and rigs:

1. **Database & Progression (Monowire Base):**
   * Retains native compatibility with the **Intelligence** attribute and the left-branch Monowire perks (*Siphon*, *Finisher: Live Wire*, RAM recovery on hit).
   * Retains the **Relic Quickhack Slot** (*Data Tunneling*), allowing players to upload Control, Covert, or Combat quickhacks via heavy/charged claw strikes.
2. **Visuals & Combat Rig (Mantis Blades Entity Swap):**
   * Re-routes the Monowire entity/mesh definitions to a customized **Mantis Blades 3D asset** (`a0_005_wa__mantis_blades`).
   * The bulky forearm blades and mechanical pistons are scaled to zero and hidden inside the wrist geometry.
   * Ten custom-modeled metallic claws are weight-painted directly to the distal phalanges (`RightHandIndex3`, `LeftHandIndex3`, etc.).
   * Replaces whipping animations with visceral slashing, clawing, and leaping (*Lunge*) animations native to the Mantis Blades rig.

---

## Key Features

* **Retractable Fingertip Claws:** Normal hands when holstered; lethal carbon/chrome claws when drawn.
* **100% Pure Netrunner Synergy:** Scales with Intelligence, restores RAM per slash, and spreads Quickhacks on charged hits.
* **Feral Mobility:** Grants the Mantis Blades leap/lunge attack to close the distance on hacked targets.
* **Cross-Platform Ready (Patch 2.5):** Built strictly within CD Projekt RED's official `REDmod` / `mod.io` cloud validation standards (No external script extenders required).

---

## Project Milestones & Roadmap

### Milestone 1: Environment Setup & Asset Extraction
- [ ] Install and configure **WolvenKit**, **Blender (3.6 LTS / 4.x)**, and the **Cyberpunk 2077 Blender Add-on**.
- [ ] Extract Female V (`wa`) First-Person (FPP) and Third-Person (TPP) Mantis Blades meshes, rigs, and `.app` / `.ent` files.
- [ ] Extract Monowire (`NanoWires`) TweakDB records for reference across all rarity tiers (Common to Legendary++) and damage types (Physical, Thermal, Electric, Chemical).

### Milestone 2: 3D Modeling & Weight Painting (Blender)
- [ ] Isolate the Mantis Blades blade/piston submeshes and collapse their geometry into a single microscopic hidden triangle inside the wrist to prevent engine crashes.
- [ ] Sculpt 10 sharp, curved cybernetic claws fitted to the fingertip cuticles.
- [ ] Join the claw geometry into the emptied blade submesh.
- [ ] Assign vertex weights (`1.000`) strictly to the distal finger bones (`*HandIndex3/4`, `*HandMiddle3/4`, `*HandRing3/4`, `*HandPinky3/4`, `*HandThumb2/3`).
- [ ] Configure `.mlsetup` / `.mi` shader materials in WolvenKit for polished chrome and matte carbon finishes.

### Milestone 3: TweakDB Hybrid Configuration
- [ ] Create the TweakDB override file targeting all `Items.AdvancedNanoWires*` records.
- [ ] Swap the Monowire `entityName`, `appearanceResourceName`, and attack animation sets with the Mantis Blades equivalents.
- [ ] Retain the `Monowire` / `NanoWires` tags, RAM recovery `OnAttach` packages, and Quickhack `slotPartListPreset`.
- [ ] Ensure Finisher animations use the Mantis Blades impale/slash motion while triggering the *Live Wire* health/RAM regeneration effect.

### Milestone 4: Male V (`ma`) & Glamdoc Support (Optional Stretch Goal)
- [ ] Adapt the 3D claw mesh and bone weights to the Male V (`ma`) hand rig.
- [ ] Integrate visual variants compatible with the Patch 2.5 **Glamdoc** cyberware customization system.

### Milestone 5: Cloud Validation & Mod.io Release
- [ ] Convert all `.yaml` / `.tweak` files into strict `.json` format using `redmod.exe cloud-validation`.
- [ ] Test the packaged mod locally inside `Cyberpunk 2077/r6/c77/retractable_cyberclaws/`.
- [ ] Capture high-resolution in-game screenshots and prepare branding-compliant promotional text.
- [ ] Submit the package to **mod.io** for CDPR QA verification across PC and consoles.

---

## Repository Directory Structure

```text
retractable-cyberclaws/
├── raw_assets/                        # Blender (.blend, .glb) source files (excluded from final build)
├── build/                             # Compiled mod ready for local testing (r6/c77/) and mod.io upload
│   └── edgerunner_cyberclaws/
│       ├── retractable_cyberclaws.archive   # Compiled 3D meshes & materials
│       └── tweaks/
│           └── cyberclaws_tweak.json       # Cloud-validated JSON TweakDB overrides
├── docs/
│   └── sasha_claws_modding_plan.md    # French technical guide & 3D workflow reference
├── GEMINI.md                          # AI Assistant rules, architecture constraints & CDPR guidelines
└── README.md                          # Project overview and roadmap
```

---

## Local Development & Compilation Commands

### 1. Validate and Convert Tweaks to JSON
Run the official REDmod CLI tool to convert TweakDB files into the `mod.io` required `.json` format:
```bash
redmod.exe cloud-validation -target-platform=windows -directory="build/retractable_cyberclaws"
```

### 2. Local Testing Path (Patch 2.5+)
Copy the contents of `build/retractable_cyberclaws/` into:
```text
<Cyberpunk 2077 Install Dir>/r6/c77/retractable_cyberclaws/
```
Enable the mod via the in-game **Mods** menu at the main title screen.
