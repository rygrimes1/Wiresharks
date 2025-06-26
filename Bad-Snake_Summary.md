# ADMI25 Hackathon: Bad Snakes Project Summary

## 1. Key Findings & Methodology

### Project Overview

* The "Bad Snakes" project investigates malicious packages on PyPI, a significant threat to software supply chains.
* The research evaluates existing tools designed to detect malware within PyPI packages.
* It aims to provide insights to enhance PyPI's overall malware detection capabilities and security.
* The study analyzes the effectiveness of various detection tools against different sets of packages (malicious, popular, random).

### Technical Tools Used

* Bandit: A widely used security linter for Python code.
* OSSGadget OSS Detect Backdoor: A tool specifically for backdoor detection.
* PyPI Malware Checks: Refers to general tools used by the PyPI Warehouse for security.
* Python Poetry: Utilized for dependency management and creating isolated Python environments.
* Jupyter Notebooks: Used by the original authors to outline and execute analysis steps.

### Example Cases (Our Reproduction Experience)

* **Environment Setup Success:** We successfully configured a Python environment using Poetry, managing dependencies and resolving minor Python version issues.
* **Tool Functionality Demonstration:** We were able to execute `bandit` on a small, locally created dummy Python file, confirming the basic functionality and setup of the scanning tools.
* **Dataset Unavailability (Critical Issue):** The core limitation was the explicit absence of the original malicious, popular, and random PyPI package datasets. This prevented any quantitative reproduction of the paper's reported accuracy metrics and findings.

### Methodology

The methodology of the "Bad Snakes" paper broadly involves:
* **Dataset Curation:** Compiling lists of malicious, popular, and random Python package names and versions from PyPI.
* **Package Acquisition:** (Performed by authors, not publicly reproducible) Downloading the actual `.whl` or `.tar.gz` package files based on the curated lists.
* **Tool Execution:** Running various static analysis and malware detection tools (e.g., Bandit, OSSGadget) against the acquired package files.
* **Result Analysis:** Evaluating the performance and effectiveness of these tools based on their ability to identify malicious code and their reported detection rates.

### Data & Accuracy

* **Datasets:** The project utilizes three types of PyPI package datasets: malicious, popular, and random.
* **Data Accessibility:** The **raw package data is not available** for public download due to licensing and PII concerns, severely limiting full reproduction.
* **Accuracy Metrics:** The paper reports standard accuracy metrics (True Positives, False Positives, False Negatives, False Negative Rate, False Positive Rate) for various tools.
* **Our Reproduction:** Due to the missing datasets, we **could not reproduce or verify** these quantitative accuracy metrics.

### Mitigation Proposal

The "Bad Snakes" paper itself does not propose a specific technical mitigation tool, but rather evaluates existing detection methods. The **implied mitigation proposal** stemming from its findings is:
* To leverage the insights gained from the evaluation to improve the automated malware detection mechanisms within the PyPI ecosystem, enhancing its overall security posture against supply chain attacks.

## 2. Common Issues Encountered During Reproduction

