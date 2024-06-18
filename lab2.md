# Lab 2 : Build and deploy application using Azure DevOps and landing zone accelerator

### Overview
This lab guide will walk you through the process of building and deploying applications using Azure DevOps and Landing Zone Accelerator. You'll learn how to set up your development environment, create and configure Azure resources, and use Azure DevOps for continuous integration and continuous deployment (CI/CD).

### Prerequisites
- An active Azure subscription
- Basic knowledge of Azure, Azure DevOps, and CI/CD concepts
- Visual Studio Code or another code editor installed
- Git installed on your machine

### Lab 1: Setting Up Your Environment

#### Step 1: Create an Azure DevOps Organization
1. Navigate to [Azure DevOps](https://dev.azure.com/).
2. Sign in with your Azure account.
3. Click on "Create new organization".
4. Follow the prompts to set up your new organization.

#### Step 2: Create a New Project in Azure DevOps
1. In your Azure DevOps organization, click on "New Project".
2. Provide a name and description for your project.
3. Select "Public" or "Private" as the visibility level.
4. Click "Create".

#### Step 3: Set Up a Git Repository
1. Navigate to "Repos" in your new project.
2. Click "Initialize" to create a new Git repository.
3. Clone the repository to your local machine using the URL provided.

### Lab 2: Building Your Application

#### Step 1: Create a Sample Application
1. Open your code editor (e.g., Visual Studio Code).
2. Create a new folder for your project and navigate to it.
3. Initialize a new application (for example, a simple Node.js application):

   ```bash
   npm init -y
   npm install express
   ```

4. Create an `index.js` file with the following content:

   ```javascript
   const express = require('express');
   const app = express();
   const port = process.env.PORT || 3000;

   app.get('/', (req, res) => {
     res.send('Hello, World!');
   });

   app.listen(port, () => {
     console.log(`Server is running on port ${port}`);
   });
   ```

5. Test your application locally:

   ```bash
   node index.js
   ```

#### Step 2: Push Your Code to Azure Repos
1. Commit your code to the local repository:

   ```bash
   git add .
   git commit -m "Initial commit"
   ```

2. Push your code to Azure Repos:

   ```bash
   git push origin master
   ```

### Lab 3: Configuring CI/CD in Azure DevOps

#### Step 1: Create a Build Pipeline
1. Navigate to "Pipelines" in Azure DevOps.
2. Click on "New Pipeline".
3. Select "Azure Repos Git" and choose your repository.
4. Configure your pipeline using the YAML editor or classic editor. For a Node.js application, use the following YAML as a starting point:

   ```yaml
   trigger:
   - main

   pool:
     vmImage: 'ubuntu-latest'

   steps:
   - task: NodeTool@0
     inputs:
       versionSpec: '12.x'
     displayName: 'Install Node.js'

   - script: |
       npm install
       npm test
     displayName: 'Install dependencies and run tests'

   - task: PublishBuildArtifacts@1
     inputs:
       pathToPublish: '$(Build.ArtifactStagingDirectory)'
       artifactName: 'drop'
       publishLocation: 'Container'
   ```

5. Save and run the pipeline.

#### Step 2: Create a Release Pipeline
1. Navigate to "Pipelines" > "Releases".
2. Click on "New pipeline".
3. Select "Empty job" for the new stage.
4. Link the build artifact from your build pipeline.
5. Add a task to deploy your application. For example, use the "Azure App Service deploy" task to deploy a Node.js application to Azure App Service.

### Lab 4: Setting Up a Landing Zone Accelerator

#### Step 1: Deploy the Landing Zone Accelerator
1. Navigate to the [Azure Landing Zone Accelerator documentation](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/).
2. Follow the steps to deploy a landing zone accelerator. This typically involves:
   - Using Azure Blueprints or ARM templates to deploy resources
   - Configuring policies and governance
   - Setting up networking and identity management

#### Step 2: Integrate with Azure DevOps
1. Ensure that your landing zone has the necessary resources for your application (e.g., Azure App Service, databases, storage accounts).
2. Update your release pipeline to deploy to the resources in your landing zone. Modify the deployment tasks to target the appropriate resource groups and services.

### Lab 5: Monitoring and Scaling Your Application

#### Step 1: Set Up Application Insights
1. In the Azure portal, navigate to your App Service.
2. Under "Monitoring", select "Application Insights".
3. Enable Application Insights and configure it as needed.

#### Step 2: Configure Autoscaling
1. Navigate to the "Scale out (App Service plan)" settings in your App Service.
2. Configure autoscaling rules based on metrics such as CPU usage, memory usage, or request count.

### Conclusion
By completing this lab guide, you have learned how to set up a development environment using Azure DevOps, build and deploy a sample application, configure a landing zone accelerator, and set up monitoring and scaling for your application. This comprehensive approach ensures that your application is deployed securely, efficiently, and is ready to scale as needed.

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
 
- Navigate to the Lab Validation Page, from the upper right corner in the lab guide section.
- Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
- If not, carefully read the error message and retry the step, following the instructions in the lab guide.
- If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

### Review


## You have successfully completed this lab.
