# wpi-njr-debug-results
## Overview
This repository contains the results of debugging efforts aimed at identifying the probable issue causing the Whole Program Inference (WPI) tool of the Checker Framework to not terminate on certain benchmarks from the NJR project. The main focus is on understanding why WPI does not terminate when inferring Nullness annotations on some [NJR benchmarks](https://zenodo.org/records/6314162), as reported in [Checker Framework Issue #6468](https://github.com/typetools/checker-framework/issues/6468). To investigate this, two experiments were conducted based on suggestions from Martin ([@kelloggm](https://github.com/kelloggm)) to narrow down the potential causes of the problem.

## Experiments Conducted
Two key experiments were performed to identify the likely cause of the non-termination issue:

1. **Contract Inference Test:** This experiment involved rerunning the test using a different typechecker to see if the contract inference code could be causing the problem. The Index Checker was chosen for this purpose, as it could induce a significant number of contracts. The results of this experiment are available in the `1-IndexChecker` directory.

2. **Monotonic Non-null Support Test:** To assess if the support for inferring monotonic non-null annotations was the issue, this feature was disabled by removing the code in `NullnessAnnotatedTypeFactory#wpiAdjustForUpdateField` and `NullnessAnnotatedTypeFactory#wpiAdjustForUpdateNonField`. The findings from this test are stored in the `2-NullnessWithoutMonotonicNull` directory.

## Summary of Results
Both experiments concluded with WPI terminating after 9 iterations, leading to the preliminary conclusion that the issue likely lies with the inference of `@MonotonicNonNull` annotations. This outcome suggests that while the problem seems to be related to `@MonotonicNonNull` inference, further investigation is necessary to uncover more detailed insights into the exact cause and potential solutions. 
