# 🤖 OPEN-LFR-SIMULATION

**A browser-based Line-Following Robot (LFR) challenge.** Tune a virtual robot, then
watch it drive itself around three tracks using simulated light sensors and real
differential-drive physics.

No installs, no build step, no dependencies — it's a single HTML file. Just open it and play.

![License: MIT](https://img.shields.io/badge/license-MIT-green)
![Dependencies: none](https://img.shields.io/badge/dependencies-none-blue)
![Built with HTML + CSS + JS](https://img.shields.io/badge/built%20with-HTML%20%2B%20CSS%20%2B%20JS-orange)

---

## ▶️ Play it

**Just open the file** — download or clone the repo and double-click **`index.html`**.
It runs in any modern browser (Chrome, Edge, Firefox, Safari).

```bash
git clone https://github.com/jagathram-tech/OPEN-LFR-SIMULATION.git
cd OPEN-LFR-SIMULATION
# then open index.html in your browser
```

There is nothing to install.

---

## 🎯 What is a line-following robot?

A line-following robot (LFR) drives itself by reading a dark line on the floor with small
light sensors. You don't steer it directly — you **set it up** (how fast it goes, how sharply
it corrects, how many sensors it has) and then it follows the track on its own. Your goal is
to tune it well enough to finish each track before time runs out, with as few
"fell off the line" moments as possible.

---

## 🕹️ How to play

1. **Pick a level** on the home screen (start with Level 1).
2. On the setup screen, click **✨ Use recommended settings** — good values are also applied
   automatically the first time you open a level.
3. Press **Start Level** and watch the robot drive.
4. Didn't finish? Tweak the two controls that matter most:
   - **Motor speed** — faster is harder to control.
   - **Steering strength (Kp)** — too low drifts off the line; too high makes it wobble.
5. Reach the red **F** (finish) before the timer ends to clear the track and earn **stars**.

> New here? The home screen has a built-in **"What is this / How do I play?"** panel, and the
> results screen tells you exactly what to change next.

---

## 🎚️ Controls & settings

### The basics (shown by default)

| Control | What it does |
|---|---|
| **Motor speed** | How fast the robot drives. Faster = harder to keep on the line. |
| **Steering strength (Kp)** | How hard it turns back toward the line. |
| **Light sensors** | More sensors = smoother tracking on curves. |
| **Sensor sensitivity** | How dark a surface must be to count as "the line". |

### Advanced (collapsed, for tinkerers)

Behind the **Advanced** section you can change the full robot build and physics model:
robot dimensions (wheel / chassis / track width), motor RPM, mass, surface friction (μ),
motor time-constant (τ), max wheel acceleration, sensor noise, control-loop rate (Hz),
and ambient-light interference.

---

## 🧩 The three levels

| Level | Track | Challenge |
|---|---|---|
| **1 — Beginner** | A clean straight line | Learn the controls |
| **2 — Intermediate** | A smooth figure-8 (lemniscate) | Handle the crossover with responsive sensors |
| **3 — Advanced** | 90° corners, S-curves, a loop and a narrow gauntlet | Precision tuning required |

---

## ⭐ Scoring

- **Clear the track** for a base score, plus a **speed bonus** for finishing with time to spare.
- **Line losses** (drifting off the line) cost points.
- Earn up to **3 stars** based on how fast and how cleanly you drove.
- Your **best score per level** is saved locally in your browser (`localStorage`) — no account needed.

---

## ⚙️ How it works (under the hood)

This is a real little simulation, not a scripted animation:

- **Sensing** — the track is rasterised to an offscreen canvas; each sensor samples pixel
  brightness at its real-world position, with optional Gaussian noise and ambient-light drift.
- **Control** — a **proportional (P) controller** reads the line error from the sensor array
  and adjusts the left/right motor commands.
- **Motors** — PWM commands pass through a deadband and a mild non-linearity, then a
  first-order lag toward target speed, capped by a torque/acceleration limit.
- **Physics** — **differential-drive kinematics** with a traction/slip model: if longitudinal
  plus centripetal acceleration exceeds μ·g, the wheels slip and the robot understeers.
- **Progress** — tracked by the nearest point on the track polyline, clamped to move forward
  only, so the robot has to actually drive the whole route.

---

## 🛠️ Tech

- Single self-contained **`index.html`** — HTML + CSS + vanilla JavaScript.
- HTML5 **Canvas** for rendering and sensor sampling.
- **Zero** external libraries or build tooling.

---

## 📄 License

Released under the [MIT License](LICENSE). © 2026 Jagathram.
