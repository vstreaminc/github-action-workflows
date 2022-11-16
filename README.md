# GitHub Action Reusable workflows

## Workflows 

There are several main reusable workflows that makes release engineering process works
The workflows operates with single application from monorepo.
So if you have multiple applications in the repo you have to reference the workflows multiple times - 
one per application 

### [Feature branch](.github/workflows/dockerized-ecs-app-feature-branch.yml)

This workflow should be triggered on PR open/syncronized/closed or labeled/unlabeled.
It performs Docker build, run tests and deploys application with ECS one or multiple QA environments.

### [Main branch](.github/workflows/dockerized-ecs-app-main-branch.yml) 

This workflow should be triggered on push into the main branch. 
It performs Docker build, run tests and deploys application with ECS on multiregion dev environment.

### [Release](.github/workflows/dockerized-ecs-app-release.yml)

This workflow should be triggered on publishing new release.
It promotes exiting Docker build from the main branch to release version and deploy it with ECS on multiregion staging 
environment.

### [Deploy production](.github/workflows/dockerized-ecs-app-deploy-production.yml)

This workflow should be triggered manually with release version as input.
It will check that the docker image for the release version exists and deploy it with ECS on multiregion
production environment.

### [Hotfix branch](.github/workflows/dockerized-ecs-app-hotfix-branch.yml)

### [Hotfix release](.github/workflows/dockerized-ecs-app-hotfix-release.yml)

## Controllers

Controllers are reusable workflows that helps to automate interaction between main workflows and GitHub API

### [Monorepo](.github/workflows/controller-monorepo.yml)

The workflow draft new GitHub release.
Used as the final step in a main branch workflow to create/update predefined release


### [Draft release](.github/workflows/controller-draft-release.yml)

The workflow draft new GitHub release. 
Used as the final step in a main branch workflow to create/update predefined release

### [Hotfix releas branch](.github/workflows/controller-hotfix-release-branch.yml)

This is a glue workflow to connect regular releases' workflow with hotfix workflow.
It creates a release branch for each new release version.
Used as part of the release workflow. 

## CI

### [DOcker build](.github/workflows/ci-dockerized-app-build.yml)

Promote previous version or build new docker image and test it 

### [DOcker promote](.github/workflows/ci-dockerized-app-promote.yml)

Promote docker image to specific release version

### [DOcker verify](.github/workflows/ci-dockerized-app-verify.yml)

Check if there is docker image with specific tag in the ECR

## CD