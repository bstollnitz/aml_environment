# How to use Azure ML environments

This project shows four different ways to define an environment in Azure ML: using a curated environment, extending a curated environment, extending a base-image, and extending a container from Docker Hub.

## Setup

- You need to have an Azure subscription. You can get a [free subscription](https://azure.microsoft.com/en-us/free) to try it out.
- Create a [resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal).
- Create a new machine learning workspace by following the "Create the workspace" section of the [documentation](https://docs.microsoft.com/en-us/azure/machine-learning/quickstart-create-resources). Keep in mind that you'll be creating a "machine learning workspace" Azure resource, not a "workspace" Azure resource, which is entirely different!
- Install the Azure CLI by following the instructions in the [documentation](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
- Install the ML extension to the Azure CLI by following the "Installation" section of the [documentation](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-configure-cli).
- Install and activate the conda environment by executing the following commands:

```
conda env create -f environment.yml
conda activate aml_environment
```

- Within VS Code, go to the Command Palette clicking "Ctrl + Shift + P," type "Python: Select Interpreter," and select the environment that matches the name of this project.
- In a terminal window, log in to Azure by executing `az login`.
- Set your default subscription by executing `az account set -s "<YOUR_SUBSCRIPTION_NAME_OR_ID>"`. You can verify your default subscription by executing `az account show`, or by looking at `~/.azure/azureProfile.json`.
- Set your default resource group and workspace by executing `az configure --defaults group="<YOUR_RESOURCE_GROUP>" workspace="<YOUR_WORKSPACE>"`. You can verify your defaults by executing `az configure --list-defaults` or by looking at `~/.azure/config`.
- You can now open the [Azure Machine Learning studio](https://ml.azure.com/), where you'll be able to see and manage all the machine learning resources we'll be creating.
- Optionally, you can install the [Azure Machine Learning extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.vscode-ai). Log in by clicking on "Azure" in the left-hand menu, and then clicking on "Sign in to Azure."

## Train locally

Under "Run and Debug" on VS Code's left navigation, choose the "Train locally" run configuration and press F5.

## Create environments in the cloud and use them to train in the cloud

```
cd aml_environment
```

Create the compute cluster.

```
az ml compute create -f cloud/cluster-gpu.yml
```

Create the dataset.

```
az ml data create -f cloud/data.yml
```

Create the environments and run the training jobs that use the environments.

```
az ml job create -f cloud/environment_1/job.yml
```

```
az ml environment create -f cloud/environment_2/environment.yml
az ml job create -f cloud/environment_2/job.yml
```

```
az ml environment create -f cloud/environment_3/environment.yml
az ml job create -f cloud/environment_3/job.yml
```

```
az ml environment create -f cloud/environment_4/environment.yml
az ml job create -f cloud/environment_4/job.yml
```
