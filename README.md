# Multi-Agent Collaboration and VLM Action Controllers

**CS275 Artificial Life — Term Project, Spring 2026**  
University of California, Los Angeles

**Authors:** Athena Mo · Victor Lee · Zhao Xu · Ramnath Kumar

**Live page:** https://f26cs275.github.io/CS275-Project-Page

---

## Overview

This repository hosts the project webpage for our CS275 term project. We explore multi-agent collaboration and the use of Vision Language Models (VLMs) as a communication and control layer, built on top of the Unity ML-Agents *Pyramids* reinforcement learning environment.

**Three contributions:**

1. **Multi-agent role decomposition with MA-POCA** — Two heterogeneous agents (ButtonPresser and GoldCollector) are trained jointly using Multi-Agent POsthumous Credit Assignment. Role lock is enforced at the Unity collision layer so neither agent can solo the task.

2. **VLM action controller** — The trained PPO policy is replaced with Qwen2.5-VL (7B) running zero-shot via Ollama. The model receives an egocentric camera frame each step and returns a structured JSON with a scene description, high-level command, and low-level action. We find strong perception but poor real-time control (0.03–0.1 Hz vs Unity's 50 Hz physics).

3. **Three-stage curriculum learning** — A scalar `task_difficulty` parameter gates three lessons (gold-only → nearby switch → full task). Automatic advancement via ML-Agents' curriculum API yields a **61.9% win rate vs 18.4%** for the PPO + ICM baseline at matched compute (1.5M steps) — a 3.4× relative improvement.

---

## Repo structure

```
CS275-Project-Page/
├── index.html                          # Main project webpage
├── static/
│   ├── css/
│   │   ├── index.css                   # Custom styles
│   │   ├── bulma.min.css               # Bulma CSS framework
│   │   ├── bulma-carousel.min.css
│   │   ├── bulma-slider.min.css
│   │   └── fontawesome.all.min.css
│   ├── js/
│   │   ├── index.js                    # Page interactivity
│   │   ├── bulma-carousel.min.js
│   │   └── bulma-slider.min.js
│   ├── images/
│   │   ├── carousel1.jpg               # Pyramids environment overview
│   │   ├── carousel2.jpg               # MA-POCA multi-agent setup
│   │   ├── carousel3.jpg               # Curriculum reward curves
│   │   └── carousel4.jpg               # VLM egocentric camera view
│   ├── videos/
│   │   ├── curriculum_side_by_side.mp4 # Teaser: baseline vs curriculum side-by-side
│   │   ├── curriculum_success.mp4      # A complete successful curriculum episode
│   │   ├── curriculum_demo.gif         # Curriculum agent behavior loop (short)
│   │   ├── baseline_demo.gif           # Baseline agent behavior loop (short)
│   │   ├── curriculum_1M5.mp4          # Full curriculum training run (1.5M steps)
│   │   ├── baseline_1M5.mp4            # Full baseline training run (1.5M steps)
│   │   ├── vlmagent.mp4                # Single-agent VLM controller demo
│   │   └── vlm_simul_multi_agent.mp4   # VLM multi-agent simulation
│   └── pdfs/
│       └── CS275_Term_Project_Report.pdf   # Full project report
└── .github/
    └── workflows/
        └── static.yml                  # GitHub Pages auto-deploy
```

---

## Viewing locally

No build step required — open `index.html` directly in a browser:

```bash
# Python 3 simple server (avoids CORS issues with local videos/PDFs)
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## Submission contents

Per the CS275 submission requirements, the zip archive contains:

| Requirement | Location |
|---|---|
| Title, authors, abstract | `index.html` hero + abstract sections |
| Link to project report (PDF) | `index.html` → Paper button; `static/pdfs/CS275_Term_Project_Report.pdf` |
| Representative images with captions | `index.html` image carousel; `static/images/` |
| Video demos | `index.html` Videos section; `static/videos/` |
| Source code link | `index.html` → Code button → GitHub |

---

## Acknowledgments

We thank Professor Demetri Terzopoulos for instruction in CS275 Artificial Life, and the Unity ML-Agents team for the open-source framework and Pyramids environment.

Page template adapted from the [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template), originally based on [Nerfies](https://nerfies.github.io/).

---

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a>  
This website is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
