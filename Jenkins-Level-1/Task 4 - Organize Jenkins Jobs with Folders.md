# Task 4: Organize Jenkins Jobs with Folders

## Question

xFusionCorp Industries' DevOps team aims to streamline the management of Jenkins jobs by organizing them into distinct folders based on their purpose. Complete the task following the provided requirements:

**Task:**

1. Access the Jenkins UI by clicking on the `Jenkins` button in the top bar. Log in using the credentials: username `admin` and password `Adm!n321`.

2. Create a new folder named `Apache` within the Jenkins UI.

3. Move the existing jobs `httpd-php` and `services` under the newly created `Apache` folder.

`Note:` 

1. Ensure to install any required plugins and restart the Jenkins service if necessary. Opt for `Restart Jenkins when installation is complete and no jobs are running` on the plugin installation/update page.

2. Be aware that Jenkins UI may experience temporary unresponsiveness during the service restart. Refresh the UI page if needed.

3. Capture screenshots of your work for documentation and review purposes. Alternatively, utilize screen recording software like loom.com for detailed documentation and sharing.

---

## ✅ Step 1: Access the Jenkins Web UI

1. On the KodeKloud lab environment, click on the **“Jenkins”** button at the top bar.
This will open the Jenkins interface in a new tab or window.

2. Log in with the following credentials:

- **Username:** `admin`
- **Password:** `Adm!n321`

---

## ✅ Step 2: Check for Folder Plugin

Before creating folders, make sure the **CloudBees Folder Plugin** is installed.

1. In Jenkins, go to:
```bash
Manage Jenkins → Manage Plugins → Available
```
2. Search for:
```bash
CloudBees Folder
```
3. If it’s not installed:
- Select the checkbox next to it.
- Click **Install without restart** (or **Install and Restart** if prompted).
- Once installed, choose:
```sql
Restart Jenkins when installation is complete and no jobs are running
```
4. Wait for Jenkins to restart (refresh the page if it seems stuck).

---

## ✅ Step 3: Create the Folder

1. From the Jenkins dashboard, click “**New Item**” on the left sidebar.
2. Enter the name: `Apache`
3. Select **Folder** as the item type.
4. Click **OK**.
5. (Optional) Add a description like “***Folder for Apache-related jobs***” and click **Save**.

---

## ✅ Step 4: Move Existing Jobs to the Folder

You need to move the two jobs: `httpd-php` and `services`.

1. From the Jenkins dashboard, click on “**Manage Jenkins**” → “**Manage Old Data**” to confirm no issues (optional but safe).
2. Go back to the main dashboard.
3. Hover over the job name (e.g. `httpd-php`), click the **down arrow** next to it → select **Move**.
4. In the **Destination** field, choose or type: `Apache`
5. Click **Move**.
6. Repeat the same steps for the `services` job.

---

## ✅ Step 5: Verify

1. Go to the Jenkins dashboard.
2. Open the Apache folder.
3. You should see both jobs:
`httpd-php`
`services`

---

## 🎯 Final Verification Checklist

✅ Folder `Apache` exists
✅ Jobs `httpd-php` and `services` are inside `Apache`
✅ Jenkins is running without issues after restart

---

## 🧩 Bonus Tip (for scripting or automation)

If this were to be automated via CLI or script:

```bash
# Example using Jenkins CLI (optional knowledge)
java -jar jenkins-cli.jar -s http://localhost:8080/ create-job Apache < folder.xml
java -jar jenkins-cli.jar -s http://localhost:8080/ move-job httpd-php Apache/httpd-php
java -jar jenkins-cli.jar -s http://localhost:8080/ move-job services Apache/services
```