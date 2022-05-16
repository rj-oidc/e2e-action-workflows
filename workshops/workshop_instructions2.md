# Part 2: Set up your repository using Github Action

Part 2 will focus on issue automation and project management. It will do the following :
- Add issue to project board whenever a new issue is created.
- When an issue is assigned to a user, create another issue.
- When an issue is closed, create new issues and update old issue.

This helps in automating issues and help managing your project.

## Create a new project
   - Open a new tab and go to https://github.com/
   - Click your profile icon on top right
   - Go to `Your Projects`
   - Click on `Projects (Beta)`
   - Click on the `New Project` button.
   - Copy url of the project (without views part).
   
Store project url in actions secrets.
  - In your forked repository, go to `Settings`
  - Click on `Secrets` option listed on the left side. Then click on `Actions` option.
  - Click on `New repository secret`
  - In **Value** text box, paste the project url from the previous step.
  - In **Name**, enter `PROJECT_URL`
  - Click on `Add Secret`
  - You can see that the secret is added.
  
  Note : Project url is not a secret. We are storing it here for easy reference in action workflows. 

## Automate Project management

Now we will automate issue addition to project using GitHub Workflows. 
We will write a workflow which will add issue to the project whenever a new issue is created.

1. Create a new workflow file named `add-to-project.yml` in `.github\workflows` folder. (You can also go to `Actions` tab -> `New workflow` and use `Skip this and set up a workflow yourself`, using which you will get a basic workflow template to fill in)
2. Add the name of the workflow as "Automate project management"
3. Add triggers for the workflow as `issues` on `opened` type.
Following is the yaml for the above steps. 💡 This workflow will get trigerred whenever a new issue is created.
```yaml 
# Add issue to project board
name: Automate project management
on:
  issues:
    types: [opened]

```
4. Next we will use the `actions/add-to-project` action for adding issue to project
```yaml
jobs:
  add-to-project:
    name: Add issue to project
    runs-on: ubuntu-latest
    steps:
      - uses: actions/add-to-project@main
        with:
          project-url: ${{ secrets.PROJECT_URL }}
          github-token: ${{ secrets.PROJECT_TOKEN }}
```

### Create a new issue.
Now
