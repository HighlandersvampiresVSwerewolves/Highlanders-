# 🧛‍♂️ Vampires vs Werewolves – Winning AI  
### CentraleSupélec — MSc Artificial Intelligence

This repository contains the Artificial Intelligence agent developed for the *Vampires vs Werewolves* tournament in the **Foundation of AI** course. The project won the final competition thanks to its combination of adversarial search, probabilistic combat modeling, and threat-aware movement planning.

---

## 🚀 1. Project Overview
The challenge consisted in designing a fully autonomous AI capable of playing the strategic game *Vampires vs Werewolves*.  
At each turn, the server sends board updates, and the agent has **≤ 2 seconds** to compute and send a valid set of moves.  
The AI must respect movement constraints, combat probabilities, and the communication protocol (`SET`, `HUM`, `HME`, `MAP`, `UPD`, `END`, `BYE`).

---

## 🧠 2. Key Features

### ✔ Full Communication Layer  
Implements the complete TCP protocol and ensures stable communication with the server under strict timing constraints.

### ✔ Alpha–Beta Adversarial Search  
- Iterative deepening up to depth 4  
- MAX = our species, MIN = opponent  
- Strong pruning and time-controlled evaluation  

### ✔ Probabilistic Combat Outcome Model  
Uses expected-value reasoning based on the official game rules to estimate:  
- Likelihood of winning a battle  
- Expected surviving attackers  
- Expected conversions of humans  
- Expected losses on both sides  

### ✔ Threat-Aware Pathfinding  
Evaluates each possible step using:  
- Enemy kill thresholds (1.5× rule)  
- Human conversion thresholds  
- Dangerous/unsafe tiles  
- Distance to target and safe routing  

### ✔ Strategic Targeting & Coordination  
Groups select targets using a value-based heuristic balancing:  
- Human conversions  
- Enemy elimination  
- Distance cost  
- Overkill avoidance (too many groups chasing one target)  

### ✔ Smart Conditional Splitting  
Large groups may split when it yields strategic advantage, with checks to prevent redundant or unsafe dispersion.

### ✔ Multi-Group Move Aggregation  
After selecting the main move via Alpha–Beta, remaining groups receive opportunistic greedy moves to increase map pressure.

---

## 🏆 3. Why This AI Won
- Controlled uncertainty using **expected-value combat**  
- Predicted enemy reactions via **adversarial search**  
- Optimized movement with **threat-aware routing**  
- Avoided losing battles through strict threshold reasoning  
- Maximized conversions and map expansion every turn  
- Maintained superior tempo and board presence  

This resulted in consistent dominance across maps during the tournament.

---

## 📁 4. Repository Structure
/src
client_socket.py # TCP communication
state_update.py # Game state management
combat.py # Probability model for battles
pathfinding.py # Safe movement + threat avoidance
move_generation.py # Move + split logic
evaluation.py # State scoring function
search.py # Alpha-Beta search
main.py # Game orchestration


## ▶️ 5. Running the AI

### Requirements
- Python 3.9+  
- No external AI/graph/tree libraries  

### Command
```bash
python3 main.py --ip <server_ip> --port <server_port>
