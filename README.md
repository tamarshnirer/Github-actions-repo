# Github Actions

This project contains pipelines for Continuous Integration (CI) and Continuous Deployment (CD) of a sample application.

## CI Pipeline

The CI pipeline automates the build, testing, and versioning processes for the application. It consists of the following stages:

1. **Bump Version and Tagging**: This stage automatically increments the version and creates a new tag for the repository.

2. **Update Version in pom.xml**: This stage updates the version in the `pom.xml` file and commits the changes.

3. **Validate and Test with Maven**: This stage runs Maven to validate and test the application.

4. **Docker Build and Push**: This stage builds a Docker image of the application and pushes it to Docker Hub.

5. **Create PR to Master Branch**: If the CI pipeline succeeds, this stage creates a pull request to merge the changes into the master branch.

## CD Pipeline

The CD pipeline automates the deployment of the application to a remote server. It is triggered when changes are pushed to the master branch. The pipeline consists of the following stages:

1. **Setup SSH**: This stage sets up SSH access to the target server using the provided private key.

2. **Connect to EC2 Instance and Deploy**: This stage connects to the EC2 instance, logs in to Docker Hub, pulls the latest Docker image, stops and removes existing containers, and deploys the updated application.

## Prerequisites

Before running the CD pipeline, make sure you have the following secrets set up in your GitHub repository:

- `SSH_PRIVATE_KEY`: SSH private key for accessing the target server.
- `EC2_INSTANCE_IP`: IP address of the target EC2 instance.
- `DOCKERHUB_PASSWORD`: Docker Hub password for logging in to Docker Hub.

## Usage

To use these pipelines, follow these steps:

1. Make sure the necessary secrets are set up in your GitHub repository.
2. Push changes to the `development` branch to trigger the CI pipeline.
3. Merge changes into the `master` branch to trigger the CD pipeline.
