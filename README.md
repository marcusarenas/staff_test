# Pismo Solution


![Diagram](https://github.com/marcusarenas/pismo/blob/master/solution_images/pismo.drawio.svg?raw=true)
<br>
<b>Issues Found</b>
<br>
Airflow setup <br>
File: compose.yaml
- Line 31 - Replaced user id from: `admin` to `airflow`;
- Line 59 - Listen port was <b>`xxx`</b>, it was corrected by replacing to `8080`;
- All setup from airflow was getting a warning when tried to run `docker-compose up` locally, it was corrected by giving the necessary permissions to local folders after initial run - command: `chmod -R 777 ./dags ./logs ./plugins`;

File: smooth.py
- Line 6 - Changed `schedule` to `schedule_interval` to match Airflow's expected argument name;
- Line 11 - Added ':' after function definition `def smooth():`;
- Line 16 - Assigned the DAG: Assigned the result of `smooth()` to `smooth_dag` to ensure it is properly registered with Airflow.

![Dag](https://github.com/marcusarenas/pismo/blob/master/solution_images/dag_executed0.png?raw=true)
![Dag](https://github.com/marcusarenas/pismo/blob/master/solution_images/dag_executed.png?raw=true)

<br>
Dag Log
```
*** Reading local file: /opt/airflow/logs/dag_id=smooth/run_id=manual__2024-07-09T18:35:24.551199+00:00/task_id=youtube_video/attempt=1.log
[2024-07-09, 18:35:27 UTC] {taskinstance.py:1083} INFO - Dependencies all met for <TaskInstance: smooth.youtube_video manual__2024-07-09T18:35:24.551199+00:00 [queued]>
[2024-07-09, 18:35:27 UTC] {taskinstance.py:1083} INFO - Dependencies all met for <TaskInstance: smooth.youtube_video manual__2024-07-09T18:35:24.551199+00:00 [queued]>
[2024-07-09, 18:35:27 UTC] {taskinstance.py:1279} INFO - 
--------------------------------------------------------------------------------
[2024-07-09, 18:35:27 UTC] {taskinstance.py:1280} INFO - Starting attempt 1 of 1
[2024-07-09, 18:35:27 UTC] {taskinstance.py:1281} INFO - 
--------------------------------------------------------------------------------
[2024-07-09, 18:35:27 UTC] {taskinstance.py:1300} INFO - Executing <Task(SmoothOperator): youtube_video> on 2024-07-09 18:35:24.551199+00:00
[2024-07-09, 18:35:27 UTC] {standard_task_runner.py:55} INFO - Started process 109 to run task
[2024-07-09, 18:35:27 UTC] {standard_task_runner.py:82} INFO - Running: ['***', 'tasks', 'run', 'smooth', 'youtube_video', 'manual__2024-07-09T18:35:24.551199+00:00', '--job-id', '3', '--raw', '--subdir', 'DAGS_FOLDER/smooth.py', '--cfg-path', '/tmp/tmpf3bidq88']
[2024-07-09, 18:35:27 UTC] {standard_task_runner.py:83} INFO - Job 3: Subtask youtube_video
[2024-07-09, 18:35:27 UTC] {task_command.py:388} INFO - Running <TaskInstance: smooth.youtube_video manual__2024-07-09T18:35:24.551199+00:00 [running]> on host 97783b75dcf5
[2024-07-09, 18:35:27 UTC] {taskinstance.py:1509} INFO - Exporting the following env vars:
AIRFLOW_CTX_DAG_OWNER=***
AIRFLOW_CTX_DAG_ID=smooth
AIRFLOW_CTX_TASK_ID=youtube_video
AIRFLOW_CTX_EXECUTION_DATE=2024-07-09T18:35:24.551199+00:00
AIRFLOW_CTX_TRY_NUMBER=1
AIRFLOW_CTX_DAG_RUN_ID=manual__2024-07-09T18:35:24.551199+00:00
[2024-07-09, 18:35:27 UTC] {smooth.py:37} INFO - Enjoy Sade - Smooth Operator: https://www.youtube.com/watch?v=4TYv2PhG89A
[2024-07-09, 18:35:27 UTC] {taskinstance.py:1323} INFO - Marking task as SUCCESS. dag_id=smooth, task_id=youtube_video, execution_date=20240709T183524, start_date=20240709T183527, end_date=20240709T183527
[2024-07-09, 18:35:27 UTC] {local_task_job.py:208} INFO - Task exited with return code 0
[2024-07-09, 18:35:27 UTC] {taskinstance.py:2578} INFO - 0 downstream tasks scheduled from follow-on schedule check
```