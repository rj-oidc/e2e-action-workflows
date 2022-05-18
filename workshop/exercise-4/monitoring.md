# Set up monitoring for issues.

This exercise will focus on bug automation and notifications. Whenever a new issue with bug title is created, the workflow will :
- Add a `bug` label to the issue.
- Assign the issue to the DRI (Directly Responsible Individual)
- Optional : Send a message to slack channel.

This helps in notifying the individual and quick response time for fixing the issue.

## Add `DRI.txt` file.
1. Create a new file in root directory of your repo.
2. Name the file : `DRI.txt`
3. Add you GitHub alias in the content.
<img width="425" alt="Screenshot 2022-05-17 at 12 35 29 PM" src="https://user-images.githubusercontent.com/17411453/168749953-9313c851-fc7e-416f-906f-c771b18f89ef.png">
4. Commit the file.

## Create a new workflow

1. Open [bug-added.yml](/.github/workflows/bug-added.yml) in new tab.
2. Uncomment the issue trigger logic. 
3. The workflow has logic to assign the issue to DRI and add a `bug` label.

```yml
# Triggers whenever a new bug is added 
name: "Assign label and dri"
on:
  issues:
    types: [opened]
jobs:
  automate-bug:
    name: Add label to bug and assign the issue
    if: contains(github.event.issue.title, 'bug')
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name : Get dri
        id : dri
        shell: bash
        run : |
          ls
          dri=$(cut -d' ' -f1 ./DRI.txt)
          echo "::set-output name=dri::$dri"
          
      - uses: actions-ecosystem/action-add-labels@v1
        with:
          github_token: ${{ secrets.ACTIONS_TOKEN }}
          labels: bug
          
      - uses: actions-ecosystem/action-add-assignees@v1
        with:
          github_token: ${{ secrets.ACTIONS_TOKEN }}
          assignees: ${{ steps.dri.outputs.dri }}
          
#       - name: Send message to Slack API
#         uses: archive/github-actions-slack@v2.0.0
#         id: notify
#         with:
#           slack-bot-user-oauth-access-token: ${{ secrets.SLACK_BOT_USER_OAUTH_ACCESS_TOKEN }}
#           slack-channel: CPPUV5KU0
#           slack-text: Hello! A new bug is created in "${{ github.repository }}"
```

### Create a new bug.
1. Go to issues tab and create a new issue.
2. Add title : `A bug in this repo`
3. Submit the issue.

A workflow will be trigerred which will add `bug` label and assign issue to the DRI. 
