## Setting up end-to-end testing workflow

This section demonstrates how we can perform E2E tests on applicatons with component services in different repositories.
It consists of 3 repos :
   1. Node app [Backend]
   2. React app [Frontend]
   3. E2E test suite repo

We first setup the 3 repos and then see how tests can be run and failures traced to specific commits.

### Node app [Backend]
1. Create a Heroku account for free [here](https://signup.heroku.com/).
2. For the repository https://github.com/JysinTestOrg/node-app
3. Retrieve the API key from your heroku `account settings` and click on Reveal button under the `API Key` section.
   Store the API key as a repository secret in the forked repository with the name `HEROKU_API_KEY`
4. Uncomment the yaml until (including) the `deploy-staging job` and complete the TODOs accordingly.
5. Click on Actions tab and click the I understand my workflows, go ahead and enable them button.
<img width="613" alt="image" src="https://user-images.githubusercontent.com/58063491/168782305-85addca8-3f79-4ce3-b28e-3378964bde47.png">
<img width="630" alt="image" src="https://user-images.githubusercontent.com/58063491/168782379-37db8ec7-deb9-4220-a950-25c65ed56989.png">

### React app [Frontend]
1. Fork the repository https://github.com/JysinTestOrg/React-app
2. Add the URL of the node app deployed from the previous step to the `.env.staging` file
4. Uncomment the workflow until (including) the `Deploy to staging environment` job
5. Click on Actions tab and enable actions in the forked repository.
6. Trigger the workflow. 
7. Go to Settings -> Pages -> The staging pages website should be live and running when banner turns green.

<img width="1154" alt="image" src="https://user-images.githubusercontent.com/58063491/168782225-4bce768a-f5b5-4a57-b9e4-1638640e79e1.png">
<img width="1029" alt="image" src="https://user-images.githubusercontent.com/58063491/168782554-1804e8a1-3159-42f0-b083-023af76cb9b9.png">

### Test suite
1. Fork the repository https://github.com/JysinTestOrg/e2e-test-suite
2. Update the TODO in `src/tests/text-check.e2e.js` to point to the staging URL of the frontend application.
3. Uncomment the workflow.
4. Trigger the same.

### Node app
1. Go to the repository with the node application.
2. Uncomment the `trigger_e2e_tests` job in the `node.yml` workflow file and fix the TODOs.
3. Commit the file.
4. Make any changes to the node server’s code. The workflow run will deploy the app to staging environment and then trigger the E2E test suite.


### Optional

#### Node app
1. Uncomment the deploy-production job and complete the TODOs. 
The workflow will be triggered and the production instance of the application should be up and running

#### React app
1. Create a new repo react-app-prod in the same org where other repos are forked
2. Populate the heroku app’s production url in the .env.production file.
3. Uncomment the Deploy to production environment job and complete the TODOs
4. Once the workflow is run you should see the react app’s prod instance hosted via GH pages.

### NOTE:
```
Once you are done with all the required steps, you can start pushing changes to your backend server. 
For each push. a deployment happens to staging environment and then the E2E test suites will get triggered. 
You can configure an approval in the production environment present in the Node-app repository. 
This will make sure to pause the deployment to production by asking for an approval from the reviewers.
```
## Exercise 4 :
[Monitoring](../exercise-4/monitoring.md)
