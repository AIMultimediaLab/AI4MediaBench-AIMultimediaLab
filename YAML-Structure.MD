## Codalab Competition Definition Language
This page provides a detailed description of attributes within the Codalab competition definition language, which uses YAML. This language is utilized for creating configuration files in Codalab competition bundles.

## Competition Properties

**Required:**
- title: Title of the competition
- image: File path to the competition logo, relative to competition.yaml
- terms: File path to a markdown or HTML page containing the terms of participation participants must agree to before joining the competition

**Optional:**

- description: A brief description of the competition.
- registration_auto_approve: True/False. If True, participation requests will not require approval by competition administration (defaults to False).
- docker_image: Can specify a specific Docker image for the competition to use (defaults to codalab/codalab-legacy:py3).
- make_programs_available: Can specify whether to share the ingestion and scoring program with participants or not (always available to competition organizers).
- make_input_data_available: Can specify whether to share the input data with participants or not (always available to competition organizers).
- queue: Queue submissions are sent to; can be used to specify competition-specific compute workers (defaults to the standard queue shared by all competitions). The queue should be referenced by its Vhost, not by its name. You can find the Vhost in Queue Management, accessible via the eye button labeled "View Queue Detail."
- enable_detailed_results: True/False. If True, the competition will watch for a detailed_results.html file and send its contents to storage (more information available here).
- contact_email: A valid contact email to reach the organizers.
- reward: A string to indicate the reward of the competition (e.g., "$1000" for the competition).

```
version: 2
title: Compute Pi
description: Calculate pi to as many digits as possible, as quick as you can.
image: images/pi.png
terms: pages/terms.md
registration_auto_approve: True
make_programs_available: True
make_input_data_available: False
contact_email: organizer_email@example.com
reward: $1000 prize pool
```

## Pages

**Required:**

- title: String to be displayed as the title of the page on the competition detail page.
- file: File path to a markdown or HTML page relative to competition.yaml containing the desired content of the page.

Sample:
```
pages:
  - title: Welcome
    file: welcome.md
  - title: Getting started
    file: pages/getting_started.html
```

## Phases
**Required:**
- name: Name of the phase
- start: Datetime string for the start of the competition (ISO 8601 format recommended).
- end: Datetime string for the end of a phase (optional for the last phase only; if not supplied for the final phase, that phase continues indefinitely).
- tasks: An array of numbers pointing to the index of any defined tasks relevant to this phase (see tasks for more information).

*Optional:*
- index: Integer for noting the order of phases. Phases must be sequential without overlap. If indexes are not supplied, ordering will be assumed by declaration order.
- max_submissions: Total submissions allowed per participant for the entire phase.
- max_submissions_per_day: Submission limit for each participant for a given day.
- auto_migrate_to_this_phase: Cannot be set on the first phase of the competition. This will re-submit all successful submissions from the previous phase to this phase at the time the phase starts.
- execution_time_limit: Execution time limit for submissions, given in seconds (default is 600).
- hide_output: True/False. If True, stdout/stderr for all submissions to this phase will be hidden from users who are not competition administrators or collaborators.
- starting_kit: Path to the starting kit, a folder that participants can download, including useful files to help participants (example submissions, notebooks, documentation).
- public_data: Path to public data, which participants can download.
Sample:
```
phases:
  - index: 0
    name: Development Phase
    description: Tune your models
    start: 2019-12-12
    end: 2020-02-01
    execution_time_limit: 1200
    starting_kit: starting_kit
    public_data: public_data
    tasks:
      - 0
  - index: 1
    name: Final Phase
    description: Final testing of your models
    start: 2020-02-02
    auto_migrate_to_this_phase: True
    tasks:
      - 1
```

## Tasks
**Required:**
- index: Number used for internal reference of the task, pointed to by solutions (below) and phases (above).
- name: Name of the task
- scoring_program: File path relative to competition.yaml pointing to a .zip file or an unzipped directory containing the scoring program.

