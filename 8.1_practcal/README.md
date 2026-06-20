<div align="center">

<img src="https://img.shields.io/badge/Unity-2021.3%2B-black?style=for-the-badge&logo=unity&logoColor=white" />
<img src="https://img.shields.io/badge/Language-C%23-239120?style=for-the-badge&logo=csharp&logoColor=white" />
<img src="https://img.shields.io/badge/Subject-Chemistry-00b4d8?style=for-the-badge&logo=flask&logoColor=white" />
<img src="https://img.shields.io/badge/Type-Educational%20Simulation-ff6b35?style=for-the-badge" />
<img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />

---

# 🧪 Virtual Chemistry Lab — Unity Package
### `8_1_practical.unitypackage`

**An interactive, step-by-step chemistry education simulator built entirely in Unity using runtime-generated 3D environments, procedural UI, and guided laboratory workflows — no external assets required.**

---

</div>

## 📋 Table of Contents

- [Overview](#-overview)
- [What's Inside](#-whats-inside)
- [Scripts Reference](#-scripts-reference)
- [Lab Experiments Covered](#-lab-experiments-covered)
- [Installation & Setup](#-installation--setup)
- [How to Use](#-how-to-use)
- [Project Structure](#-project-structure)
- [Key Features](#-key-features)
- [Screenshots](#-screenshots)
- [Compatibility](#-compatibility)
- [Contributing](#-contributing)

---

## 🔬 Overview

> **This Unity package delivers a fully self-contained virtual chemistry laboratory.** All scenes, UI, 3D geometry, lighting, and logic are generated at runtime through C# scripts — making it portable, asset-free, and instantly importable into any Unity project.

The package covers **two major chemistry practicals**:

| Practical | Concept | Difficulty |
|-----------|---------|------------|
| 🔥 **Flame Test (BaCl₂)** | Identifying metal ions by flame colour | Beginner |
| ⚗️ **Iron Sulphide Synthesis** | Direct combination reaction: Fe + S → FeS | Intermediate |

---

## 📦 What's Inside

```
8_1_practical.unitypackage
│
├── Assets/
│   ├── Scripts/
│   │   ├── PracticalChemistryLabController.cs       ← Hands-on Flame Test Lab
│   │   ├── RealisticVirtualChemLabController.cs     ← 12-Step Iron Sulphide Lab
│   │   ├── VirtualChemistryLabController.cs         ← Interactive Flame Test Module
│   │   └── ChemistryLabAppController.cs             ← Full App (13-Screen Flow)
│   │
│   ├── Scenes/
│   │   └── SampleScene.unity                        ← Entry point scene
│   │
│   ├── Screenshots/                                 ← In-editor preview images
│   │   ├── flame_test_lab_first_person.png
│   │   ├── practical_chemistry_lab_hands_on.png
│   │   ├── realistic_virtual_chemlab_*.png
│   │   └── chemistry_lab_app_guide_flow.png
│   │
│   ├── _Recovery/
│   │   └── 0.unity                                  ← Recovery scene backup
│   │
│   └── InputSystem_Actions.inputactions             ← Unity Input System config
```

---

## 📝 Scripts Reference

### 🟡 `PracticalChemistryLabController.cs`
> **The beginner-friendly, hands-on Flame Test practical.**

This controller simulates the classic **BaCl₂ flame test** in a guided, 7-step workflow.

**Workflow Steps (enum `LabStep`):**

```
PickWire → CleanWire → PickSalt → LoadSalt → LightBurner → HeatWire → RecordObservation → Complete
```

**Key behaviours:**
- ⚠️ **Inventory is context-sensitive** — only shows items needed for the current step
- 🌿 Animated **apple-green flame glow** using `Mathf.Sin` pulsing
- ✅ Particle burst spawned on correct observation
- 🔁 Full reset via `ResetPractical()` — all objects return to initial state
- 📋 **Observation board** in 3D world updates live with `TextMesh`
- ❌ Wrong colour choice gives instant feedback without advancing the step

**Important Classes & Fields:**

| Member | Type | Purpose |
|--------|------|---------|
| `LabStep` | `enum` | Controls which step the user is on |
| `selectedItem` | `string` | Tracks currently selected inventory item |
| `recordedColour` | `string` | Stores the student's colour observation |
| `greenGlowObject` | `GameObject` | Animated glow sphere during flame reaction |
| `flameObject` | `GameObject` | Burner flame visual (toggled on `LightBurner`) |

---

### 🟠 `RealisticVirtualChemLabController.cs`
> **A 12-step, fully immersive virtual chemistry lab for the Fe + S → FeS reaction.**

This is the most complete controller — featuring drop-zone mechanics, progress tracking, animated reactions, a lab notebook panel, and an integrated study guide.

**12-Step Workflow:**

```
1. Build Stand Assembly     →   7. Cover Crucible
2. Place Crucible           →   8. Position Burner
3. Weigh Iron (7g)          →   9. Light Burner
4. Weigh Sulphur (4g)       →  10. Heat Strongly (animated)
5. Mix Powders              →  11. Cool Product (animated)
6. Magnet Test (before)     →  12. Magnet Test (after)
```

**Guide Tabs available in-app:**

| Tab | Content |
|-----|---------|
| `Aim` | Experiment objective |
| `Apparatus` | Full equipment list |
| `Theory` | Fe + S chemistry explanation |
| `Procedure` | 8-step written procedure |
| `Observation` | Before/during/after observations |
| `Viva` | 3 Q&A viva questions |
| `Quiz` | 5 self-check questions |
| `Result` | Conclusion statement |

**Key Features:**

- 🎯 **Drop-zone placement system** — items must be placed on the correct coloured zone markers
- 📊 **Live progress bar** tracking completion across all 12 steps
- ⚖️ **Animated digital balance** counts up smoothly to the target mass
- 🔴 **Heat animation coroutine** — crucible colour shifts from yellow-grey → red-hot → dark FeS
- 💨 **Smoke column** spawns procedurally during the reaction
- ✨ **Spark particles** randomly burst from the crucible while heating
- 🧲 **Magnet comparison** — before heating (iron attracted) vs. after (FeS not attracted)
- 📓 **Live notebook panel** — updates automatically at each stage

> **⚠️ IMPORTANT:** Wrong zone placement triggers a **panel shake animation** (`ShakePanel` coroutine) as visual feedback.

---

### 🔵 `VirtualChemistryLabController.cs`
> **An open-style Flame Test lab with a shelf-and-slot drag-and-drop system.**

This controller creates a more freeform experience — students pick materials from a shelf and drop them onto the lab bench.

**Available Materials:**

| Material | Flame Colour | Ion |
|----------|-------------|-----|
| NaCl | Yellow | Na⁺ |
| CaCl₂ | Brick Red | Ca²⁺ |
| SrCl₂ | Crimson | Sr²⁺ |
| **BaCl₂** | **Apple Green** | **Ba²⁺** |
| KCl | *(listed)* | K⁺ |
| CuSO₄ | *(listed)* | Cu²⁺ |

**Key behaviours:**
- Shelf items instantiated as coloured 3D prefabs (cylinders + cubes built in code)
- 7 slot markers on the lab table for placed modules
- Bobbing animation on placed items (`Mathf.Sin` per-slot phase offset)
- `RunReaction()` auto-ensures all needed items are placed before triggering
- Persistent green flame (`Apple Green Burner Flame`) spawns on reaction

---

### 🟣 `ChemistryLabAppController.cs`
> **A complete 13-screen Chemistry App — quiz, viva, score card, and animated 3D lab.**

This is the most app-like of the four controllers, designed as a **full guided learning flow**.

**13 Screens in order:**

```
[1] Main Menu          [6] Pre-Lab Quiz      [11] Post-Lab Quiz
[2] Experiment Info    [7] Procedure         [12] Viva
[3] Materials          [8] Observation       [13] Score Card
[4] Theory             [9] Reaction Animation
[5] Safety Checklist   [10] Result
```

**Quiz system:**
- Pre-Lab Quiz (4 questions) and Post-Lab Quiz (4 questions)
- Correct/incorrect feedback with colour coding (🟢 green / 🔴 red)
- Score tracked separately for pre and post, combined into a grade
- Grades: `A+` (≥90%) | `A` (≥80%) | `B` (≥70%) | `C` (≥60%) | `D` (below)

**Viva system:**
- 3 typed-out answers using a `TypeAnswer` coroutine (character-by-character reveal)
- "Reveal Answer" button per question

**Safety Checklist (interactive):**
- Click each item to toggle `□` → `✓`
- Items: goggles, hair, hot wire, HCl, sample size, calm observation

> **⚠️ IMPORTANT:** Score persists across screen navigation within the same session. Use "Restart App" to reset scores.

---

## ⚗️ Lab Experiments Covered

### Experiment 1 — Flame Test for Metal Ions
**Aim:** Identify metal ions by the colour they emit when heated in a Bunsen flame.

**Reaction highlighted:** `BaCl₂` → **Apple Green Flame** → confirms **Ba²⁺**

**Required apparatus:**
- Nichrome wire (carrier)
- HCl solution (cleaning agent)
- Bunsen burner (heat source)
- BaCl₂ salt sample

**Colour reference table:**

| Salt | Flame Colour | Ion Identified |
|------|-------------|----------------|
| NaCl | 🟡 Yellow | Na⁺ |
| KCl | 🟣 Lilac | K⁺ |
| CaCl₂ | 🧱 Brick Red | Ca²⁺ |
| SrCl₂ | 🔴 Crimson | Sr²⁺ |
| BaCl₂ | 🟢 Apple Green | Ba²⁺ |

---

### Experiment 2 — Preparation of Iron Sulphide (Fe + S → FeS)

**Aim:** Demonstrate direct combination by heating iron and sulphur to form a new compound.

**Reaction:** `Fe + S → FeS`

**Key observations to record:**
1. Before heating: grey/yellow mixture; iron filings respond to magnet
2. During heating: mixture glows red with sparks and smoke
3. After cooling: dark grey-black iron sulphide — **not attracted to magnet**

**Masses used:**
- Iron filings: `7.00 g`
- Sulphur powder: `4.00 g`

---

## 🚀 Installation & Setup

### Prerequisites

> **⚠️ REQUIRED:** Unity `2021.3 LTS` or later. The Input System package must be installed.

1. Open **Unity Hub** and create or open a project.
2. Ensure the **Input System** package is installed:
   - Go to `Window → Package Manager`
   - Search for `Input System` and install it
   - When prompted, restart Unity and enable the new input system

### Importing the Package

```
1. In Unity, go to:
   Assets → Import Package → Custom Package...

2. Navigate to and select:
   8_1_practical.unitypackage

3. In the Import dialog, select ALL items (default)
   and click Import.
```

### Running the Lab

```
1. Open the scene:
   Assets → Scenes → SampleScene.unity

2. Press ▶ Play in the Unity Editor.

3. Choose which controller to attach:
   - Select the Main Camera (or an empty GameObject)
   - Add Component → search for one of:
       • PracticalChemistryLabController
       • RealisticVirtualChemLabController
       • VirtualChemistryLabController
       • ChemistryLabAppController
```

> **💡 TIP:** Each script is entirely self-contained. Attaching any one of them will build the full scene, UI, and world geometry on `Awake()`. You do not need to configure any additional GameObjects or prefabs.

---

## 🖥️ How to Use

### Practical Flame Test Lab (`PracticalChemistryLabController`)

```
Step 1 → Select "Wire" from inventory, click "Take wire"
Step 2 → Select "HCl", click "Dip wire in HCl"
Step 3 → Select "BaCl2", click "Take BaCl2"
Step 4 → Click "Touch wire to salt" (no item selection needed)
Step 5 → Select "Burner", click "Turn on burner"
Step 6 → Click "Put wire in flame"
Step 7 → Observe the green flame, click "Apple green"
         ✅ Practical complete!
```

### Realistic Iron Sulphide Lab (`RealisticVirtualChemLabController`)

```
• Select the highlighted item from the top inventory
• Click the matching coloured drop zone on the bench
• For Steps 10–11 (heating/cooling): click the action button directly
• Use the guide tabs (Aim / Theory / Procedure / etc.) for reference
• Progress bar fills as you complete each step
```

### Full App (`ChemistryLabAppController`)

```
• Navigate screens using Back / Next buttons or numbered dots
• Complete Safety Checklist by clicking each item
• Answer quiz questions — feedback shown immediately
• Use "Reveal Answer" in Viva to see typed answers
• Score Card shows your combined grade at the end
```

---

## 📁 Project Structure

```
Assets/
├── Scripts/                          ← All runtime logic
│   ├── PracticalChemistryLabController.cs
│   ├── RealisticVirtualChemLabController.cs
│   ├── VirtualChemistryLabController.cs
│   └── ChemistryLabAppController.cs
│
├── Scenes/
│   └── SampleScene.unity             ← Open and press Play
│
├── Screenshots/                      ← Reference images
│   ├── flame_test_lab_first_person.png
│   ├── practical_chemistry_lab_hands_on.png
│   ├── realistic_virtual_chemlab_final.png
│   ├── realistic_virtual_chemlab_playmode.png
│   ├── realistic_virtual_chemlab_step2_verified.png
│   ├── realistic_virtual_chemlab_step_wait.png
│   ├── clean_wall_virtual_chemlab.png
│   ├── plain_wall_virtual_chemlab.png
│   └── chemistry_lab_app_guide_flow.png
│
├── _Recovery/
│   └── 0.unity                       ← Backup scene
│
└── InputSystem_Actions.inputactions  ← Input bindings
```

---

## ✨ Key Features

### 🏗️ Fully Procedural 3D World
All geometry is created at runtime using `GameObject.CreatePrimitive()`. No meshes, prefabs, or textures required. The lab builds itself from code every time you press Play.

### 🎓 Curriculum-Aligned Content
Content follows standard chemistry curriculum for:
- Flame test identification of metal ions
- Direct combination reactions
- Viva Q&A and pre/post-lab assessment

### 📱 Responsive UI System
All UI panels use `CanvasScaler` with `ScaleWithScreenSize` at `1440×900` reference, ensuring the interface scales correctly across different resolutions.

### 🔄 Full Reset Support
Every controller includes a reset function:
- `ResetPractical()` — PracticalChemistryLabController
- `ResetLab()` — RealisticVirtualChemLabController
- `ClearTable()` — VirtualChemistryLabController
- Score reset on "Restart App" — ChemistryLabAppController

### ⚡ Input System Compatible
The package includes `InputSystem_Actions.inputactions` and automatically detects whether `InputSystemUIInputModule` or the legacy `StandaloneInputModule` should be used.

### 🎨 Colour-Coded Feedback System

| Colour | Meaning |
|--------|---------|
| 🟢 Green | Correct / Success |
| 🟡 Yellow/Amber | Prompt / Attention needed |
| 🔴 Red | Error / Wrong answer |
| 🔵 Blue/Cyan | Neutral / Accent |

---

## 🖼️ Screenshots

Screenshots are bundled inside the package under `Assets/Screenshots/`. Open them in Unity to preview the lab at various stages:

| Filename | Shows |
|----------|-------|
| `flame_test_lab_first_person.png` | First-person view of the flame test |
| `practical_chemistry_lab_hands_on.png` | Hands-on practical UI in action |
| `realistic_virtual_chemlab_playmode.png` | Full lab in Play mode |
| `realistic_virtual_chemlab_final.png` | Completed reaction with FeS |
| `chemistry_lab_app_guide_flow.png` | App guide flow screen |

---

## 🔧 Compatibility

| Setting | Requirement |
|---------|-------------|
| **Unity Version** | 2021.3 LTS or later |
| **Render Pipeline** | Built-in Render Pipeline (Standard shader) |
| **Input System** | Unity Input System package installed |
| **Platform** | Windows, macOS, Android, iOS, WebGL |
| **No external dependencies** | ✅ Fully self-contained |

> **⚠️ NOTE:** These scripts use the legacy `UnityEngine.UI` text system. If you are using TextMeshPro, the UI text will still render via the built-in `LegacyRuntime.ttf` font. For production use, consider migrating UI text to TMP.

---

## 🤝 Contributing

1. Fork this repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Import the package into your Unity project and make your changes
4. Export the updated package: `Assets → Export Package`
5. Commit and open a Pull Request

**Suggested improvements:**
- [ ] Add TextMeshPro support for sharper UI text
- [ ] Add audio feedback (click sounds, flame audio)
- [ ] Expand flame test to cover all 5 ions (NaCl, KCl, CaCl₂, SrCl₂, BaCl₂)
- [ ] Add a leaderboard or score saving
- [ ] Mobile touch input support

---

<div align="center">

**Built with ❤️ using Unity & C#**

`Fe + S` **→** `FeS` · `BaCl₂` **→** 🟢 **Apple Green** · Chemistry made interactive

</div>
