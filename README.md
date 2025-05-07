# 🐦 AI Flappy Bird with NEAT

---

## 🚀 Overview

This project implements an **AI-powered Flappy Bird game** using the **NEAT (NeuroEvolution of Augmenting Topologies)** algorithm. The AI autonomously **learns to play Flappy Bird** by evolving a neural network that controls a bird’s jump timing to pass through pipes.

> 💡 **Goal:** Train birds to play perfectly through **trial, error, and evolution.**

**Tech stack:**

- 🎮 **Pygame**: For game simulation.
- 🧠 **neat-python**: For neural network evolution.

---

## 🧬 What is NEAT and neat-python?

### 🔍 NEAT (NeuroEvolution of Augmenting Topologies)

**NEAT** is a genetic algorithm that **evolves both the weights and the structure of a neural network.**

**Key features:**

- 🛠 **Starts simple:** Begins with minimal networks that grow more complex over time.
- 🧪 **Speciation:** Groups similar genomes to promote innovation.
- ♻️ **Crossover & mutation:** Mixes and mutates genomes to evolve better performance.

---

### 🐍 neat-python

[`neat-python`](https://neat-python.readthedocs.io/en/latest/) is a Python implementation of the NEAT algorithm that makes it **easy to evolve neural networks** in Python projects.

In this project, it:

- 🐣 Creates and evolves a population of birds (genomes).
- 📈 Calculates fitness based on gameplay.
- 🔄 Evolves smarter birds over generations.

---

## 🧠 Why NEAT?

Unlike traditional machine learning (which requires **large datasets**), NEAT learns by **interacting directly with the environment.** This makes it **perfect for games and simulations**—no labeled data required, just play and learn!

---

## 🎮 How the Neural Network Works

**Input Features (4 total):**

1. Bird’s y-position.
2. Distance to the top of the nearest pipe gap.
3. Distance to the bottom of the nearest pipe gap.
4. Horizontal distance to the nearest pipe.

**Output:**

- 1 value between 0 and 1.
- If > 0.5 → 🕊 **Jump**
- If ≤ 0.5 → 🪂 **Do nothing**

---

### 🏆 Fitness Function

Rewards the birds based on **survival and performance:**

- ✅ +0.3 per frame survived.
- ✅ +0.5 when passing a pipe.
- ✅ +5 bonus for clearing a pipe.
- ⚠️ -1 penalty for colliding.
- 🎯 Small bonus for staying near the pipe gap’s center (encourages precision).

---

---

## 📊 Example Benchmark Results

Here’s how birds improve over time:

- **Generation 1:** Best 1 | Avg 0.5 → Random jumps.
- **Generation 10:** Best 8 | Avg 3.2 → Learning to time jumps.
- **Generation 25:** Best 25 | Avg 15.0 → Outperforms humans.
- **Generation 50:** Best 45 | Avg 30.0 → Masters the game.

---

## ⚙️ Key Configurations (`config.txt`)

**[NEAT]**
- `fitness_criterion`: Selects based on maximum fitness.
- `fitness_threshold`: Stops when a genome hits 100 fitness.
- `pop_size`: 100 birds per generation.
- `reset_on_extinction`: Continue even if all species die.

**[DefaultGenome]**
- Inputs: 4 (bird y + distances)
- Outputs: 1 (jump decision)
- Hidden: Starts with 1 (expands)
- Activation: `tanh` for smooth output.
- Mutation: Balanced to explore & refine.
- Connections: Can add/delete dynamically.

**Other Sections:**
- **SpeciesSet:** Controls how different birds are grouped.
- **Stagnation:** Stops stale species after 20 gens.
- **Reproduction:** Top 2 birds always survive; top 20% can reproduce.

---

## 🗂 Class & Function Reference

### 🐦 Bird

- `__init__`: Setup bird.
- `jump()`: Jump up.
- `move()`: Update position & tilt.
- `draw(win)`: Render bird.
- `get_mask()`: For collision detection.

### 🚧 Pipe

- `__init__`: Create a pipe.
- `set_height()`: Randomize height.
- `move()`: Scroll pipe left.
- `draw(win)`: Render pipes.
- `collide(bird)`: Detect collisions.

### 🏞 Base

- `__init__`: Create scrolling base.
- `move()`: Scroll the ground.
- `draw(win)`: Render ground.

### ⚙️ Main Functions

- `draw_window()`: Draw the full game scene.
- `main()`: Run & evolve birds.
- `run(config_path)`: Start NEAT training.

---

## 📦 Dependencies

- Python 3.x
- `pygame`
- `neat-python`

📥 Install everything:

pip install pygame neat-python
---

## ▶️ How to Run

1️⃣ Download the repo.  
2️⃣ Ensure your folder includes:

- `/imgs/` folder with:  
  bird1.png, bird2.png, bird3.png, pipe.png, base.png, bg.png.
- `config.txt`
- `flappy_bird.py`

3️⃣ Launch:
python flappy_bird.py

---

## 🛠 Troubleshooting & FAQ

- **Black screen/crash?**  
  Check that your images are in the `/imgs/` folder.

- **Pygame display error?**  
  Ensure you're not running headless (Pygame requires a display).

- **Birds aren't learning?**  
  Try increasing `pop_size` or tweaking fitness settings.

- **NEAT stops too soon?**  
  Raise the `fitness_threshold`.

---

## 💡 Further Ideas

- Add moving obstacles.
- Create a human vs AI mode.
- Save/load trained networks.
- Add real-time fitness charts.
- Experiment with different neural architectures (e.g., RNNs).

---

## 📜 Licensing & Credits

- **Game Assets:** Flappy Bird clone graphics (open source).  
- **Libraries:**  
  - Pygame (LGPL license)  
  - neat-python (MIT license)