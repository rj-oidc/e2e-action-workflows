## Secrets management

### 1. Create another repo to copy secrets to 

1. Fork the repo : https://github.com/JysinTestOrg/secret-test-repo
 
### 2. Create secrets in current repo
   - `GH_TOKEN_SECRET` : Required, Token to use to get repos and write secrets. ${{secrets.GITHUB_TOKEN}} will not work. Only add to above repo.
       - <img width="868" alt="image" src="https://user-images.githubusercontent.com/58063491/168108601-95501126-f85d-4d23-afca-c4bc559c3a2f.png">

       - <img width="957" alt="image" src="https://user-images.githubusercontent.com/58063491/168108211-92f48588-bfcd-4001-8d6a-38713a40dd99.png">

   - `TEST_SECRET_1`, `TEST_SECRET_2` to copy to other repo.

### 3. Create workflow in current repo

```
name: Secret manager
on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: google/secrets-sync-action@v1.7.0
        with:
          SECRETS: |
            ^FOO$
            ^CONTAINER*
          REPOSITORIES: |
            <your_org_name>/secret-test-repo # Update repo owner name here to your org
          DRY_RUN: true # Update this to false to create the secrets
          GITHUB_TOKEN: ${{ secrets.GH_TOKEN_SECRET }}
          CONCURRENCY: 10
        env:
         FOO: ${{secrets.TEST_SECRET_1}} # Will be picked up
         FOOBAR: BAZ # will not be picked up
         CONTAINER: ${{secrets.TEST_SECRET_2}} # Will be picked up
```

### 4. Run workflow with `DRY_RUN: true`
### 5. Run workflow with `DRY_RUN: false`
### 6. Test copied secrets
Run workflow `print_test_secrets.yml` in the repository created in step 1 above , and verify they were correctly copied.


## 📚 Resources :
 - https://github.com/google/secrets-sync-action#readme
 - https://github.com/say8425/aws-secrets-manager-actions#readme
