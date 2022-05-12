1. Create workflow
2. Create another repo to copy to
3. Add secrets
   - GITHUB_TOKEN_SECRETS : Required, Token to use to get repos and write secrets. ${{secrets.GITHUB_TOKEN}} will not work. Only add to above repo.
       - <img width="868" alt="image" src="https://user-images.githubusercontent.com/58063491/168108601-95501126-f85d-4d23-afca-c4bc559c3a2f.png">

       - <img width="957" alt="image" src="https://user-images.githubusercontent.com/58063491/168108211-92f48588-bfcd-4001-8d6a-38713a40dd99.png">

   - Create secrets starts with FOO
   - Starts with CONTAINER

4. Run workflow with `DRY_RUN: true`
5. Run workflow with `DRY_RUN: false`


Resources :
 - https://github.com/google/secrets-sync-action#readme
 - https://github.com/say8425/aws-secrets-manager-actions#readme
