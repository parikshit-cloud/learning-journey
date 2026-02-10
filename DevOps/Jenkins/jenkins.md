# 🤖 Jenkins: CI/CD Automation Tool

**Jenkins** is an open-source automation server used for **Continuous Integration (CI) and Continuous Delivery/Deployment (CD)**. It helps developers automate the building, testing, and deployment of applications.

---

## 🔑 Key Concepts

### 1. Job / Project
- A **Job** or **Project** defines a task for Jenkins to execute.
- Types:
  - **Freestyle Project**: Simple build job with manual configuration.
  - **Pipeline**: Scripted workflow using `Jenkinsfile`.
  - **Multibranch Pipeline**: Automatically discovers branches in a Git repository.
  - **Folder**: Organizes multiple jobs into folders.

### 2. Jenkinsfile
- A text file containing the **pipeline definition**.
- Can be **Declarative** or **Scripted** syntax.
- Example:

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'scp target/myapp.war user@server:/deploy/path/'
            }
        }
    }
}

### 3. Nodes & Agents

- **Master Node**: Manages Jenkins jobs and schedules builds.
- **Agent Node**: Executes jobs as instructed by the master.
- Supports distributed builds for scalability.

### 4. Plugins

Jenkins is highly extensible through plugins. Examples:

- **Git Plugin** → Connect Jenkins to Git repositories
- **Pipeline Plugin** → Use Jenkinsfile pipelines
- **Docker Plugin** → Build and deploy Docker containers
- **Slack Plugin** → Notifications for builds

### 5. Pipelines

- Automate build, test, and deployment processes.
- Can be **Declarative** (simpler) or **Scripted** (more flexible).

---

## ⚙️ Installing Jenkins (Ubuntu Example)

```bash
# Update system
sudo apt update
sudo apt install openjdk-11-jdk -y

# Add Jenkins repo key
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

# Add Jenkins repo
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

# Install Jenkins
sudo apt update
sudo apt install jenkins -y

# Start Jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins

# Check status
sudo systemctl status jenkins
