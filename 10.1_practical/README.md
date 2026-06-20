<div align="center">

# 🔥 Flame Test Lab
### An Interactive 3D Virtual Chemistry Practical — Built in Unity

*Identify metal ions by the colour they burn — no Bunsen burner required.*

![Unity](https://img.shields.io/badge/Engine-Unity-000000?logo=unity&logoColor=white)
![Input System](https://img.shields.io/badge/Input-New%20Input%20System-2c2c2c)
![Subject](https://img.shields.io/badge/Subject-Chemistry-7b2ff7)
![Practical](https://img.shields.io/badge/Type-Virtual%20Practical-ff6b6b)
![Status](https://img.shields.io/badge/Status-Active-4caf50)

</div>

---

## 🧪 What Is This?

**Flame Test Lab** is a self‑contained Unity scene that turns the classic
**flame test experiment** into a hands‑on, first‑person virtual practical.
Drop into the lab, grab a nichrome wire, clean it with HCl, dip it into a
salt sample, and hold it in the burner flame to reveal which metal ion is
hiding inside.

Built entirely from a single runtime script (`FlameTestLabRuntime.cs`) that
procedurally generates the beaker, burner, wire, salt rack, and UI — open
the scene and it builds itself.

---

## 🌈 Flame Colour Reference

Six salts, six ions, six unmistakable flame colours:

| Salt | Ion | Flame Colour | Swatch |
|------|-----|--------------|--------|
| `NaCl` | **Na⁺** | Golden Yellow | ![#FFC214](https://img.shields.io/badge/-FFC214-FFC214) |
| `CaCl2` | **Ca²⁺** | Orange Red | ![#FF4F0F](https://img.shields.io/badge/-FF4F0F-FF4F0F) |
| `SrCl2` | **Sr²⁺** | Crimson Red | ![#FF0D08](https://img.shields.io/badge/-FF0D08-FF0D08) |
| `BaCl2` | **Ba²⁺** | Apple Green | ![#73FF2E](https://img.shields.io/badge/-73FF2E-73FF2E) |
| `CuSO4` | **Cu²⁺** | Blue Green | ![#00EBD1](https://img.shields.io/badge/-00EBD1-00EBD1) |
| `KCl` | **K⁺** | Lilac | ![#A15CFF](https://img.shields.io/badge/-A15CFF-A15CFF) |

> 💡 **The science:** heat excites the electrons in each metal ion. As they
> fall back to lower energy levels, they release that energy as light of a
> very specific colour — a fingerprint for the ion.

---

## 🎮 How the Practical Works

The lab is played in three simple drag‑and‑drop steps:

1. 🧴 **Clean** — Drag **HCl** onto the beaker to clean the nichrome wire.
2. 🧂 **Load** — Drag a **salt sample** from the shelf onto the wire.
3. 🔥 **Test** — Drag the **wire** into the burner flame and observe the colour.

Get it wrong? No problem — **Reset Lab** clears the wire, the flame, and your
observation log so you can start fresh.

---

## 📋 Practical Modules

A tabbed side panel guides students through the full practical workflow:

| Module | Purpose |
|--------|---------|
| 🎯 **Aim** | States the experiment's objective and the ions covered |
| 📝 **Procedure** | Step‑by‑step instructions + live ion‑identification prompt |
| 📊 **Observation** | Auto‑generated table logging every salt, colour, and ion tested |
| ❓ **Quiz** | A 6‑question self‑test with a running score |
| 🗣️ **Viva** | Conceptual viva‑voce questions for deeper understanding |

---

## 🗂️ Project Structure

```
Assets/
├── Scenes/
│   └── SampleScene.unity              # The lab — press Play and it builds itself
├── Scripts/
│   └── FlameTestLabRuntime.cs         # Procedural scene builder + practical logic
└── InputSystem_Actions.inputactions   # Unity New Input System action map
```

---

## 🚀 Getting Started

1. **Import** `10_1_practical.unitypackage` into a Unity project
   (`Assets → Import Package → Custom Package…`).
2. Open **`Assets/Scenes/SampleScene.unity`**.
3. Hit **▶ Play** — the beaker, burner, wire, salt rack, and UI are all
   generated automatically at runtime.
4. Work through the **Procedure**, **Quiz**, and **Viva** tabs in the side
   panel.

### Requirements
- Unity 2021.3 LTS or newer
- [Input System](https://docs.unity3d.com/Packages/com.unity.inputsystem@latest) package

---

## 🤝 Contributing

Ideas for more salts, better flame VFX, or additional viva questions are
welcome — open an issue or submit a pull request.

## 📄 License

Add your preferred license here (e.g. MIT) before publishing.

---

<div align="center">
<sub>Built for chemistry students who want to set things on fire — safely. 🔥🧪</sub>
</div>
