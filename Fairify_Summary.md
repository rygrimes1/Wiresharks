# Fairify: Fairness Verification of Neural Networks

This document provides a summary of the Fairify project, a tool designed for the fairness verification of neural networks, primarily referencing paper `Fairify: Fairness Verification of Neural Networks (2022)` by Sumon Biswas and Hridesh Rajan.

## 1. Key Findings & Methodology

### Project Overview

* **Main Problem:** Artificial Intelligence (AI) models are increasingly used for significant decisions, but they can exhibit unfair biases. Fairify is a tool developed to systematically check these models for fairness.

* **What is Fairness?** Fairify specifically focuses on "individual fairness." This concept ensures that similar individuals should receive similar outcomes from an AI model, regardless of their sensitive background traits (e.g., race, gender, age).

* **Fairify's Solution:** It employs a sophisticated computational method to formally verify AI models for fairness. It tackles the complexity of verification by breaking down the problem into smaller parts and "trimming" the AI model to accelerate the checking process.

* **Results:** Fairify demonstrated significant effectiveness. When tested on 25 real-world AI models, it successfully identified fairness issues or confirmed the absence of bias much faster than alternative methods (completing tasks in minutes rather than days).

* **Deliverables:** The tool can provide either a "fairness certificate" (proof that the model is fair) or specific "unfair examples" (counterexamples), enabling developers to precisely locate and correct biased behaviors in AI systems.

### Technical Tools Used

* **Code Language:** Primarily Python.

* **AI Building Tool:** Keras (used for constructing the neural network models that Fairify verifies).

* **Logic Solver:** Z3 (a specialized Satisfiability Modulo Theories (SMT) solver that Fairify uses to solve the underlying logical puzzles involved in finding fairness issues).

* **Data Handling:** Numpy (utilized for efficient numerical operations and structuring the data within the AI models).

### Methodology

Fairify's verification process involves several key steps:

1. **Input Partitioning (Divide and Conquer):**

   * The tool divides the vast space of possible inputs for the AI into numerous smaller, more manageable segments.

   * This strategy transforms each fairness check into a smaller, simpler problem, allowing many checks to be performed concurrently.

2. **Sound Pruning (Provable Smart Trimming):**

   * For each input segment, Fairify analyzes the AI model to identify any "neurons" or parts that will remain inactive (i.e., not contribute to the decision) for that specific input range.

   * These inactive parts are then demonstrably removed, making the AI model more compact and faster to verify without altering its original decision-making logic.

3. **Heuristic Based Pruning (Estimated Clever Trimming):**

   * If "Sound Pruning" alone isn't sufficient to simplify the model, Fairify employs an estimation-based approach.

   * It runs the AI model multiple times with various inputs to pinpoint parts that are consistently inactive.

   * More parts are carefully removed based on these estimations, with efforts made to preserve the AI's accuracy.

### Example Verification Task

Consider verifying an AI model used for credit decisions to ensure fairness regarding a protected attribute like race:

* **Fairify's Steps:**

  * It takes the AI's inputs and systematically splits them into smaller segments.

  * For each segment, it simplifies the AI model by removing irrelevant parts.

  * Then, it queries the underlying logic solver (Z3) to determine if any unfairness exists within that simplified part of the AI.

* **Unfair Example Found:** If unfairness is detected, Fairify can identify a hypothetical pair of individuals who are identical in all aspects except for their race, yet receive different credit outcomes from the AI. This clearly flags a bias that needs correction.

### Data

* **AI Models Checked:** Fairify was tested on 25 diverse, real-world AI models.

* **Source of Models/Data:** These models and their associated testing data were collected from various sources, including data science platforms like Kaggle and academic research papers.

* **Types of Data Used in Models:**

  * **Bank Marketing:** Data related to bank customers, used to predict their likelihood of signing up for a service.

  * **German Credit:** Information about individuals applying for loans, used to predict credit risk.

  * **Adult Census:** U.S. census data, used to predict if an individual earns over $50,000 annually.

* **AI Model Type:** The verified AI models primarily consisted of simple, fully connected neural networks, which are common architectures for fairness evaluations on structured data.

* **Availability:** All the AI models and testing data are provided within the Fairify GitHub package, making them accessible for others to use and reproduce.

### Mitigation Proposal / Practical Utilities

Fairify offers several practical advantages for addressing and preventing AI bias:

* **Precise Problem Identification:** The tool can pinpoint the exact locations and conditions under which an AI model exhibits unfair behavior. This helps developers understand precisely which data points or model components require adjustment.

* **Accelerated Checking:** Fairify significantly speeds up the fairness checking process, even for complex AI models, moving from days to minutes.

* **Partial Guarantees:** Even if a comprehensive check of the entire AI model is not feasible, Fairify can provide formal guarantees that specific parts of the model adhere to fairness criteria.

* **Confident AI Deployment:** Developers can confidently deploy "trimmed" (pruned) and formally verified AI models, assured that they have undergone rigorous fairness checks.

## Fairify Scorecard

| Metric | Rating | Explanation |
| :------------------------------- | :----: | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Paper Availability** | **4** | The research paper (`Fairify`) was easily found and accessed, and its GitHub repo was clearly referenced. |
| **Availability of Code and Software** | **4** | The project's code was publicly available on GitHub, and we could clone it. All necessary parts were there. |
| **Availability of Datasets** | **5** | All AI models and testing data, including German Credit (GC), were provided within the GitHub package and were accessible. |
| **Computer Requirements** | **3** | It required a specific older Python version (3.9) not standard on our modern Kali system, needing special `pyenv` setup. |
| **GPU Requirements** | **5** | No GPU was strictly needed; the tool successfully ran using only the CPU, even with TensorFlow warnings. |
| **Documentation Quality** | **2** | Instructions were insufficient for common setup issues (like Python version fixes, `pyenv` setup, and missing output folders), requiring much external troubleshooting. |
| **Ease of Setup** | **2** | Setting it up was very difficult due to Python version conflicts, `pyenv` setup issues, and the persistent problem of results not being saved. |
| **Reproducibility of Results** | **1** | Even after the script ran for hours, no result files were generated. We could not get the project to produce verifiable output, making true reproduction impossible. |
| **Overall Rating** | **3** | Can be run with some effort; requires troubleshooting or minor fixes. |

## Fairify Project Rating: 3/5 (Doable)

The Fairify project received an overall reproducibility rating of **3 out of 5 (Doable)**.

**Reasoning:**

* **Code and Data Accessible:** A major positive was that the paper, all necessary code, and the datasets were readily available, which allowed us to start the reproduction process.
* **Python Version Challenges:** We faced significant issues due to a required older Python version (Python 3.9 for TensorFlow 2.5.0) which conflicted with our system's newer Python 3.13. This demanded extra effort using `pyenv`.
* **Complex Setup:** Getting the environment ready was challenging, including manual `pyenv` setup, installing specific libraries, and dealing with virtual environment issues.
* **No Output Files:** The most critical problem was that even after the script ran for hours, **it never generated any output CSV files**. This prevented us from being able to compare our results to the paper's claims, making full reproduction impossible.
* **Outdated Instructions:** The project's instructions were not complete for modern setups, lacking clear guidance for Python version management and where to create output folders.

---

*This summary references information from the paper `Fairify: Fairness Verification of Neural Networks`. by Sumon Biswas and Hridesh Rajan*
