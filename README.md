# Pupil Dilation and Reading Comprehension in OneStop

Course project for Language, Computation and Cognition (00960222), Technion, Spring 2026.

Authors: Elad Rubani and Naama Inbar

## What this project is about

We check whether pupil size during reading carries information about reading
comprehension, using the OneStop eye-tracking dataset (360 readers, one of the
datasets in EyeBench). Pupil size is a known measure of cognitive effort, but it
is rarely used in work on reading comprehension.

Main findings:

- Pupil tracks word difficulty (surprisal and frequency), but only after centering
  pupil within each reader, and it drifts strongly from the start to the end of
  each passage.
- The average pupil over a whole passage says nothing about whether the question
  was answered correctly.
- Pupil is higher on the words that hold the answer (the critical span), and this
  effect comes almost entirely from readers who saw the question before reading.
  For these readers the critical words can be located from pupil above chance.
- The link between pupil on the critical span and answering correctly is weak.

The full description is in the project report.

## Files

- `pupil_onestop.ipynb` - the whole analysis, saved with its outputs, so all the
  numbers and figures in the report can be seen without running anything.
- `requirements.txt` - the Python packages the notebook uses.

The data is not in this repository. The notebook downloads it (see below).

## Notebook structure

- **Every Session: Mount Drive** - mounts Google Drive and checks which files exist.
- **Run Once: Download the Data** - downloads the OneStop word-level file.
- **Stage 1: Data Preparation and Pupil Characterization** - preprocessing, word
  difficulty, the position drift, and the whole-passage pupil vs. comprehension.
- **Stage 2: Critical Span Analysis** - pupil on the critical, distractor and rest
  words, artifact checks, and the link to comprehension.
- **Stage 3: Reading With and Without the Question** - the same contrast split by
  reading regime, the decoding test, and a robustness check.

## How to run

The notebook was written for Google Colab and saves its files to Google Drive.

1. Open `pupil_onestop.ipynb` in Google Colab.
2. Run the **Every Session: Mount Drive** cell and approve the Drive access.
3. Only the first time: run the **Run Once: Download the Data** cell. It downloads
   the OneStop word-level reading measures from OSF (about 380 MB zipped, about
   5.4 GB unzipped) into `MyDrive/eyebench_data/`, so about 6 GB of free Drive
   space is needed.
4. Run the rest of the cells in order. Stage 1 Section 2 (preprocessing) reads the
   large raw file and takes a few minutes. It saves two smaller tables to Drive
   that the later sections use.

Notes:

- The sections depend on each other, so they should be run from top to bottom.
- If the preprocessing in Stage 1 Section 2 is rerun, Stage 2 Section 2 (the span
  flags) has to be rerun too.
- The decoding test in Stage 3 uses a fixed random seed, so the results are
  reproducible.

## Data

OneStop: Berzak et al. (2025), "OneStop: A 360-participant English eye tracking
dataset with different reading regimes", Scientific Data.
We use the precomputed word-level reading measures (`ia_Paragraph.csv`), the same
file that EyeBench uses for OneStop.

EyeBench: Shubi et al. (2025), "EyeBench: Predictive modeling from eye movements
in reading", NeurIPS Datasets and Benchmarks Track. https://eyebench.github.io/
