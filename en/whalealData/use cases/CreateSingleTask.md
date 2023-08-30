#### Creating One-Time Tasks

To create a one-time task, follow these steps:

1. Navigate to the "Task Configuration" menu and select "Task Configuration."
2. Click the blue "New" button to open the task creation form.
3. In the task creation form (second image), select the task mode as "One-Time."
4. Choose a specific execution time using a Cron expression. Cron expressions allow you to define the exact date and time when the task should be executed.
5. Configure other settings as needed, such as execution mode, task timeout, and retry attempts.
6. Optionally, set up a notification strategy by adding email addresses for alerts. Notifications will be sent based on the chosen strategy after the task completes.
7. Click the "Add Job" button to attach a job (table job) to the task. In the job configuration form (third image), select the desired job(s) to be associated with this task.
8. Click "OK" or "Confirm" to save the task configuration.

Please note that one-time tasks need to be reviewed and approved by an administrator before they can be executed. Once the task is approved, it will be scheduled for execution based on the specified time using the Cron expression.

One-time tasks are suitable for tasks that need to be executed at a specific point in time, such as data synchronization or archiving activities that are scheduled to happen once.


![image-20230621142941634](../../../images/whalealDataImages/image-20230621142941634.png)

![image-20230621143119669](../../../images/whalealDataImages/image-20230621143119669.png)

![image-20230621143532776](../../../images/whalealDataImages/image-20230621143532776.png)