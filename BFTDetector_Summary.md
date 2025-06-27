# ADMI25 Hackathon: BFTDETECTOR Project Summary

## 1. Key Findings & Methodology

### Project Overview

* Websites often use paywalls or ads for revenue.

* "Business Flow Tampering" (BFT) allows users to bypass these restrictions using browser tools or JavaScript.

* BFTDETECTOR is an automated tool designed to find these BFT flaws.

* The tool successfully found 315 problems on 204 websites, including major sites like TIME, Forbes, and Fortune.

* It demonstrated high accuracy: 0.5% false alarms and only 1.4% missed problems.

### Technical Tools Used

* Google's Puppeteer (for web browser control)

* Custom Chrome engine (for website inspection)

* Machine Learning (AI) (to spot success/failure)

* Code editing and "mutation" (for testing flaws)

### Example Cases

* **TIME.com:** BFTDETECTOR found a way to bypass article limits.

* **Bookmate.com:** The tool bypassed the paywall for premium book chapters.

### Methodology

1. **Visit Websites Normally and as a Hacker:** Browses a site twice – once as a regular user (e.g., with subscription), and once pretending to be a hacker (e.g., ads blocked).

2. **Compare Code:** Identifies where the normal and "hacked" versions of the website start behaving differently.

3. **Trick the Website:** Creates special code to "jump over" paywalls or ad checks.

4. **Verify Success:** Checks if the trick provided access to premium content or blocked ads without detection.

5. **AI Confirmation:** Uses machine learning to confirm if the tampered version was truly successful.

### Data & Accuracy

* **Websites Checked:** 352 real websites.

* **Tests Run:** 449 different tests (some sites had multiple paywalls).

* **Flaws Found:** 315 tests revealed actual flaws.

* **Breakdown of Flaws:**

  * 31 sites with hard paywalls

  * 67 sites with soft paywalls

  * 217 sites using ad blockers

* **Accuracy Metrics:**

  * False Positive Rate: 0.49%

  * False Negative Rate: 1.44%

### Mitigation Proposal

* Randomizing server-side JavaScript for critical logic can block repeated tampering.

* Their tests showed that randomizing key functions prevented both automated and manual tampering.

## 2. Common Issues Encountered During Reproduction

| Issue | What Happened | Why It Happened | Concern | Fix |
| ----- | ----- | ----- | ----- | ----- |
| **`pyhash` Installation Failure** | The `pyhash` program couldn't install. | It's made for older Intel computer chips, but your computer has a newer Apple Silicon chip. They're not compatible. | This program won't work on your Apple Silicon or Windows computer without special steps or a different program. | Try using a different program, or run your terminal with Apple's Rosetta 2 (Intel chip emulator). |
| **`networkx` Missing** | The main program couldn't find a tool called `networkx`. | The first attempt to install all programs didn't finish, so `networkx` was never put on your computer. | This problem should go away once the main installation is fixed. | Run: `pip install networkx` |
| **`scikit-image` Install Failed (Python 3.13)** | The `scikit-image` program failed to install. | The version (0.19.2) is old and doesn't work with newer Python (3.13) or related tools like `setuptools`. It tries to use an old method that Python 3.13 doesn't have anymore. | Your Python version is too new for this old program. | Use an older, more compatible Python version (e.g., Python 3.8 or 3.9). |
| **`numpy` Missing for `scikit-image`** | `scikit-image` couldn't install because `numpy` wasn't there first. | Some programs, like `scikit-image`, need `numpy` to be installed on your computer before they can even start their own installation. | Always put `numpy` on your computer before installing other complex science-related programs. | Run: `pip install numpy` |

## 3. Reproducibility Assessment

### BFT Detector Scorecard

| Metric | Rating | Explanation (Simple) |
| :------------------------------- | :----: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Paper Availability** | **3** | The paper was accessible, but the exact method wasn't clear, suggesting it wasn't a direct, easy find. |
| **Availability of Code and Software** | **3** | Code was on GitHub and cloned, but installation failed repeatedly due to very outdated instructions for modern Python. |
| **Availability of Datasets** | **2** | Datasets were mentioned but had no clear links or instructions, so we couldn't find or access them. |
| **Computer Requirements** | **3** | Specific OS and Python versions were required, and a crucial virtualization issue on the host made setting up a compatible environment very hard. |
| **GPU Requirements** | **1** | No GPU requirements were stated in the documentation, making it unclear if one was needed or not. |
| **Documentation Quality** | **2** | Instructions were outdated and caused extensive troubleshooting, forcing us to go far beyond the provided guide. |
| **Ease of Setup** | **2** | Setting it up was extremely challenging due to constant Python conflicts and an unfixable hardware barrier (BIOS virtualization). |
| **Reproducibility of Results** | **1** | We couldn't get the project to run at all, so we couldn't execute any experiments or verify the paper's claimed results. |
| **Overall Rating** | **2** | Can't run without major problems; needs expert help or significant workarounds. |

| Question | Answer |
| ----- | ----- |
| **Did the repo include all necessary code?** | Yes, the repository code was complete. |
| **Was the dataset public and accessible?** | No, the dataset was not explicitly public or accessible in the documentation. |
| **Were instructions up to date?** | No, instructions were outdated for modern Python environments (e.g., Python 3.13 vs. required 3.8/3.9). |
| **Any issues with dependencies or hardware?** | Yes, dependency conflicts (scikit-image, setuptools) and hardware virtualization issues (unable to enable in BIOS/UEFI) occurred. |
| **How close were your results to theirs?** | Unable to compare; project could not be run due to setup issues. |

**Reproducibility Rating: 2 out of 5 (Low Reproducibility)**

**Reasoning:**

* Significant issues were faced with environment setup (Python 3.13 vs. required 3.8/3.9).

* Dependency conflicts (scikit-image, setuptools) were prevalent.

* Unresolvable hardware/system barriers (inability to enable virtualization for Docker) were encountered.

* Even a cloud-based alternative (Gitpod) presented platform-specific setup issues.

* The project's instructions were not sufficiently up-to-date for modern environments, and the dataset was not readily accessible.
