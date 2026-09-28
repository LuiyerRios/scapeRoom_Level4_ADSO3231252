# Level 4 — The Encrypted Terminal

**Project K-9 • NEXUS-9 • Escape Room**
SENA CDITI — Software Analysis and Development (ADSO)

> Game module developed by **Team Unity 1**. This README documents the story, puzzles, solutions, integration with the other levels, and how to run the level.

---

## 👥 Team

| Member | Role |
|---|---|
| Luiyer Gamaiel | Leader |
| Karen Herrera | Developer |
| Jhoan Sebastián Marín | Developer |
| Johan Esteban Lemus | Developer |

---

## 📖 Story

Luna arrives in a dark room. A single terminal lights up the place. The screen reads:

```
ACCESS DENIED — ENTER PASSWORD
```

To move forward, Luna must crack the terminal's password.

## 🎯 Objective

Decrypt the terminal password and obtain **Key 4**, which grants access to Level 5 (The NEXUS Core).

## 🧩 Scene Objects and Elements

| Element | Purpose |
|---|---|
| Terminal | Displays the encrypted messages and receives the password |
| Hints | Help shown according to the difficulty mode |
| Code panel | Displays the challenges (binary and Caesar) |
| Keyboard | Text input for answers |
| Door | Level exit; opens once the password is validated |

---

## 🔐 Puzzles and Solutions

### Puzzle 1 — Binary

The terminal displays:

```
01001100 01010101 01001110 01000001
```

Each byte is a letter in ASCII code:

| Binary | Decimal | Letter |
|---|---|---|
| 01001100 | 76 | L |
| 01010101 | 85 | U |
| 01001110 | 78 | N |
| 01000001 | 65 | A |

✅ **Answer:** `LUNA`

### Puzzle 2 — Caesar Cipher

The terminal displays an encrypted text with the hint **"Shift back two positions"**.

> ⚠️ **Correction to the master document:** the original text `NQPC` shifted back two positions gives **LONA**, not LUNA (N→L, Q→**O**, P→N, C→A). To make the solution unambiguous, the text **`NWPC`** is used instead:

| Encrypted | −2 | Result |
|---|---|---|
| N | → | L |
| W | → | U |
| P | → | N |
| C | → | A |

✅ **Answer:** `LUNA`

### Puzzle 3 — Final Password

The terminal displays:

```
LUNA + 4
```

✅ **Password:** `LUNA4`

When entered, the terminal responds:

```
ACCESS GRANTED
ACCESO AL NÚCLEO AUTORIZADO   (Core access authorized)
```

---

## 🏆 Reward

🔑 **KEY 4**

---

## ⚡ Difficulty Modes

The story and puzzles are the same across all three modes. Only the global time limit and the number of hints change.

| Mode | Total game time | Hints in this level |
|---|---|---|
| Easy | 90 min | Many — explains ASCII and how the Caesar cipher works |
| Normal | 60 min | Limited — only the "Shift back two positions" hint |
| Hard | 40 min | Very few — no table or explanation |

> _To be defined with Team Game Design: exact number of hints per mode._

---

## 🔗 Integration with Other Levels

| | Detail |
|---|---|
| **Scene** | `Nivel04` |
| **Entry** | Requires **Key 3** (Level 3 — The Servers completed) |
| **Exit** | When `LUNA4` is validated: **Key 4** is granted, **autosave** runs, and `Nivel05` is unlocked |
| **Contribution to the final code (Level 6)** | Hint 4: `Level 4 = LUNA4` → segment `4` in the code `4-247-123-4-1013` |

**Rule:** the only valid path is `1 → 2 → 3 → 4 → 5 → 6`. The level cannot be entered without Key 3.

### Level Flow

```
Enter with Key 3
      │
      ▼
Puzzle 1: Binary   ──►  LUNA
      │
      ▼
Puzzle 2: Caesar   ──►  LUNA
      │
      ▼
Puzzle 3: LUNA + 4 ──►  LUNA4
      │
      ├── ❌ Wrong   → "ACCESS DENIED" + hint (based on difficulty)
      │
      └── ✅ Correct → "ACCESS GRANTED" → Key 4 → Autosave → Nivel05
```

---

## ⚙️ Technical Responsibilities

- Interactive terminal
- Keyboard for entering answers
- Password validation
- Error messages (`ACCESS DENIED`)
- Difficulty-based hint system
- Visual feedback for errors and success
- Transition to Level 5

---

## 🛠️ Technologies

| Tool | Version |
|---|---|
| Flutter | 3.47.5 (stable) |
| Dart | 3.13.4 |
| Game engine | Flame _(to be confirmed)_ |
| Platforms | Android and Web (Chrome) |
| Version control | Git + GitHub |

---

## 🚀 Installation and Running

### Requirements

- Git
- Flutter SDK (includes Dart)
- Chrome (for web) or Android Studio (for Android)
- VS Code with the Flutter extension

> See the full installation guide in `docs/installation.md` _(pending)_.

### Important Recommendations

- Install the SDK in a simple path, for example `C:\src\flutter`.
- **Do not** work inside OneDrive — syncing locks files.
- Avoid paths with spaces, accents, or special characters (such as ñ).

### Run

```bash
# Clone the repository
git clone <REPOSITORY_URL>
cd <repository_name>

# Get dependencies
flutter pub get

# Check the environment
flutter doctor

# Run on Chrome
flutter run -d chrome

# Run on Android (emulator or connected phone)
flutter run
```

---

## 📁 Proposed Structure

```
lib/
└── niveles/
    └── nivel04/
        ├── nivel04.dart            # Main scene
        ├── componentes/
        │   ├── terminal.dart
        │   ├── teclado.dart
        │   ├── panel_pistas.dart
        │   └── puerta.dart
        └── puzzles/
            ├── puzzle_binario.dart
            ├── puzzle_cesar.dart
            └── puzzle_contrasena.dart

assets/
└── nivel04/                        # Level images and sounds

docs/
└── nivel04/
    └── diagramas/                  # UML diagrams
```

> _Subject to the structure defined in the project's main repository._

---

## 📐 Documentation

| Diagram | Status |
|---|---|
| Component diagram | ⏳ Pending |
| Deployment diagram | ⏳ Pending |
| Class diagram | ⏳ Pending |
| Architecture diagram | ⏳ Pending |
| Activity diagram | ⏳ Pending |

---

## ✅ Level Checklist

- [ ] Level only opens with Key 3
- [ ] Binary puzzle works
- [ ] Caesar puzzle works (text `NWPC`)
- [ ] `LUNA4` password validation
- [ ] Error message on wrong password
- [ ] Different hints per difficulty
- [ ] Key 4 is granted
- [ ] Autosave on level completion
- [ ] Transition to `Nivel05`
- [ ] Level tested from start to finish

---

## 🌿 Git Workflow

```bash
# Create the level branch
git checkout -b nivel04

# Save changes
git add .
git commit -m "feat(nivel04): description of the change"
git push origin nivel04
```

Every change must be logged in GitHub/Jira to avoid conflicts with other teams.