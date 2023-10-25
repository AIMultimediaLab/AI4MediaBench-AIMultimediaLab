## Overview:
The creation of competitions has been streamlined through the implementation of a comprehensive wizard or form. This document elucidates each individual tab found within the competition creation form, aligning each with its respective section, and details the fields associated with each section.

## Details:
The "Details" tab encompasses fundamental information about the competition, including the title, logo, description, and the queue utilized.
- Title: This pertains to the official title of the competition.
- Logo: The designated logo representing the competition.
- Description: A comprehensive description outlining the nature and objectives of the competition.
- Queue: If a queue has been previously established via queue management, it can be associated with the competition at this juncture.

## Participation:
The "Participation" tab is dedicated to stipulating the terms and conditions governing competition participation, as well as settings for automatic participant approval.
- Terms: This section allows for the stipulation of the terms and conditions applicable to the competition.
- Auto Approve Registration: When selected, this option negates the necessity for organizer approval in the case of new participant registrations.

## Pages:
Under the "Pages" section, you are afforded the opportunity to integrate supplementary content that you wish to present to competition participants as dedicated pages. These pages are accessible through tabs on the competition detail page.

Upon selecting "Add Page," a modal window will appear, prompting the input of the following details:
- Title: The title for the page you are introducing.
- Content: The content of your page, which should be formatted using Markdown.

## Phases:
The "Phases" section empowers you to define the distinct phases of your competition and associate tasks with each.

Selecting "Add Phase" initiates a modal for phase creation, where you must specify:
- Name: The name ascribed to the phase.
- Start: The initiation date of the phase.
- End: The concluding date of the phase.
- Tasks: This is the area where you can assign one or multiple task objects to the phase. Tasks represent problems that submitted solutions are expected to address. Additional information about competition structure can be found here. If no tasks have been created yet, you can click the green button at the bottom of the new phase modal, titled "Manage Tasks/Datasets."
- Description: A comprehensive description of the phase.

**Advanced**:

- Execution Time Limit: This parameter dictates the maximum allowable execution time for submissions, measured in seconds. (Note: The label may incorrectly state that it's measured in milliseconds; this is not accurate.)
- Max Submissions per Day: Specifies the maximum number of submissions allowed for the phase within a 24-hour period, calculated from midnight UTC to midnight of the following day UTC.
- Max Submissions per Person: This defines the absolute maximum number of submissions a participant can make within the context of this phase.

## Leaderboards
The "Leaderboards" section facilitates the configuration of leaderboards that govern the scoring of submissions.

Upon selecting "Add Leaderboard," a modal window will emerge, soliciting the following details:
- Title: The title assigned to the leaderboard.
- Key: A distinctive name used to reference this leaderboard, preferably in lowercase.

Adding a column will introduce fields for column values, including:
- Title (Unlabeled top input): The designated title for the column.
- Primary Column: An indicator specifying whether this column serves as the primary column within the leaderboard. In essence, it determines whether it represents the sum or average of other columns.
- Computation (None/Average): If "Average" is chosen, this column should not receive direct score submissions; instead, it will compute the average of all other columns.
- Sorting: Defines the sorting order for scores in this column.
- Column Key: A unique identifier used to reference this column.

## Collaborators
This section facilitates the addition of other Codalab users as administrators for your competition.

Similar to other pages, selecting "Add Collaborator" prompts the appearance of a modal window. The search text can either be the user's email or their username, if known.
