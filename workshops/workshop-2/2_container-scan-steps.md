## Setup container scanning

As part of our CD process, we might be creating docker containers in our repo, from our repo code. 
The container creation process allows us to install other dependencies into the container, that are required for our apps to run.
This is one place where new vulnerabilities could be introduced, which the code-scanning process might miss.
In this section we see how that can be identified using an action workflow.

### 1. Create the workflow

```
name: Container scan
on:
  workflow_dispatch:
#  push:
#    branches: [ master ]
#  pull_request:
#    branches: [ master ]

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      CONTAINER_REGISTRY: 'hub.docker.com'
    steps:
      - uses: actions/checkout@v3

      - run: docker build . -t ${{ env.CONTAINER_REGISTRY }}/joshsample:${{ github.sha }}

      - uses: Azure/container-scan@v0
        with:
          image-name: ${{ env.CONTAINER_REGISTRY }}/joshsample:${{ github.sha }}

# Optional steps
#       - uses: Azure/docker-login@v1
#         with:
#           login-server: ${{ env.CONTAINER_REGISTRY }}
#           username: ${{ secrets.REGISTRY_USERNAME }}
#           password: ${{ secrets.REGISTRY_PASSWORD }}

#       - run: docker push ${{ env.CONTAINER_REGISTRY }}/constellation:${{ github.sha }}
```

### 2. Setup env variables and secrets (if required)

### 3. Commit and run


## 📚 Resources : 

- Action used: https://github.com/azure/container-scan#readme
- Reference for container vulnerabilities: https://nvd.nist.gov/vuln
