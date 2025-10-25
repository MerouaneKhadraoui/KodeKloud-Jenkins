# Task 1: Jenkins Views

## Question

The DevOps team of xFusionCorp Industries is planning to create a number of Jenkins jobs for different tasks. So to easily manage the jobs within Jenkins UI they decided to create different views for all Jenkins jobs based on usage/nature of these jobs, - for example `datacenter-crons` view for all cron jobs. Based on the requirements shared below please perform the below mentioned task:

**Task:**

Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using username `admin` and password `Adm!n321`.

1. Create a Jenkins job named `datacenter-test-job`.

2. Configure this job to run a simple bash command i.e `echo "hello world!!"`.

3. Create a view named `datacenter-crons` (it must be a `global` view of type `List View`) and make sure `datacenter-test-job` and `datacenter-cron-job` (which is already present on Jenkins) jobs are listed under this new view.

4. Schedule this newly created job to build periodically at `every minute` i.e `* * * * *` (`please make sure to use the cron expression exactly same how it is mentioned here`)

5. Make sure the job builds successfully.

`Note:` 

1. You might need to install some plugins and restart Jenkins service. So, we recommend clicking on `Restart Jenkins when installation is complete and no jobs are running` on plugin installation/update page i.e `update centre`. Also, Jenkins UI sometimes gets stuck when Jenkins service restarts in the back end. In this case please make sure to refresh the UI page.

2. For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.

---

## Steps to Complete the Task

### 1. Access Jenkins
- Click the **“Jenkins”** button on the top bar.
- Login with:
  ```
  Username: admin
  Password: Adm!n321
  ```

---

### 2. Create a Jenkins Job
- From the Jenkins dashboard, click **“New Item”**.
- Enter the job name: `datacenter-test-job`.
- Select **“Freestyle project”** and click **OK**.

---

### 3. Configure the Job
- In the **Build** section, click **“Add build step” → “Execute shell”**.
- Add the following command:
  ```bash
  echo "hello world!!"
  ```

---

### 4. Schedule the Job
- In the **Build Triggers** section, check **“Build periodically”**.
- Enter the following cron expression:
  ```
  * * * * *
  ```
  ⚠️ Make sure to use the exact syntax with spaces.

- Click **Save**.

---

### 5. Create a Jenkins View
- From the Jenkins dashboard, click the **“+”** tab next to existing views.
- Enter the view name: `datacenter-crons`.
- Select **“List View”** and click **OK**.
- Under **Jobs**, select:
  - `datacenter-test-job`
  - `datacenter-cron-job` (already existing).
- Click **Save**.

---

### 6. Verify Job Execution
- Wait one minute for the scheduled build to trigger.
- Open the job **datacenter-test-job** → **Build History** → latest build.
- Check **Console Output**; it should display:
  ```
  hello world!!
  Finished: SUCCESS
  ```

---

## ✅ Verification Checklist

| Step | Requirement | Status |
|------|--------------|--------|
| 1 | Job `datacenter-test-job` created | ✅ |
| 2 | Runs `echo "hello world!!"` | ✅ |
| 3 | View `datacenter-crons` created | ✅ |
| 4 | Includes both jobs (`datacenter-test-job`, `datacenter-cron-job`) | ✅ |
| 5 | Scheduled every minute (`* * * * *`) | ✅ |
| 6 | Build succeeds | ✅ |

---

## Summary
You have successfully:
- Created a Jenkins freestyle job (`datacenter-test-job`).
- Configured it to print “hello world!!”.
- Scheduled it to run every minute.
- Created a **List View** named `datacenter-crons` containing both `datacenter-test-job` and `datacenter-cron-job`.
- Verified successful job execution.