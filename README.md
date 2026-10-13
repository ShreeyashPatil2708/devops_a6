# Assignment No. 6: Jenkins Integration with GitHub

## Title
Integrate Jenkins with a Git Repository and Automate Source Code Retrieval from GitHub

## Aim
To configure Jenkins with a GitHub repository and automate the process of pulling source code from the repository for Continuous Integration.

## Objectives
- Understand the role of Jenkins in CI/CD.
- Install and configure the Git plugin in Jenkins.
- Connect Jenkins with a GitHub repository.
- Create a Jenkins job for automatic source code checkout.
- Execute a simple build through Jenkins.

## Prerequisites
- Jenkins installed and running
- Git installed
- GitHub account and repository
- Java/JDK
- Sample application or project

## Concept
Jenkins is an automation server used to implement Continuous Integration and Continuous Delivery pipelines. It can integrate with GitHub so that the latest version of an application is automatically retrieved whenever a build is initiated.

**Basic workflow:**

```
Developer → GitHub Repository → Jenkins → Build/Test → Build Result
```

## Project Structure

```
devops-demo/
├── README.md
├── index.html
├── app.py
└── Jenkinsfile
```

## Procedure

### Step 1: Create a GitHub Repository
Created the repository `devops_a6` containing the sample application files (`index.html`, `app.py`).

Repository URL: https://github.com/ShreeyashPatil2708/devops_a6

### Step 2: Configure Git in Jenkins
Navigate to:

```
Manage Jenkins → Plugins → Available Plugins
```

Install the following plugins:
- **Git Plugin**
- **GitHub Plugin**
- **Pipeline Plugin**

Restart Jenkins if required after installation.

### Step 3: Create a Jenkins Job
1. Open the Jenkins Dashboard.
2. Select **New Item**.
3. Enter job name: `GitHub-Jenkins-Demo`.
4. Select **Freestyle Project**.
5. Click **OK**.

### Step 4: Configure Source Code Management
In the job configuration page:

1. Under **Source Code Management**, select **Git**.
2. Enter the repository URL:
   ```
   https://github.com/ShreeyashPatil2708/devops_a6.git
   ```
3. For a private repository, configure GitHub credentials in Jenkins (**Manage Jenkins → Credentials**).
4. Specify the branch to build:
   ```
   */main
   ```

### Step 5: Configure Build Step
Add a build step (**Execute Shell**) to run one of the following:

```bash
python3 app.py
```

or simply verify that the repository has been cloned:

```bash
ls
```

### Step 6: Build the Job
1. Select **Build Now**.
2. Verify:
   - The Git repository is cloned successfully.
   - The latest source code is available inside the Jenkins workspace.
   - The **Console Output** displays successful checkout and build information.

## Jenkins Pipeline (Declarative)

A `Jenkinsfile` is included in this repository so the same job can be run as a **Pipeline** project instead of a Freestyle project:

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ShreeyashPatil2708/devops_a6.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'ls'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'python3 app.py'
            }
        }
    }
}
```

To use it, create a new **Pipeline** job in Jenkins and under **Pipeline → Definition**, select **Pipeline script from SCM**, choose **Git**, point it at this repository, and set the script path to `Jenkinsfile`.

## Expected Result
Jenkins successfully connects to GitHub, retrieves the latest project source code, and executes the configured build. Both the Freestyle job and the Pipeline job produce a `SUCCESS` build status, and the console output confirms the checkout of the `main` branch and the execution of the build/test steps.

## Learning Outcome
Through this assignment, we learned how to:
- Integrate Jenkins with a GitHub repository using the Git plugin.
- Configure Source Code Management (SCM) in a Jenkins job to automatically pull the latest code.
- Create and run both Freestyle and Pipeline jobs in Jenkins.
- Understand how source-code changes participate in an automated CI/CD workflow, from commit to build.
