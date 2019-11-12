# upstream-node

A clone of docker hub, to enable demo updates to "upstream" images

## Env Vars

```sh
source ./upstream-node/env.sh
```

## Build with ACR Tasks

- Set the registry to upstream registry:

  ```sh
  az acr task create \
    --name node-hub \
    -f acr-task.yaml \
    --context ${GIT_NODE_UPSTREAM} \
    --git-access-token $(az keyvault secret show \
                          --vault-name $AKV_NAME \
                          --name github-token \
                          --query value -o tsv)
  ```
- Run the Task

  ```sh
  az acr task run --name node-hub
  
  watch -n1 az acr task list-runs
  ```

