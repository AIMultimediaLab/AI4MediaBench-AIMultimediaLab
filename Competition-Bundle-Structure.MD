## Overview
A competition bundle represents a structured archive, typically in the form of a zip file, which encompasses vital components of your competition. These components include the competition.yaml file, which defines critical aspects and attributes of the competition, as well as supplementary elements such as the competition logo, HTML or Markdown pages documenting the competition, and the requisite data associated with the competition.

## What is a Competition?
A competition comprises one or more phases that delineate the active periods within the competition's timeline. These phases are equipped with specific configurations, including execution time limits. Each phase, in turn, may feature one or more tasks, each task representing a problem that submitted solutions aim to solve. In essence, submissions addressing a task can be viewed as solutions. A task encompasses essential components, such as reference data, input data, a scoring program, and an ingestion program. Additionally, for a deeper understanding of the various types of data involved, refer to the lower section of this page.

## Example Competition Bundle Layout:

Please note that files can be organized within a directory; however, they must be referenced using their full path in the YAML configuration. Further details can be found in the "Competition YAML" section below.
```
--\ example_competition.zip
  |
  |- competition.yaml
  |- logo.png
  |- example_reference_data.zip
  |- example_scoring_program.zip
  |- example_solution.zip
  |- overview.md
  |- evaluation.md
  |- terms_and_conditions.md
  |- data.md
```

## Example competition.yaml:
```
title: Example Competition Submit Scores
description: An example competition where submissions should output the score they want
image: logo.jpg
terms: terms.md
pages:
    - title: overview
      file: overview.md
    - title: evaluation
      file: evaluation.md
    - title: terms
      file: terms_and_conditions.md
    - title: data
      file: data.md
phases:
    - index: 0
      name: First phase
      description: An example phase
      start: 2018-03-01
      end: 2027-03-01
      tasks:
        - 0
tasks:
    - index: 0
      name: First Phase Task
      description: Task for the first phase
      scoring_program: example_scoring_program.zip
      reference_data: example_reference_data.zip
solutions:
    - index: 0
      path: example_solution.zip
      tasks:
        - 0
leaderboard:
  - title: Results
    key: main
    columns:
      - title: score
        key: score
        index: 0
        sorting: desc
```

## Competition YAML
The competition.yaml file takes precedence as the central document within the bundle. It serves as the primary reference for AI4MediaBench to ascertain the structural framework of your competition, along with supplementary specifics.

## Data Types And Their Role:
### Reference Data:
Reference data, in most cases, represents the ground truth data against which participants' predictions are evaluated.

### Scoring Program
The scoring program is the script executed to determine submission scores, often relying on prediction outputs or submission results compared with reference data. Typically, this script is written in languages like Python, but it can be of various formats.

This script is accompanied by a metadata.yaml file that includes a key command, correlating with the command used to execute the scoring program. Special directories may also be accessible. For instance, a metadata.yaml may resemble the following:
```
command: python3 /app/program/scoring.py /app/input/ /app/output/
```
This command indicates that the scoring program (usually located at /app/program/scoring.py) is executed with Python 3 and operates on input data, which may contain user results or ingestion-generated predictions. The results are placed in the output folder, which is also specified as an argument. While arguments are optional, they can enhance convenience.

The scoring program generates a scores.json file, featuring results for each leaderboard column. After processing a submission, this file typically resembles the following:
```
{"accuracy": 0.886, "duration": 42.4}
```
The keys in this file should correspond to the leaderboard column keys defined in the competition.yaml file.

The scoring program may also produce detailed results as HTML files for each submission.

### Ingestion Program
The ingestion program is executed to generate predictions from submitted solutions when required. Like the scoring program, it is generally a script, often written in Python, although other formats are acceptable.

The ingestion program is complemented by a metadata.yaml file specifying the execution details. The metadata.yaml should include a key command, indicating the command used to run the ingestion program. Similar to the scoring program, special directories are accessible. An example of an ingestion metadata.yaml is as follows:
```
command: python3 /app/program/ingestion.py /app/input_data/ /app/output/ /app/program /app/ingested_program
```
As demonstrated above, this specifies the use of Python to run the ingestion program. It's worth noting that passing these directories as arguments is not obligatory but can be advantageous.

### Input Data
Input data typically represents the test data used to generate predictions from user code submissions, particularly when coupled with an ingestion program.
