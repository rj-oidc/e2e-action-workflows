## Setup container scanning

### 1. Create workflow
   - Build a docker image
   - Scan the docker image for any security vulnerabilities
   - Push to registry - optional

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

- https://github.com/azure/container-scan#readme
- https://nvd.nist.gov/vuln
