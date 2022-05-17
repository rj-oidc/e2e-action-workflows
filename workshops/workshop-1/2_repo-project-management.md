# Set up your repository using Github Action

Part 2 will focus on issue automation and project management. It will do the following :
- Add issue to project board whenever a new issue is created.
- When an issue is assigned to a user, create another issue.
- When an issue is closed, create new issues and update old issue.

This helps in automating issues and help managing your project. We will use these workflows to traverse through the workshop.

## Create a new project
   - Open a new tab and go to https://github.com/
   - Click your profile icon on top right
   - Go to `Your Projects`
   - Click on `Projects (Beta)`
   - Click on the `New Project` button.
   - Copy url of the project.
   
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
          github-token: ${{ secrets.ACTIONS_TOKEN }}
```

**Overall workflow looks like [this](/workshops/workflows/add-to-project.yml) :**
```yaml
# Add issue to project board

name: Automate project management
on:
  issues:
    types: [opened]
    
jobs:
  add-to-project:
    name: Add issue to project
    runs-on: ubuntu-latest
    steps:
      - uses: actions/add-to-project@main
        with:
          project-url: ${{ secrets.PROJECT_URL }}
          github-token: ${{ secrets.ACTIONS_TOKEN }}
```

### Create a new issue.
(Incase issues tab is not present in your repo. Enable issues from settings)
1. Go to issues tab in your forked repo.
2. Click on `New issue`
3. Enter title : `E2E Action Workflows`
4. Add label `feature` from right part of UI.
5. In description add : `Issue to track workshop progress`.
6. Submit the issue.
<img width="1403" alt="Screenshot 2022-05-16 at 10 16 06 PM" src="https://user-images.githubusercontent.com/17411453/168642767-283b8d70-79e6-4029-b151-1a9f3cdb4d62.png">


If you go to`Actions` tab you can see that a workflow is trigerred
<img width="1393" alt="Screenshot 2022-05-16 at 10 16 43 PM" src="https://user-images.githubusercontent.com/17411453/168642868-4efd8f9a-6a8f-49b1-9a48-637bb5498b8f.png">
Once workflow runs successfully, you can see that the issue is getting reflected in project board.
<img width="1493" alt="Screenshot 2022-05-16 at 10 19 16 PM" src="https://user-images.githubusercontent.com/17411453/168643314-f6640917-e1de-4617-a9c8-4ef5b7e0f0e3.png">

## Issue automation

### 1. On issue assignment.
   We will now write a workflow which gets triggered whenever an issue with label `feature` is assigned to some one. 
   The workflow will create a new issue with `design` label. It will also comment on the `feature` issue.

1. Create a new workflow file named `issue-assigned.yml` in `.github\workflows` folder. (You can also go to `Actions` tab -> `New workflow` and use `Skip this and set up a workflow yourself`, using which you will get a basic workflow template to fill in)
2. Add the name of the workflow as "Issue assigned"
3. Add triggers for the workflow as `issues` on `assigned` type.
Following is the yaml for the above steps. 💡 This workflow will get trigerred whenever a new issue is created.
```yaml 
# Triggers when an issue is assigned.
name: "Issue assigned"
on:
  issues:
    types: [assigned]
```
4. We want to run the job when an issue with feature tag is assigned to someone. For this we will get deatils from `github.event` and check if `feature` label is present.
```yaml
jobs:
  issue-assigned:
    name: issue assigned
    runs-on: ubuntu-latest
    if: contains(github.event.issue.labels.*.name, 'feature')
```
6.  Next we will use the `actions-ecosystem/action-create-issue@v1` and `peter-evans/create-or-update-comment@v2` action for creating new issue and commenting on feature issue. Whole workflow looks like [this](/workshops/workflows/issue-assigned.yml) :
```yaml
# Triggers when an issue is assigned.

name: "Issue assigned"
on:
  issues:
    types: [assigned]

jobs:
  issue-assigned:
    name: Issue assigned
    runs-on: ubuntu-latest
    if: contains(github.event.issue.labels.*.name, 'feature')
    steps:
      - name : Create Design Issue
        uses: actions-ecosystem/action-create-issue@v1
        with:
          github_token: ${{ secrets.ACTIONS_TOKEN }}
          title: "[Design] ${{ github.event.issue.title }}"
          body: |
            #${{ github.event.issue.number }} Feature : ${{ github.event.issue.title }} 
            - [ ] Have a meeting with UX team
            - [ ] Share Design
            - [ ] Close Design
          labels: |
            design
          assignees: ${{ github.event.issue.assignee.login }}
          
      - name: Create comment on feature issue
        uses: peter-evans/create-or-update-comment@v2
        with:
          issue-number: ${{ github.event.issue.number }}
          token: ${{ secrets.ACTIONS_TOKEN }}
          body: |
            Design issue created.
```



Now go ahead and assign the issue created in last step(E2E Action Workflows) to yourself.
Once workflow runs successfully, you can see that a new issue is created. A comment in feature issue is also added.
Since we have the previous workflow (`add-to-project.yml`) as well, the new issue is added to project as well.

### 2. On issue closure.
   We will now add automation whenever an issue is closed.

1. Create a new workflow file named `issue-closed.yml` in `.github\workflows` folder. (You can also go to `Actions` tab -> `New workflow` and use `Skip this and set up a workflow yourself`, using which you will get a basic workflow template to fill in)

Following is the yaml for the above steps. 💡 This workflow will get trigerred whenever a new issue is closed.
[yaml](/workshops/workflows/issue-closed.yml)
2. Copy this and paste in `issue-closed.yml` file.


Now we will close the design issue. This will create a two new issues and add a comment in feature issue.