| Issue                                     | What Happened                                                                                                        | Why It Happened                                                                                                                                                                                                            | Concern                                                                                                                          | Fix (or Attempted Fix)                                                                                                                                       |
| :---------------------------------------- | :------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Python Version Incompatibility            | The project required Python 3.8/3.9, but our system had Python 3.13.                                                 | Project dependencies (like older TensorFlow versions in related contexts) are often tied to specific Python versions, and newer versions introduce breaking changes.                                                      | The project couldn't run correctly or install dependencies without the specific Python version.                                  | Attempted to manage Python versions using `pyenv` and explicit version installations.                                                                          |
| `scikit-image` Install Failed             | The `scikit-image` program (version 0.19.2) failed to install.                                                       | This older version is incompatible with newer Python (e.g., 3.13) and potentially newer `setuptools` versions, attempting to use deprecated installation methods.                                                          | A critical dependency could not be installed, preventing the project from running.                                               | Required using an older, more compatible Python version (e.g., 3.8 or 3.9) and potentially specific `setuptools` versions.                                      |
| `setuptools` Dependency Conflict          | `setuptools` versions caused installation failures.                                                                  | Newer `setuptools` versions often break compatibility with older packages that rely on legacy build processes.                                                                                                            | Dependencies couldn't resolve, stopping the installation process.                                                                | Explicitly installed an older, compatible version: `pip install "setuptools<58.0.0"`.                                                                         |
| Hardware Virtualization (Docker Issue)    | Docker Desktop for Windows (required for WSL integration) could not run due to disabled hardware virtualization.     | The system's BIOS/UEFI had virtualization extensions (VT-x or AMD-V) disabled, which are mandatory for virtualization software like Docker.                                                                                  | Docker containers, which might be necessary for environment isolation or specific tool execution, could not be used.             | **Unresolved:** Manual manipulation of BIOS/UEFI was required but could not be performed, leading to a dead end for Docker-based reproduction.                   |
| Platform-Specific Issues (Gitpod Attempt) | Encountered setup issues even when attempting to use cloud-based Gitpod for reproduction.                            | While cloud environments aim for consistency, they can have their own specific configurations, pre-installed software, or limitations that diverge from local setup expectations.                                         | The alternative reproduction path also faced roadblocks, indicating broader environmental sensitivity.                       | No general fix, as issues were platform-specific; would require deeper debugging within Gitpod's environment.                                                  |
| Missing Datasets                          | The original raw PyPI package datasets were not available for download.                                              | Authors cited licensing restrictions and PII (Personally Identifiable Information) concerns as reasons for not distributing the raw data.                                                                                | Prevented quantitative reproduction and verification of the paper's key findings (e.g., accuracy metrics).                   | **Unresolved for full reproduction:** Could only demonstrate tool functionality on dummy data, not reproduce original results.                                   |


## 3. Reproducibility Assessment

| Question                                    | Answer                                                                                                                                                                                                                               |
| :------------------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Did the repo include all necessary code?      | Yes, the GitHub repository included all the source code for the analysis tools and scripts.                                                                                                                                            |
| Was the dataset public and accessible?        | No, the specific raw PyPI package datasets used in the paper were explicitly stated as not being publicly distributed or accessible due to licensing and PII concerns.                                                                   |
| Were instructions up to date?                 | No, the instructions were largely outdated for modern Python environments (e.g., requiring Python 3.8/3.9 while our system had 3.13) and did not fully account for dependency conflicts or specific setup nuances.                       |
| Any issues with dependencies or hardware?     | Yes, significant dependency conflicts (e.g., `scikit-image`, `setuptools`) and unresolvable hardware/system barriers (inability to enable virtualization for Docker) were encountered.                                                    |
| How close were your results to theirs?        | We were **unable to compare** our results to theirs. Due to critical setup issues, dependency conflicts, and the unavailability of the datasets, the project could not be run to produce any comparative output files.                  |

## **Reproducibility Rating:** 2 out of 5 (Very Difficult)

### **Reasoning:**
The "Bad Snakes" project received a reproducibility rating of **2 out of 5 (Very Difficult)**. This classification indicates that the artifact "can't run without major problems" and "needs expert help or significant workarounds" to attempt reproduction. While the core code was available, the following factors contributed to this low rating:

* **Significant Environment Setup Issues:** Persistent challenges were faced with Python version compatibility (e.g., Python 3.13 vs. required 3.8/3.9) and resolving dependency conflicts (`scikit-image`, `setuptools`).
* **Unresolvable Hardware/System Barriers:** A critical roadblock was the inability to enable hardware virtualization necessary for Docker to function, which potentially prevented running parts of the analysis in isolated environments. Even attempting cloud-based alternatives like Gitpod introduced platform-specific setup issues.
* **Outdated Instructions:** The project's documentation was not sufficiently comprehensive or up-to-date for modern computing environments, lacking clear guidance for Python version management and intricate dependency resolution.
* **Crucial Missing Datasets:** Most importantly, the explicit unavailability of the original raw PyPI package datasets used in the paper's experiments rendered a full, quantitative reproduction of the published results impossible. While the tools could be functionally demonstrated on small, dummy data, verifying the paper's core findings (e.g., accuracy metrics) was not feasible.

