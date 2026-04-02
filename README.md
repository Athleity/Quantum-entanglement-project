# Quantum Computing Project

## What is this?

I built this project to really understand quantum entanglement - not just the theory, but actually running circuits on real IBM quantum computers. It covers everything from basic state comparison to hardware validation.

**The headline result?** I achieved **99.86% fidelity** generating Bell states on IBM's 133-qubit `ibm_torino` processor. That's pretty good for real hardware with all its noise!

---

## The Results (No Fluff)

| What I Measured | What I Got | Why It Matters |
|----------------|------------|----------------|
| Bell state fidelity | 99.86% | Real quantum hardware can be surprisingly accurate |
| CHSH value (Bell state) | 2.828 (max possible) | Confirms quantum mechanics - no hidden variables |
| Entropy range | 0 → 1 | Covers fully separable to maximally entangled |
| Purity range | 1 → 0.5 | Matches theory exactly |

---

## What's Inside (10 Parts)

**Part 1: Swap Test**
I compare quantum states using an ancilla qubit trick. Shows how similar two random states are.

**Part 2: Entropy vs Rotation**
Took a simple 2-qubit state `cos(γ/2)|00⟩ + sin(γ/2)|11⟩` and watched how entanglement changes as I rotate γ from 0 to 2π. Entropy peaks at π/2 (Bell state) and hits zero at 0 and π (separable).

**Part 3: Bloch Sphere**
Visualized what happens to one qubit when the other is entangled. For separable states, the vector sits on the sphere surface (pure state). For Bell states, it shrinks inside (mixed state). This really helped me visualize entanglement.

**Part 4: Probability Distributions**
Simple but revealing. At γ=0, 100% chance of |00⟩. At γ=π/2, 50-50 split between |00⟩ and |11⟩. No |01⟩ or |10⟩ ever appear. That's the weird thing about this state.

**Part 5: Noise Effects**
Added depolarizing noise to the swap test circuit. As noise increased, overlap measurements dropped. Even identical states started looking different. Real quantum computers have this problem constantly.

**Part 6: Entropy Under Noise**
Applied the depolarizing channel `ρ' = (1-p)ρ + (p/4)I₄` to different initial states. Three things stood out:

- Bell state (γ=π/2): entropy stayed near 1 throughout (already maximally mixed)
- Partial entanglement (γ=π/4): entropy climbed from 0.6 to 1
- Separable state (γ=0): entropy went from 0 to 1 (biggest change)

At p=1, everything becomes the maximally mixed state. Noise destroys quantum information.

**Part 7: Three Ways to Measure Entanglement**
I implemented:
- Von Neumann entropy (information theory approach)
- Concurrence (Wootters formula - algebraic)
- Entanglement of Formation (operational - how many Bell pairs needed)

All three gave identical results (correlation ~1.0). That's reassuring - different math, same physics.

**Part 8: CHSH Bell Test**
This was fun. The CHSH parameter S should be 2.828 for Bell states (violating the classical bound of 2). My calculation gave exactly that. No local hidden variable theory can explain quantum mechanics.

**Part 9: Purity Analysis**
Purity `P = Tr(ρ²)` is the inverse of entropy. When entropy is 0, purity is 1. When entropy is 1 (maximally mixed), purity hits the theoretical minimum of 0.5 for qubits. The overlay plot shows this beautifully.

**Part 10: Real Hardware (The One I'm Proud Of)**
This part actually ran on IBM's quantum computer. I used `ibm_torino` (133 qubits) and did state tomography - measuring in X, Y, and Z bases to reconstruct the density matrix.

Results from the actual hardware:

| State | γ | Ideal Entropy | Hardware Entropy | Fidelity |
|-------|---|---------------|------------------|----------|
| Separable | 0 | 0.000000 | 0.040613 | 99.56% |
| Partial | π/4 | 0.600876 | 0.585246 | 99.97% |
| **Bell** | **π/2** | **1.000000** | **0.996085** | **99.86%** |
| Partial | 3π/4 | 0.600876 | 0.607036 | 99.90% |
| Separable | π | 0.000000 | 0.038547 | 99.59% |

Average fidelity across all states: **99.78%**

The small deviations come from gate errors, decoherence, and measurement noise. But honestly? 99.86% for a Bell state on real hardware is better than I expected.

---

## How I Built It

**Tools used:**
- Qiskit (obviously - it's the standard for IBM hardware)
- Qiskit Aer for noisy simulations
- NumPy for the math
- Matplotlib and Seaborn for plots

**The hardware:**
IBM Quantum's `ibm_torino` - 133 qubits, running live.

---

## Want to Run This Yourself?

1. **Clone the repo**
```bash
git clone https://github.com/Athleity/Quantum-entanglement-project.git
cd Quantum-entanglement-project
