# Wiresharks: Reproducibility Project for HACKHPC@ADMI25

This document outlines the Wiresharks team's project for the HACKHPC@ADMI25 Hackathon, detailing our goals, team structure, process, and findings in reproducible science.

## Project Overview

Our core objective for the ADMI25 Hackathon is to delve into the critical area of **reproducible science** within computing research. As Team Wiresharks, we are undertaking the hands-on task of reproducing existing scientific projects hosted on GitHub. Our primary aim is to thoroughly assess how straightforward or challenging it is for others to replicate previously published research.

## Our Goals

Our main goal is to **evaluate how easy it is to reproduce existing papers with code repositories**. We do this by answering key questions:

* **Did the repo include all necessary code?**
* **Was the dataset public and accessible?**
* **Were instructions up to date?**
* **Any issues with dependencies or hardware?**
* **How close were your results to theirs?**

By documenting every step and challenge, we assign a reproducibility rating, offering insights into practical scientific replication.

## How We Address Reproducible Science

Our project directly addresses reproducible science by:

* **Attempting to Replicate:** We try to rebuild and run existing research projects.
* **Evaluating Challenges:** We identify common roadblocks like outdated instructions, Python version issues, and missing datasets.
* **Providing Feedback:** Our detailed reports and ratings help the scientific community understand what makes a project truly reproducible.

## Team Wiresharks

Our team consists of four members from Hampton University:

* **Auiana D'Avilar** - Slide Guru (prepares presentation visuals)
* **Ayinde Hooks** - Scribe (documents everything)
* **Howard "Shiloh" Ames** - Coder and Portal Builder (reproduces code, sets up environment, builds web portal)
* **Ryan Grimes** - Coder and Portal Builder (reproduces code, sets up environment, builds web portal)


## Our Process (Hackathon Schedule)

Our hackathon plan is structured across several days for systematic evaluation:

### Day 1: Kickoff & Understanding

* Assign Roles, Read Paper, Skim GitHub Repo.

### Day 2: Environment Setup

* Install Dependencies, Run Sample Code, Note Challenges.

### Day 3: Reproduction Attempt

* Run Main Experiments, Compare Results, Record Differences, Scribe Documentation.

### Day 4: Build & Deliverables

* Rate Reproducibility (1-5), Build Portal, Test Portal, Polish Slides, Practice Presentation.

## How We Evaluated HPC Papers

We picked papers with code from areas like HPC or data science (e.g., from ICSE conferences). We used a detailed checklist to score them on:

* **Paper Availability:** Can you get the paper (e.g., free online)?
* **Code & Software:** Is the code on GitHub with setup steps?
* **Datasets:** Is the data available and described?
* **Computer Needs:** What hardware (CPU, memory) is required?
* **GPU Needs:** Are special GPUs needed, and what kind?
* **Documentation Quality:** Are the instructions clear and helpful?
* **Ease of Setup:** How simple is it to get the project running?
* **Reproducibility of Results:** Can we get the same answers as the paper?

## What We Learned (Key Takeaways)

Making science reproducible is hard! For projects to be easier to reproduce, they need:

* **Clear, up-to-date instructions.**
* **Easy-to-get data** (or clear alternatives).
* **Simple setup steps** (e.g., using tools like Docker).
* **No assumptions** about what computers users have.

## Technology Used

* **Programming Languages:** Python, JavaScript
* **Core Libraries/Frameworks:** TensorFlow/Keras, Numpy, Z3, Poetry, Bandit, scikit-image
* **Automation/Virtualization:** Google Puppeteer, Docker (attempted), `pyenv`
* **Environment:** Kali Linux (WSL)

Thank you for visiting our repository! We hope our work contributes to a better understanding of reproducible research practices.
```
