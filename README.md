# Finite-Volume-Demo (Commented)

Short, self-contained demos of 1D hyperbolic solvers with **clean, commented code**:

- **Linear advection** (finite differences): Upwind (1st), Central (FTCS, unstable), Lax–Wendroff (2nd)  
- **Burgers’ equation** (finite volume): Godunov with **exact Riemann** flux  
- **MUSCL (TVD)**: slope-limited reconstruction with **minmod**, **van Leer**, **Superbee**

The notebook emphasizes **shock capturing** and the **accuracy–stability trade-off** tied to **Godunov’s barrier theorem**.

---

## Why this repo?

Hyperbolic conservation laws model transport, waves, and shocks. Numerically:

- **First-order upwind** is stable and monotone (no spurious oscillations) but **diffusive** at shocks.  
- **Higher-order schemes** (e.g., Lax–Wendroff) reduce diffusion in smooth regions but can **oscillate near discontinuities**.  
- **Godunov’s barrier theorem** says: for linear advection, any **linear monotone** conservative scheme is **at most first-order** accurate.  
  - Consequence: you can’t simultaneously have **linearity + monotonicity + >1st order**.  
  - Practical fix: **nonlinear** (solution-dependent) reconstruction via **limiters**.

**TVD/MUSCL** schemes “walk the line”:
- Become **first-order near shocks** (to keep monotonicity & stability).  
- Recover **second-order in smooth regions** (to reduce diffusion).  
- Limiters encode different compromises:
  - **minmod**: safest/most diffusive  
  - **van Leer**: balanced  
  - **Superbee**: sharpest/most compressive

---

## What’s inside

- `finite_volume_demo_commented.ipynb` – one notebook, short cells, heavy inline comments:
  1. **Linear Advection** `u_t + a u_x = 0` (periodic BCs)  
     - Upwind (donor-cell), Central (FTCS, for illustration), Lax–Wendroff  
  2. **Burgers’ equation** `u_t + (½u^2)_x = 0`  
     - **Godunov** finite-volume update with exact Riemann flux: correct shock/rarefaction handling  
  3. **MUSCL (TVD)** for advection  
     - Limiter comparisons: minmod, van Leer, Superbee

---

## Quick start

```bash
# create & activate an environment (optional)
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# install deps
pip install numpy matplotlib notebook

# run the notebook
jupyter notebook finite_volume_demo_commented.ipynb


