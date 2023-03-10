# mlops-sample-templates

The YAML templates in this repository aim to make your introduction to Azure ML and MLOps as simple as possible. The templates provided walk you through:
- Creating a custom enviornment using a Conda file
- Training your data to create a model
- Registering your model to your Azure Machine Learning workspace
- Creating an online endpoint that allows you to inference on your newly created model

## mlops-demo.yml

The `mlops-demo.yml` file serves as our main Azure DevOps pipeline. Within this pipeline, we leverage smaller `yml` files to isolate each step. This allows us to very easily comment out any steps that we might not want to run and also use these `yml` files as puzzle pieces acrross different projects based off of how simple or robust our use case might be. This format makes it very easy to add new pipeline steps if needed. When running this pipeline, you will need to provide the value for all the variables declared at the top. If you choose to not run a particular template and a particular variable is only leveraged by that template, you may comment it out. Additionally, if you introduce new templates and would like to add new variables, you can add them to the current set.

## install-aml-cli.yml

This template installs the Azure CLI extension for ML (v2). No changes are required within this template

## connect-to-workspace.yml

This template allows us to set the contect to our Azure Machine Learning workspace so we do not have to provide the workspace name, resource group, and location in every command. No changes are required within this template.

## register-environment.yml

This template leverages our `conda.yml` and `environment.yml` to create a custom environment within our Azure Machine Learning workspace. This custom enviornment will be used for our training step. Within our `conda.yml` you would add add any additonal packages that you need and remove any packages that you do not need. Note this `conda.yml` is just a sample giving you the format of a Conda file but will most likely need additional packages for your unique use case. In the `environment.yml` we would need to change the image to match whichever base image you would like to use. The value we provided our `condaEnv` variable will replace the current "none" as the name and will be used as the environment name in the workspace registry.

## run-pipeline.yml

This template kicks off the training job that you would fill in the details for within `train.yml`. The training pipeline can be expanded to include a data import step and an evaluation step. To run this step we would pass in our `pipeline_file` path and an experiment name. Our training job will also update the `run_id` variable
