# CodeFlow: CI/CD Node.js Image - GitHub Actions Workflow


# Prerequisites
To follow along with this guide, you require the following:

- Docker Engine installed on your computer.
- AWS CLI installed.
- Git installed.
- Basic knowledge of working with AWS and GitHub.

  # Setting Up the AWS IAM
- To allow GitHub Actions to communicate with AWS, you’ll need an AWS IAM user account to manage access to AWS resources.
- You can achieve it using AWS CLI. It Provides commands for interacting with various AWS services, such as ECR.
- Give the created user access to the AWS Management Console.
- Give the created user permission to access AWS ECR (AWS EC2 ELASTIC CONTAINER REGISTRY)

![bakare-iam](https://github.com/bakare-rasheed/nodejs-Githubaction/assets/114327344/464d7786-007f-4280-b029-290dfa802dc4)


From your terminal, initialize a Node.js application:
`npm init -y`

Install express to create a simple web server:

`npm install express`

# Creating Application Dockerfile
Docker will use this application and build an image that has the application code and dependencies. GitHub action will then ship the image to ECR. 
Therefore, you need the correct Docker command for building the application image. 

- Create a `.dockerignore` to ignore the `node_modules` and npm log file on Docker while building the image. 
- This reduces the image size by instructing Docker not to copy any unnecessary files and folders
- Likewise, the code will be pushed to GitHub. Therefore create a `.gitignore` to avoid shipping node_modules to GitHub 
- Once the application is ready, it’s time to use the repository you just created. First,

- initialize a local GitHub repository:  `git init`
  
- Add the project files and folders to the repository: `git add .`

- Then commit them using the following command: `git commit -m "build initial commit"

- Finally, push the code to the online GitHub Repository: `git push`

   # Setting Up AWS ECR
  
- You will require an ECR instance to store the image we will build and deploy. 
  Navigate to your AWS Management Console, and from the dashboard section, search for Elastic Container Registry, 
  then click on Create a repository.

- Ensure you have selected Private, enter the name of the repository, and create Repository

![bakare-repo](https://github.com/bakare-rasheed/nodejs-Githubaction/assets/114327344/2b44bfbf-a7f1-4658-9a1e-3b1d24eb236f)


 # Configure GitHub With AWS ECR
 
For your workflow to work, you must configure the permissions for GitHub Actions to access ECR.
From the project’s GitHub repository page, click on Settings. From this page, click on Secrets and Variables 

![bkr-secret](https://github.com/bakare-rasheed/nodejs-Githubaction/assets/114327344/9cdee11d-5ce4-494b-8b60-7f7456a75ecd)

![bkr-secrete2](https://github.com/bakare-rasheed/nodejs-Githubaction/assets/114327344/43e7f220-f593-4be1-a364-1380c166e681)


# Writing the Workflow YAML File

The most important part is to create a workflow that will trigger builds and deployments. 
This will create, connect the pipeline and ensure every process works as expected. Let’s discuss how to create a GitHub Actions workflow that deploys our sample Node.js application to ECR.

The first step is to set up is when the workflow should be triggered. 
In this case, a change to the main branch should always automatically triggers the workflow.

To execute the above workflow, on the project’s GitHub repository page, 
navigate to the Actions menu and set up a workflow yourself:

![bakare-yml](https://github.com/bakare-rasheed/nodejs-Githubaction/assets/114327344/0e50477e-e074-4363-9038-261abad9d02e)

# Deploying to AWS ECR

To deploy your workflow, you only need to hit the Start commit.
Once you have committed, a workflow should be started automatically.
Go ahead and refresh your ECR repository, and your application image will be deployed 

![bakare-deploy](https://github.com/bakare-rasheed/nodejs-Githubaction/assets/114327344/20b51853-2d86-4588-a810-bc35d57d4b73)

![bkr-success](https://github.com/bakare-rasheed/nodejs-Githubaction/assets/114327344/2798eb75-da56-4c80-99cb-e0c3b29b44b7)

![bakare-image](https://github.com/bakare-rasheed/nodejs-Githubaction/assets/114327344/46b2acf8-c7b3-4f78-8d95-fe243dae9155)


# Conclusion

Deploying applications to AWS ECR with a GitHub Actions CI/CD establishes a robust and dependable pipeline for managing the entire lifecycle of containerized applications. This automated workflow streamlines the process by integrating GitHub Actions with AWS ECR, enabling seamless Docker builds and deployments. With each code push, the CI/CD pipeline triggers automatic container builds, runs tests, and pushes the built images to AWS ECR, ensuring a continuous and consistent deployment cycle. 
This combination of GitHub Actions and AWS ECR provides developers with a reliable and efficient approach to manage containerized applications, eliminating manual interventions and reducing the risk of errors during deployment.
