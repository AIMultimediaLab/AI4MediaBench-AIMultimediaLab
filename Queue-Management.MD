## Overview
The queue management page lists all queues you have access to, and optionally all current public queues. For queues you've created, it will also show options for editing, deleting, and copying and displaying the broker url. You can also create new Queues from this page. You can use the server status page to have an overview of the submissions made to a queue you own.

### Show Public Queues
Enabling this checkbox will display public queues as well as queues you organized, or have been given access to. You will not be able to edit them, but you can view queue details and copy the broker url.

### Create Queue
Clicking this button will bring up a modal with the queue form.

The following fields are present:
- Name: The name of the queue
- Make Public: If checked, this queue will be available for public use.
- Collaborators: A multi-select field that you can search for users by username or email. These will be people who have access to your queue.

## Action Buttons
### Eye Icon
Clicking this button will show you details about your queue such as the Broker URL and Vhost name.

### Document Icon
The document icon is used to copy the broker url to your clipboard with one-click.

### Edit Icon
The edit icon brings up the queue modal/form for editing the current queue.

### Trash Icon
The trash icon deletes the current queue. There will be a confirmation dialogue. Once this is done your queue is gone forever so be careful.

##Compute workers setup
Internal and external compute workers can be linked to AI4Media competitions. The queues dispatch the jobs between the compute workers. Note that a queue can receive jobs (submissions) from several competitions, and can send them to several compute workers.
