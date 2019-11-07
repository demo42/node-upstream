# upstream-node

A clone of docker hub, to enable demo updates to "upstream" images

## Env Vars

```sh
source ./upstream-node/env.sh
```

## Build with ACR Tasks

- Set the registry to upstream registry:
```sh
export ACR_NAME_UPSTREAM=demo42upstream
```

  ```sh
  az acr task create \
    -n node-upstream \
    -r ${ACR_NAME_UPSTREAM} \
    -f acr-task.yaml \
    --context ${GIT_UPSTREAM_NODE} \
    --git-access-token $(az keyvault secret show \
                  --vault-name $AKV_NAME \
                  --name $GIT_TOKEN_NAME \
                  --query value -o tsv)
  ```
- Run the task

  ```sh
  az acr task run -r ${ACR_NAME_UPSTREAM} -n node-upstream
  ```
