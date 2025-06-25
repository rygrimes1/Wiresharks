# Fairify Tool Execution Report: German Credit (GC) Experiment 1

This report details the execution of the `./fairify.sh GC` command for the Fairify tool, documenting the observed progress, attempts to locate output files, and current status.

---

## 1. Preparation Steps

Prior to running the experiment, the following steps were consistently ensured:

* The terminal session was navigated to the main `~/Fairify/` directory.
* The `fenv` Python virtual environment was activated (indicated by `(fenv)` in the prompt).
* Necessary output directories (`~/Fairify/data/GC/res/` and later `~/Fairify/src/GC/libra/`) were created using `mkdir -p`.

---

## 2. Experiment Execution: `./fairify.sh GC`

The command `./fairify.sh GC` was executed from the `~/Fairify/src/` directory, as per the Fairify `INSTALL.md` instructions for Experiment 1. The run was initiated to process all models within the German Credit (GC) dataset, with each model configured for a maximum of 30 minutes.

**Observed Terminal Output During Execution:**

During the multi-hour execution (approximately 3 hours as reported by the user), the following pattern of output was consistently observed for each model or partition:

```
Started running verification for GC models.
Missing Data: XXX rows removed.
Number of partitions: XXX
==================  STARTING MODEL GC-X.h5
[TensorFlow CUDA warnings - ignored as no GPU is available]
INTERVAL BASED PRUNING
SINGULAR VERIFICATION
Pruning done!
Verifying ...
unknown
Pruning done!
XX.XX % HEURISTIC PRUNING
XX.XX % TOTAL PRUNING
Verifying ...
unknown
V time:  XXX.XXX
[Occasionally 'sat' results were observed, along with counterexample data (e.g., ['40', '6', ...])]
******************
==================  COMPLETED MODEL GC-X.h5
```

The presence of `Pruning done!`, `Verifying ...`, `unknown`/`sat` results, and `V time` indicates that the Fairify verification logic was actively running and processing the models. The script eventually completed its execution and returned to the command prompt.

---

## 3. Result Verification Attempts and Debugging

Despite the script running to completion, the generated CSV output files could not be located in the initially expected directories.

### Attempt 1: Checking `~/Fairify/data/GC/res/`

* **Command Executed:** `cd ~/Fairify/data/GC/res/`
* **Output:** `-bash: cd: /home/pi/Fairify/data/GC/res/: No such file or directory` (initially), or `total 0` after `mkdir -p` was used to create the directory.
* **Conclusion:** Files were not being written to this location.

### Attempt 2: Inspecting `Verify-GC.py` for Output Path

To determine the exact output path, the `Verify-GC.py` script was inspected.

* **Command Executed (from `~/Fairify/src/GC/`):** `cat Verify-GC.py | grep -E "open\(|csv"`
* **Relevant Output from Script:**
    ```python
    file = result_dir + model_name + '.csv'
    import csv
    with open(file, "a", newline='') as fp:
        wr = csv.writer(fp, dialect='excel')
        wr = csv.writer(fp)
    ```
* **Deduction:** The script dynamically constructs the output filename using `result_dir`. This `result_dir` variable, if not explicitly defined with an absolute path, resolves relative to the script's execution context.

### Attempt 3: Checking `~/Fairify/src/GC/libra/` (Based on Previous `FileNotFoundError`)

Based on earlier `FileNotFoundError` messages (`./libra/sex-AC-5.csv`), it was deduced that the script might be attempting to write to a `libra` subdirectory relative to its own location (`~/Fairify/src/GC/`).

* **Command Executed (from `~/Fairify/src/GC/`):** `mkdir libra` (to create the expected directory)
* **Command Executed (after run, from `~/Fairify/src/GC/libra/`):** `ls -l`
* **Output:** `total 0`
* **Conclusion:** Even after creating the `libra` subdirectory within `~/Fairify/src/GC/`, no CSV files were generated there.

---

## 4. Current Status and Conclusion

The Fairify tool successfully ran to completion for the German Credit (GC) dataset, as indicated by the progress logs and the final prompt return. However, despite multiple attempts to pre-create and locate the output directories based on the `INSTALL.md` and script inspection, **no CSV result files were found in either `~/Fairify/data/GC/res/` or `~/Fairify/src/GC/libra/`**.

This suggests a deeper issue with how the `result_dir` variable is resolved or how files are being written within the `Verify-GC.py` script. It's possible the script has an internal logic that prevents file writing under certain conditions or directs output to another, undiscovered location, or that the `result_dir` is still resolving to an unexpected or inaccessible path in the current environment. Further in-depth analysis of the `Verify-GC.py` script's internal logic and `result_dir` definition would be required to definitively pinpoint where the output is (or isn't) being written.
