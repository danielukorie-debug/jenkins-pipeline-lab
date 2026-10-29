# Jenkins Pipeline Automation Lab

cd ~/jenkins-pipeline-lab
nano README.mdcd ~/jenkins-pipeline-lab
nano README.md## Project Overview

This project demonstrates introductory Continuous Integration (CI)
skills using Jenkins Pipeline as Code.

The pipeline is stored in a Jenkinsfile and defines automated stages
that print messages to the Jenkins build log.

## Technology Stack

- Jenkins
- Declarative Pipeline
- Groovy-based Jenkinsfile syntax
- Ubuntu Linux
- Git and GitHub

## Pipeline Stages

### Welcome

Prints a message confirming that the pipeline is running.

### Check

Prints a second message to demonstrate sequential pipeline stages.

## How to Use

1. Open Jenkins.
2. Create a Pipeline job or open an existing Pipeline job.
3. Configure the job to use this repository.
4. Select the `Jenkinsfile` from source control.
5. Run the job and review Console Output.

## Learning Objectives

- Understand the structure of a Jenkinsfile.
- Define stages and steps.
- Read Jenkins build logs.
- Version-control pipeline code with Git.
- Prepare for future automated testing and deployment.

## Future Improvements

- Add required-file validation.
- Run Terraform formatting and validation.
- Build and test Docker images.
- Add automated deployment stages.


## Pipeline Workflow Diagram

This diagram represents the two stages defined in the current `Jenkinsfile`. The screenshot below will provide evidence from an actual Jenkins run.

```mermaid
flowchart TD
    Start[Build starts]
    Agent[agent any: Jenkins selects an available agent]
    Welcome[Welcome stage: print greeting messages]
    Check[Check stage: print automated job message]
    Result[Pipeline result]
    Start --> Agent --> Welcome --> Check --> Result
```

## Successful Pipeline Run

The screenshot below captures the successful Jenkins build and provides evidence of an actual pipeline run.

![Successful Jenkins pipeline](docs/images/jenkins-pipeline-success.png)
## Kubernetes Manifest Validation

The Jenkins pipeline checks Kubernetes YAML manifests using [Kubeconform](https://github.com/yannh/kubeconform).

### Validation Workflow

1. Check out the Kubernetes manifests repository.
2. Download the pinned Kubeconform release.
3. Verify the downloaded archive against its SHA-256 checksum.
4. Extract and run Kubeconform in strict mode.
5. Validate the Deployment and Service manifests against Kubernetes version 1.37.0.

### Validation Results

The successful Jenkins Console Output reported:

```text
Summary: 2 resources found in 2 files
Valid: 2
Invalid: 0
Errors: 0
Skipped: 0
Finished: SUCCESS
```

These results confirm that both manifests passed Kubeconform schema validation during the recorded build. This does not, by itself, prove that the application was deployed or that runtime behavior was tested.

### Evidence

The validation results can be reviewed in the Jenkins job's **Console Output** for the successful build.
