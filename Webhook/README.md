# GitHub Webhook Configuration for Automated Build Pipeline

To set up a GitHub webhook that automatically triggers a build pipeline in Jenkins, follow these steps:

1. Go to your GitHub repository's settings.

2. Select the "Webhooks" option from the left sidebar.

3. Click on the "Add webhook" button to create a new webhook.

4. In the "Payload URL" field, enter the URL of your Jenkins master. The URL should be in the following format:
   `http://<public-IP>:8080/github-webhook/`
   For example:
   `http://13.232.139.21:8080/github-webhook/`

5. Choose the "Content type" as "application/json".

6. In the "Which events would you like to trigger this webhook?" section, select the "Just the push event" option.

7. Make sure the webhook is active and click on the "Add webhook" button to save the configuration.

Now, whenever a push event occurs in your GitHub repository, the webhook will automatically trigger the build pipeline in Jenkins.

Note: Make sure your Jenkins master is accessible from the public IP or URL specified in the webhook configuration.
