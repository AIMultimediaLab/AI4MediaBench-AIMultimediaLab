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

'''
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
'''