**Optional:**
- description: Brief description of the task.
- input_data: File path to the data provided during the prediction step.
- reference_data: File path to the data provided to the scoring program.
- ingestion_program: File path to the ingestion program files.
- ingestion_only_during_scoring: True/False. If true, the ingestion program will run in parallel with the scoring program and can communicate with the scoring program via a shared directory.
Sample:
```
tasks:
  - index: 0
    name: Compute Pi Development Task
    description: Compute Pi, focusing on accuracy
    input_data: dev_phase/input_data/
    reference_data: dev_phase/reference_data/
    ingestion_program: ingestion_program.zip
    scoring_program: scoring_program.zip
  - index: 1
    name: Compute Pi Final Task
    description: Compute Pi, speed and accuracy matter
    input_data: final_phase/input_data/
    reference_data: final_phase/reference_data/
    ingestion_program: ingestion_program.zip
    scoring_program: scoring_program.zip
```

## Solutions
**Required:**
- index: Index number of the solution.
- tasks: Array of the tasks (referenced internally) for which this solution applies.
- path: File path to .zip or directory containing the solution data.
Sample:
```
solutions:
  - index: 0
    path: solutions/solution1.zip
    tasks: 
      - 0
      - 1
  - index: 1
    path: solutions/solution2/
    tasks:
      - 0
```

## Fact Sheet
**Optional:**

JSON for asking metadata questions about each submission when they are submitted.

Sample Structure:
```
fact_sheet: {
    "[KEY]": {
        "key": "[KEY]",
        "type": "[QUESTION TYPE]",
        "title": "[DISPLAY NAME]",
        "selection": [SELECTION],
        "is_required": ["true" OR "false"],
        "is_on_leaderboard": ["true" OR "false"]
    }
}
```

Example Fact Sheet Questions:
```
"bool_question":
yaml
Copy code
{
  "key": "bool_question",
  "type": "checkbox",
  "title": "boolean",
  "selection": [True, False],
  "is_required": "false",
  "is_on_leaderboard": "false"
}
```

"text_question":
```
{
  "key": "text_question",
  "type": "text",
  "title": "text",
  "selection": "",
  "is_required": "false",
  "is_on_leaderboard": "false"
}
```

"text_required":
```
{
  "key": "text_required",
  "type": "text",
  "title": "text",
  "selection": "",
  "is_required": "true",
  "is_on_leaderboard": "false"
}
```

"selection":
```
{
  "key": "selection",
  "type": "select",
  "title": "selection",
  "selection": ["", "v1", "v2", "v3"],
  "is_required": "false",
  "is_on_leaderboard": "true"
}
```

## Leaderboards
Leaderboard Details 
**Required):**
- title: Title of the leaderboard.
- key: Key for the scoring program to write to.
- columns: An array of columns (see column layout below).

**Optional:**
- submission_rule: Determines the behavior of the leaderboard regarding new submissions (e.g., "Force_Last").
- hidden: True/False. If True, the contents of this leaderboard will be hidden from all users who are not competition administrators or collaborators.

## Column Details (Required):
- title: Title of the column.
- key: Key for the scoring program to write to. The keys must match the keys of the scores.json file returned by the scoring program (detailed explanation available here).
- index: Number specifying the order in which the column should appear on the leaderboard.

**Optional:**
- sorting: Sorting order for the column (e.g., "Descending" or "Ascending").
- computation: Computation to be applied, accompanied by computation indexes.
- computation options: Options like "sum," "avg," "min," "max."
- computation_indexes: An array of indexes of the columns to which the computation should be applied.
- precision: Integer to round the score to a specific number of digits (default is 2).

Sample:
```
leaderboards:
  - title: Results
    key: main
    submission_rule: "Force_Last"
    columns:
      - title: Accuracy Score 1
        key: accuracy_1
        index: 0
        sorting: desc
        precision: 2
      - title: Accuracy Score 2
        key: accuracy_2
        index: 1
        sorting: desc
        precision: 3
      - title: Max Accuracy
        key: max_accuracy
        index: 2
        sorting: desc
        computation: max
        precision: 3
        computation_indexes:
          - 0
          - 1
      - title: Duration
        key: duration
        index: 3
        sorting: asc
        precision: 2
```
This Markdown file provides a structured overview of the AI4MediaBench competition definition language, facilitating the creation of competition bundles for AI4MediaBench.
