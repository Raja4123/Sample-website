# Sample-website
Sample-website using jenkins, nginx
🚀 Jenkins Pipeline – Deploy Static Website to Nginx +++++++++++++++++++++++++++++++++++++++++++++++++++++

This Jenkins pipeline automatically deploys a static website from a GitHub repository to an Nginx web server.

🧩 Steps Performed

+++++++++++++++++++

1.Checkout Code: Pulls the latest code from the main branch.

2.Deploy to Nginx: Copies files from the Sample_website folder to /var/www/html.

3.Restart Nginx: Restarts the Nginx service to apply changes.

⚙️ Environment Variables

+++++++++++++++++++++++++

Variable Description 1.WEB_DIR Target deployment directory (/var/www/html)

2.SRC_DIR Source folder in the repository (Sample_website)

🧰 Requirements

++++++++++++++++

1.Jenkins with Git and Pipeline plugins

2.Nginx installed and running

3.Jenkins user with sudo privileges to copy files and restart Nginx

▶️ How to Use

++++++++++++++

Add the pipeline script to your Jenkinsfile or create a new Jenkins pipeline job.

Update the GitHub repository URL if required.

Run the pipeline — it will deploy the website automatically.

✅ Result

++++++++++

Once successful, you’ll see this message in Jenkins logs:

 ✅ Deployment Successful!
Your website will be available at: 👉 http://<your-server-ip>




