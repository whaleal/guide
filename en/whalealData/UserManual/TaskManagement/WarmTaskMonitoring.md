#### Task Monitoring (Warm)

Clicking on "Task Monitoring (Warm)" under the "Task Management" menu will display a page that shows the execution status of warm tasks. The page includes information about completed tasks, tasks in progress, and exceptional tasks. Each search button is associated with condition boxes that allow you to filter and display tasks based on specified criteria.

![image-20230620140353683](../../../../images/whalealDataImages/image-20230620140353683.png)

##### Completed Tasks

Clicking on completed tasks will display information about tasks that have been successfully completed. The information includes execution strategy, start and end times, execution duration, execution status, progress percentage, archived records count, source data status, and executed SQL statements. There are four buttons at the top: Search, Modify Source Data Status, Manually Delete Source Data, and Refresh.

**Search**

The green button at the top is the search button. By entering conditions in the provided boxes and clicking on the search button, you can filter and display completed tasks that match the criteria.

**Modify Source Data Status**

After a synchronization is completed and if source data has been manually deleted, you can click the yellow button to modify the source data status to "processed."

**Manually Delete Source Data**

The red button allows you to manually delete source data. If automatic deletion is not configured in the table job settings, you can manually delete the source data from the database. Alternatively, you can click the "Manually Delete Source Data" button after selecting a task.

**Refresh**

The progress percentage of a task is updated every 3 seconds. As a result, the progress bar display might not be real-time. Clicking the refresh button updates the progress bar and some task statuses.

##### Tasks in Progress

Clicking on tasks in progress will display information about tasks that are currently being executed and archived. The information includes execution strategy, start and end times, execution duration, execution status, progress percentage, archived records count, executed SQL statements. There are three buttons: Search, Terminate Task, and Verify Task Status.

**Search**

The green button is the search button. Enter conditions in the provided boxes and click the search button to filter and display tasks in progress that match the criteria.

**Terminate Task**

The red button allows you to terminate a task. After selecting a task and clicking the "Terminate Task" button, the task will be terminated. The task will then appear in the exceptional tasks section if it was not completed normally.

**Verify Task Status**

A task can include multiple table jobs. When one table job is completed, the next one starts. If a task's status does not update promptly after a table job is completed, you can click the "Verify Task Status" button to update the task's status.

##### Exceptional Tasks

Clicking on exceptional tasks will display information about tasks that encountered exceptions. The information includes execution strategy, start and end times, execution duration, execution status, error details, progress percentage, archived records count, executed SQL statements, and rollback status. There are three buttons: Search, Rollback, and Re-execute.

**Search**

The green button is the search button. Enter conditions in the provided boxes and click the search button to filter and display exceptional tasks that match the criteria.

**Rollback**

Each exceptional task has a rollback button. Clicking the rollback button for a sub-task will roll back the exceptional data that was synchronized. Clicking the rollback button for a parent task will roll back all sub-tasks under that parent task.

**Re-execute**

Sub-tasks under an exceptional task have a re-execute button. Clicking the re-execute button will generate a new parent task. The exceptional task and the new parent task will be linked. After rolling back the exceptional data, both the exceptional task and the new parent task will appear in the "Tasks in Progress" section for re-execution.