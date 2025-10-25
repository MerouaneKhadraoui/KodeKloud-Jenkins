# Task 3: Jenkins Workspaces

## Question

Some developers are working on a common repository where they are testing some features for an application. They are having three branches (excluding the master branch) in this repository where they are adding changes related to these different features. They want to test these changes on Stratos DC app servers so they need a Jenkins job using which they can deploy these different branches as per requirements. Configure a Jenkins job accordingly.

**Task:**

Click on the `Jenkins` button on the top bar to access the Jenkins UI. Login using username `admin` and password `Adm!n321`.

Similarly, click on `Gitea` button to access the Gitea page. Login to `Gitea` server using username `sarah` and password `Sarah_pass123`.

1. There is a Git repository named `web_app` on Gitea where developers are pushing their changes. It has three branches `version1`, `version2` and `version3` (excluding the `master` branch). You need not to make any changes in the repository.

2. Create a Jenkins job named `app-job`.

3. Configure this job to have a choice parameter named `Branch` with choices as given below:

`version1`

`version2`

`version3`

4. Configure the job to fetch changes from above mentioned Git repository and make sure it should fetches the changes from the respective branch which you are passing as a choice in the choice parameter while building the job. For example if you choose `version1` then it must fetch and deploy the changes from branch `version1`.

5. Configure this job to use custom workspace rather than a default workspace and custom workspace directory should be created under `/var/lib/jenkins` (for example `/var/lib/jenkins/version1`) location rather than under any sub-directory etc. The job should use a workspace as per the value you will pass for `Branch` parameter while building the job. For example if you choose `version1` while building the job then it should create a workspace directory called `version1` and should fetch Git repository etc within that directory only.

6. Configure the job to deploy code (fetched from Git repository) on storage server (in Stratos DC) under `/var/www/html` directory. Since its a shared volume.

You can access the website by clicking on `App` button.

---

## ✅ Overview

This task tests your understanding of Jenkins parameters, Git branch configuration, and custom workspaces.

---

## 🧩 Task Summary

You must create a Jenkins job named **`app-job`** that:

- Uses a **Choice Parameter** to select between `version1`, `version2`, and `version3`
- Clones the corresponding branch from the `web_app` repository in Gitea
- Uses a **custom workspace** at `/var/lib/jenkins/${Branch}`
- Deploys the code to `/var/www/html` on the shared storage server

---

## 🧠 Step-by-Step Solution

### 1. Access Jenkins

- Click the **Jenkins** button on the top bar.
- Login using:
  ```
  Username: admin
  Password: Adm!n321
  ```

---

### 2. Create a New Job

- Click **New Item**
- Enter the name: `app-job`
- Choose **Freestyle project**
- Click **OK**

---

### 3. Add a Branch Choice Parameter

1. Check **This project is parameterized**
2. Click **Add Parameter → Choice Parameter**
3. Fill in the following:

   ```
   Name: Branch
   Choices:
   version1
   version2
   version3
   ```

---

### 4. Configure Git Repository

- Go to **Source Code Management → Git**
- Enter the repository URL (from Gitea):
  ```
  http://gitea.stratos.xfusioncorp.com/sarah/web_app.git
  ```
- Add credentials:
  - Username: `sarah`
  - Password: `Sarah_pass123`
- Change the **Branch Specifier** to:
  ```
  */${Branch}
  ```

---

### 5. Use a Custom Workspace

- Scroll to **Advanced Project Options**
- Check ✅ **Use custom workspace**
- Enter:
  ```
  /var/lib/jenkins/${Branch}
  ```

This ensures Jenkins creates separate workspaces for each branch (e.g., `/var/lib/jenkins/version1`).

---

### 6. Add Deployment Step

- Scroll to **Build → Add build step → Execute shell**
- Add the following commands:

  ```bash
  # Clean target directory before copying
  rm -rf /var/www/html/*

  # Copy repository files to web root
  cp -r * /var/www/html/
  ```

---

### 7. Save and Build

- Click **Save**
- Click **Build with Parameters**
- Choose a branch (e.g., `version1`)
- Click **Build**

---

### 8. Verify the Deployment

- Click the **App** button on the KodeKloud interface.
- The web app should now display the branch-specific content.

---

## ✅ Expected Behavior

| Branch Selected | Workspace Used             | Git Branch Checked Out | Deployed to       |
|------------------|----------------------------|------------------------|-------------------|
| version1         | `/var/lib/jenkins/version1` | `version1`             | `/var/www/html`   |
| version2         | `/var/lib/jenkins/version2` | `version2`             | `/var/www/html`   |
| version3         | `/var/lib/jenkins/version3` | `version3`             | `/var/www/html`   |

---

## ⚙️ Quick Recap

- **Parameter name:** `Branch`
- **Git branch specifier:** `*/${Branch}`
- **Custom workspace:** `/var/lib/jenkins/${Branch}`
- **Deploy command:**
  ```bash
  rm -rf /var/www/html/*
  cp -r * /var/www/html/
  ```

---

## ✅ Done!

Once built successfully, your Jenkins job dynamically switches between branches and deploys each version independently under the same shared web root.