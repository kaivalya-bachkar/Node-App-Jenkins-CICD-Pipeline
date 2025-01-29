# Node-app CICD Pipeline using Jenkins
To execute this Jenkins pipeline script, follow these steps:

### Prerequisites
1. Install Jenkins: Ensure Jenkins is installed and running.
2. Node.js Tool Installation: Make sure `mynode` (Node.js tool) is defined under Jenkins -> Manage Jenkins -> Global Tool Configuration -> NodeJS Installations.
3. SSH Credentials: The SSH key (`ubuntu`) should be added under Jenkins -> Manage Jenkins -> Credentials and associated with the required server.
4. Git Repository: Your Git repository should be accessible, and the Node.js application should have a `package.json` with the necessary dependencies.
5. Install Mocha: Ensure `mocha` is included in your `package.json` for testing.

### Steps to Execute
1. Access Jenkins: Open your Jenkins dashboard.

2. Create a New Pipeline Job:
   - From the Jenkins dashboard, click on New Item.
   - Enter a name for your job, select Pipeline, and click OK.

3. Configure the Pipeline:
   - Enable the GitHub hook trigger for GITScm polling in a Build Triggers
   - Scroll down to the Pipeline section.
   - Set Definition to Pipeline script.
   - Copy and paste the entire pipeline script provided into the Jenkinsfile.
   - Or Choose the pipeline script from SCM and in SCM select the Git option and then paste the git repository link and Save it.  

4. Configure Webhook on GitHub:
   - Navigate to your repository on GitHub → Click on the Settings tab.
   - In the Settings tab, click on Webhooks in the sidebar, then click Add webhook.
   - In the Payload URL, enter the URL of your Jenkins instance followed by `/github-webhook/` (for example, `http://<your-jenkins-server>/github-webhook/`).
   - Set the Content-Type to `application/json`.
   - Select Just the push event (or you can choose other events based on your requirement, like pull request events).
   - Click Add webhook to create it.
     
6. Save the Job:
   - Click Save at the bottom of the page.

7. Run the Pipeline:
   - Go to the newly created job and click Build Now.
   - The pipeline will execute the following stages:
     1. Git Cloning: Clone the repository from GitHub.
     2. Build: Install Node.js dependencies.
     3. Test: Run tests using Mocha.
     4. Deploy: Connect to the remote server via SSH and deploy the application using `pm2`.

8. Monitor the Pipeline:
   - View the pipeline progress in Build History.
   - Click on the build number to view console output for logs and troubleshooting if needed.
