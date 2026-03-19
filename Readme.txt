================================================================================
  Assignment — Week 04 · Day 20  (AM + PM Sessions)
  PG Diploma · AI-ML & Agentic AI Engineering · IIT Gandhinagar
  Deadline: 19/03/2026 · 09:15 AM
================================================================================

REPOSITORY CONTENTS
-------------------

  W4_D20_AM_PythonOOP.ipynb     AM session notebook (Python Fundamentals / OOP)
  W4_D20_PM_NormalDist.ipynb    PM session notebook (Statistics / Hypothesis Testing)
  README.txt                    this file

Both notebooks are self-contained Colab files.
Open in Colab → Runtime → Run all.  The first cell installs all dependencies.


--------------------------------------------------------------------------------
AM SESSION  —  W4_D20_AM_PythonOOP.ipynb
Topics: Loops, While Loops, Dictionary, Tuple, *args, **kwargs, Classes, Dunders
--------------------------------------------------------------------------------

PART A — Concept Application (40%)

  A1. Max, Min, Frequency using loops only (no built-ins)
      - find_max(lst): starts at lst[0], walks through comparing each item.
      - find_min(lst): same pattern, opposite comparison.
      - count_frequency(lst): builds a dict manually — checks if key exists,
        increments or sets to 1. No Counter, no defaultdict.

  A2. While loop — reverse a number + palindrome check
      - reverse_number(n): repeatedly extracts last digit (n % 10),
        appends to result (result * 10 + digit), chops n (n // 10).
        Example: 12345 -> 54321
      - is_palindrome(n): returns n == reverse_number(n).
        Tests on: 123, 121, 1001, 12321, 456, 9009.

  A3. Tuples and Dictionaries
      - tuples_to_dict(tuple_list): iterates pairs, assigns pair[0]=key,
        pair[1]=value manually. No dict() constructor used.
      - key_with_highest_value(d): tracks best_key/best_value in a single
        pass — no max(), no sorted().

  A4. *args — sum and average without sum()
      - sum_and_average(*args): for-loop totals all args, counts them,
        divides. Returns (total, average) tuple.
      - Tested with 3-arg, 6-arg, and single-arg calls.

  A5. **kwargs — top student from keyword arguments
      - top_student(**kwargs): iterates over kwargs.items(), tracks
        best name/mark in a single pass — no max().
      - Prints full table with the winner marked "← TOP".

PART B — Stretch: Custom Vector class with Dunder Methods (30%)

  class Vector:
    __init__   : stores components as a tuple (immutable)
    __repr__   : "Vector(1, 2, 3)" style output
    __add__    : element-wise addition with dimension check
    __sub__    : element-wise subtraction with dimension check
    __mul__    : scalar multiplication (Vector * n)
    __rmul__   : reverse scalar multiplication (n * Vector)
    __eq__     : equality check on components tuple
    __len__    : count of dimensions using a loop (no len() inside)

  Tested with:
    - 3D vector addition, subtraction, scalar multiplication
    - Chain: (v1 + v2) * 2 - v3
    - 2D vectors
    - Dimension mismatch error (caught and shown)

PART C — Interview Ready (20%)

  Q1. *args vs **kwargs
      - *args: positional, collected as a tuple, for variable-count inputs
        with no names. Examples: print(), logging, math functions.
      - **kwargs: named, collected as a dict, for variable-count named
        settings. Examples: config functions, DB record builders.
      - Covers order rule: regular params → *args → **kwargs.

  Q2. Student class with grade and __str__
      - calculate_grade(): A >= 80, B >= 60, C below 60.
      - __str__(): formatted one-liner "Student: Ravi | Marks: 78 | Grade: B"
      - Tested on 6 students; top scorer grade verified standalone.

  Q3. Dunder methods
      - Definition: Python's hook system for built-in operations.
      - Why they matter: make custom objects behave like built-in types.
      - Three examples explained: __str__, __add__, __len__.
      - Also lists: __repr__, __eq__, __lt__, __getitem__, __iter__,
        __enter__/__exit__ with their triggers.

PART D — AI-Augmented Task (10%)

  Prompt: "Explain Python dunder methods with examples for beginners and
           include a custom class implementation."

  AI provided: BankAccount class with __init__, __str__, __repr__,
               __add__, __eq__, __gt__.
  Reproduced and verified: all 5 dunders worked correctly.
  Issues flagged:
    - __sub__ and __lt__ missing (acc1 < acc2 raises TypeError)
    - __add__ for 'merging accounts' is conceptually odd for a bank class
    - __enter__/__exit__ (context managers) omitted from the list


--------------------------------------------------------------------------------
PM SESSION  —  W4_D20_PM_NormalDist.ipynb
Topics: Normal Distribution, Standard Normal, Z-score, Hypothesis Testing
--------------------------------------------------------------------------------

PART A — Concept Application (40%)

  A1. Generate Normal(50, 10) dataset (n=1000), manual stats, histogram
      - manual_mean(): for-loop total / count.
      - manual_variance(): for-loop squared differences / count.
      - manual_std(): Newton's method (50 iterations) for sqrt.
      - All three verified against np.mean / np.var / np.std.
      - Histogram plotted with theoretical PDF curve overlaid.

  A2. Z-score conversion — manual implementation
      - compute_zscore(lst): applies (x - mean) / std to every element.
      - After transformation: mean = ~0.0 (verified to 8 decimal places),
        std = ~1.0 (verified to 8 decimal places).
      - Side-by-side plot: original vs standardised distribution.

  A3. Student marks dataset (30 values including outliers 2 and 105)
      - manual_median(): bubble sort + midpoint extraction.
      - Mean, median, variance, std computed and printed.
      - Outlier detection: any mark with |Z| > 2 flagged (broad),
        |Z| > 3 flagged (strict). Both shown with actual Z-values.
      - Histogram with outlier positions marked as dotted orange lines.

  A4. One-sample Z-test — fully manual
      - one_sample_z_test(sample, null_mean, alpha=0.05):
        computes sample mean, std, standard error, Z-statistic manually.
        Uses fixed z_critical = 1.96 (two-tailed, alpha=0.05).
        p-value from stats.norm.cdf (only scipy use — the math lookup).
        Prints full table and plain-English conclusion.
      - Tested on Normal(50,10) data with H0: mean=50 (should not reject).
      - Tested on student marks with H0: mean=65.

  A5. False positive rate simulation (1000 tests under H0 true)
      - Draws 1000 samples from Normal(50,10), tests H0: mean=50 each time.
      - Counts how many times |Z| > 1.96 (false rejections).
      - Estimated false positive rate ≈ 0.05 (5%) — matches alpha.
      - Confirms: alpha is literally the false positive rate you accept.

PART B — Stretch Problem (30%)

  B1. Normal vs Standard Normal — side-by-side plots
      - Generates Normal(70,15), standardises to N(0,1).
      - Two histograms with PDF curves overlaid.
      - Written comparison: shape (identical), x-axis scale (original vs
        Z-scores), when to use each.

  B2. Two-group hypothesis test (old vs new teaching method)
      - Group OLD: Normal(65,12) n=40. Group NEW: Normal(72,11) n=40.
      - Difference in means computed, t-test via scipy for verification.
      - Conclusion: new method produces significantly higher scores.
      - Overlapping histograms with group means marked.

  B3. When to standardise + why Z-score matters in ML
      - Four scenarios requiring standardisation: KNN/PCA, gradient
        descent, L1/L2 regularisation, neural network training.
      - Z-score importance: interpretability, outlier detection,
        statistical tests, feature importance comparisons.
      - When NOT to standardise: tree-based models.

PART C — Interview Ready (20%)

  Q1. Normal vs Standard Normal
      Full explanation with formula, relationship, probability lookup
      example, and when to use each.

  Q2. z_score(x, mean, std) function
      Applied to 20-value marks dataset. Outputs a table of every mark,
      its Z-score, and a plain-English interpretation (near average /
      above average / very low outlier etc.).

  Q3. Hypothesis testing — all four concepts
      H0, H1, p-value (with the common mistake clarified), alpha.
      Worked end-to-end numeric example included.

PART D — AI-Augmented Task (10%)

  Prompt: "Explain normal distribution, Z-score, and hypothesis testing
           with a simple Python example."

  AI output reproduced and verified on a 50-student exam score dataset.
  Code ran without errors.
  Issues flagged:
    - AI used stats.ttest_1samp without explaining when t-test vs Z-test
      is appropriate (n ≥ 30 makes them equivalent here, but not stated)
    - Z-score applied via list comprehension without explanation -- a for
      loop is clearer for beginners
    - H0 mean line not shown on histogram (added in our version)
    - False positive rate simulation (the most intuitive illustration of
      alpha) was not included by the AI at all

================================================================================
