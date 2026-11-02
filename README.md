# CYBERSHIELD AI

**Predict. Protect. Recover.**

An educational, fully simulated cyber-defence prototype that models how a threat spreads through a virtual computer network and how a defender can contain it. Everything runs in the browser on synthetic devices. There is no real malware, no scanning and no connection to real machines.

## Live demo

Open `index.html` (or `cybershield.html`) in a modern browser. No install or build step is needed. An internet connection is required to load Three.js and the font from a CDN.

If GitHub Pages is enabled for this repository, the app is served at `https://maxx1626.github.io/CYBERSHIELD-AI/`.

## What it does

- **Login and register**: browser-local accounts with email validation and salted SHA-256 password hashing. A "judge demo" button starts a guided run without credentials.
- **3D network view** (Three.js): 30 to 100 virtual devices (desktops, laptops, servers, databases, routers, gateways) in five segments. Drag to rotate, scroll to zoom, click a device for details, and filter by ID, type or state.
- **Simulation lab**: five scenarios (single infection, multi-device spread, server threat, multi-segment risk, AI defence and recovery) with start, pause, resume, step, reset, speed control and a timeline scrubber. Runs are reproducible from a random seed.
- **SEIR model**: Susceptible, Exposed, Infected, Recovered states per device, driven by the generated network graph. Shows live counts, an R0 estimate and charts.
- **Risk prediction**: a GNN-style score that averages neighbour information over two hops with fixed weights.
- **Defence centre**: recommendations that need human approval. Approve isolation, block a simulated link, recover a device or reject, each with a confirmation dialog and an audit log.
- **Analytics**: session run history and a three-policy comparison (no defence, rule-based, risk-guided) replayed on the same seed.

## Honest status of the AI components

| Component | What is actually implemented |
|---|---|
| SEIR | Real stochastic SEIR simulation on the device graph. Rates (beta, sigma, gamma) are fixed model assumptions. |
| GNN | **Untrained baseline.** Hand-set message-passing weights, not a PyTorch Geometric model. Confidence reflects how much graph evidence exists, not whether a device is infected. |
| RL | **Not implemented.** The defence logic is a rule-based baseline and is labelled as such. |
| Benchmarks | Synthetic simulation measurements only, not real-world results. |

## Not yet built

The original master prompt describes a full-stack system. These parts are not in this prototype:

- FastAPI backend, SQLAlchemy database, Argon2/JWT authentication
- PyTorch / PyTorch Geometric GNN training
- Stable-Baselines3 RL policy
- WebSocket live updates
- Server-side PDF and CSV export (the export buttons are not wired up yet)
- Detection accuracy, prediction accuracy and false-alarm-rate metrics

## Roadmap

1. Move the simulation engine into a Python backend (`seir.py`, `gnn.py`, `reinforcement_learning.py`).
2. Replace the baseline risk score with a trained GNN.
3. Train an RL defence policy against the simulation environment and define its reward function in code.
4. Add real authentication, a database and WebSocket updates.
5. Add CSV and PDF report export.

## Safety

All devices, IP addresses (reserved documentation ranges `192.0.2.0/24` and `198.51.100.0/24`) and events are synthetic. The project must never be extended to target real systems.

## Tech

Single-file HTML, vanilla JavaScript, Three.js r128, Web Crypto API.

## Author

Mathivanan R, B.Tech CSE (AI & ML), SRM Institute of Science and Technology, Ramapuram.
