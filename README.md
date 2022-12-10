# How to use Azure ML environments

This project shows four different ways to define an environment in Azure ML: using a curated environment, extending a curated environment, extending a base-image, and extending a container from Docker Hub. 

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
