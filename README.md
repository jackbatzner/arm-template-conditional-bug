# step 1

Create resource group

```
az group create --location westus --resource-group test-deploy   
```

# step 2

Creates resources in West US

```
az deployment group create --mode Incremental --template-file .\azuredeploy.json --parameters .\azuredeploy.parameters.json --resource-group test-deploy
```

# step 3

Test deploy second set of resources in East US and exclude resources already created in West US.

```
az deployment group what-if --mode Incremental --template-file .\azuredeploy.json --parameters .\azuredeploy.parameters.json --resource-group test-deploy --parameters firstDeploy=false --parameters location=eastus
```

Notice that you get an error for the resource you're attempting to exclude from evaluation,

```
InvalidResourceLocation - The resource 'jbstoragetest1' already exists in location 'westus' in resource group 'test-deploy'. A resource with the same name cannot be created in location 'eastus'. Please select a new resource name.
```

