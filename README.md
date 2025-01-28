# Node-app
To execute this Jenkins pipeline script, follow these steps:

### Prerequisites
1. **Install Jenkins**: Ensure Jenkins is installed and running.
2. **Node.js Tool Installation**: Make sure `mynode` (Node.js tool) is defined under Jenkins -> Manage Jenkins -> Global Tool Configuration -> NodeJS Installations.
3. **SSH Credentials**: The SSH key (`ubuntu`) should be added under Jenkins -> Manage Jenkins -> Credentials and associated with the required server.
4. **Git Repository**: Your Git repository should be accessible, and the Node.js application should have a `package.json` with the necessary dependencies.
5. **Install Mocha**: Ensure `mocha` is included in your `package.json` for testing.

### Steps to Execute
1. **Access Jenkins**: Open your Jenkins dashboard.

2. **Create a New Pipeline Job**:
   - From the Jenkins dashboard, click on **New Item**.
   - Enter a name for your job, select **Pipeline**, and click **OK**.

3. **Configure the Pipeline**:
   - Scroll down to the **Pipeline** section.
   - Set **Definition** to **Pipeline script**.
   - Copy and paste the entire pipeline script you provided into the **Script** field.

4. **Save the Job**: Click **Save** at the bottom of the page.

5. **Run the Pipeline**:
   - Go to the newly created job and click **Build Now**.
   - The pipeline will execute the following stages:
     1. **Git Cloning**: Clone the repository from GitHub.
     2. **Build**: Install Node.js dependencies.
     3. **Test**: Run tests using Mocha.
     4. **Deploy**: Connect to the remote server via SSH and deploy the application using `pm2`.

6. **Monitor the Pipeline**:
   - View the pipeline progress in **Build History**.
   - Click on the build number to view console output for logs and troubleshooting if needed.
