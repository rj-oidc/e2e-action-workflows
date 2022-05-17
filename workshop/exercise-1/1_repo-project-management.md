# Project Management and issue automation

This section will focus on issue automation and project management. With the help of issues we will show how GitHub Actions can be used in various part of SDLC. We will use workflows which will :
- Add an issue to a project board whenever a new issue is created. This helps in tracking the issue.
- When a `feature` issue is assigned to a user, create a `design` issue.
- When an issue realted to feature is closed, create new issue(s) and update the `feature` issue.

This helps in automating issues and managing your project. We will use these workflows to traverse through the workshop.

## Create a new project
   - Open a new tab and go to your org
   - Go to `Projects` tab
   - Click on `Projects (Beta)`
   - Click on the `New Project` dropdown and Select `New Project (Beta)`.
   - A new project will be created. Copy url of the project.

## Automate Project management

Now we will automate issue addition to project using GitHub Workflows. 
We will use a workflow which will add issue to the project whenever a new issue is created.
1. Open the `<new_org_name>/e2e-action-workflows` forked repository.
2. Open [add-to-project.yml](/.github/workflows/add-to-project.yml) in new tab.
3. Replace `<PROJECT_URL>` with URL of project created in previous step.
4. This workflow is configured to be trigerred whenever a new issue is created.
5. Next, the `actions/add-to-project` action is used for adding issue to project.

**Overall workflow looks like this:
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
          project-url: https://github.com/orgs/<org_name>/projects/1
          github-token: ${{ secrets.ACTIONS_TOKEN }}
```

### Create a new issue.
(In case issues tab is not present in your repo. Enable issues from settings)
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
   We will now use a workflow which gets triggered whenever a feature issue is assigned to someone. 
   The workflow will create a new design issue. A comment will also be added in feature issue to track the progress.
   
   ![Screenshot 2022-05-17 at 11 08 04 PM](https://user-images.githubusercontent.com/17411453/168875985-b49b3a23-a4fc-4898-a2b6-e9e3f06aeac3.png)


1. Open [issue-assigned.yml](/.github/workflows/issue-assigned.yml) in new tab.
Following is the yaml for file. This workflow will get trigerred whenever a new issue is created.
```yaml 
# Triggers when an issue is assigned.
name: "Issue assigned"
on:
  issues:
    types: [assigned]
```
4. We want to run the job only when feature issue is assigned to someone. For this we get deatils from `github.event` and check if `feature` label is present.
```yaml
jobs:
  issue-assigned:
    name: issue assigned
    runs-on: ubuntu-latest
    if: contains(github.event.issue.labels.*.name, 'feature')
```
6.  Next we use the `actions-ecosystem/action-create-issue@v1` and `peter-evans/create-or-update-comment@v2` actions for creating new issue and commenting on feature issue. Whole workflow looks like this :
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

1. Create a new workflow file named `issue-closed.yml` in `.github/workflows` folder.

Following is the yaml for the above steps. 💡 This workflow will get trigerred whenever a new issue is closed.
[yaml](/workshops/workflows/issue-closed.yml)
2. Copy this and paste in `issue-closed.yml` file.
3. This workflow adds automation which we will see through the workshop.


Now we will close the design issue. This will create a two new issues and add a comment in feature issue.



## Exercise 2 : Step 1
[Security and Secrets Management](../exercise-2/2_code-scanning-steps.md)
