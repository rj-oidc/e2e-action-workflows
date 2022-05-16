# Constellation Workshop Instructions: End to end software workflows with GitHub Actions

<------image here----->

:bookmark: The following instructions will take on the assumption that you will be completing the steps on the GitHub UI. Feel free to use the terminal or any other GUIs you are comfortable with.

# Part 1: Set up your repository using Github Action

Workflow 1 will focus on setting up the repository. It will do the following :
- Create labels
- Create issue templates
- Create Initial Issue
- Create CODEOWNERS file

This helps in initialising the repository with relevent information which will be used in later part of SDLC.

## Fork e2e-action-workflows repository

1. Log into your GitHub account and fork [e2e-action-workflows](https://github.com/Josh-01/vigilant-waffle). 

    - Open the [e2e-action-workflows](https://github.com/Josh-01/vigilant-waffle) in a browser
    - Sign in to your GitHub account from top right if not signed-in already.
    - Fork this repository into your user account (using `Fork` option on top right of the screen). This repository will get forked as `<username>/e2e-action-workflows`
    
    This repo contains a starter project required in the workshop. It also contains the instructions for the workshop.
  
## Add PAT token to Actions Secret
 
We need a PAT token with required permissions for actions to create issues, labels etc.
   - Open a new tab and go to https://github.com/
   - Click your profile icon on top right
   - Go to `Settings`
   - Now click on `Developer Settings` from the options listed on the left side
   - Inside Developer Settings, click on `Personal access tokens`
   - Press `Generate new token`
   - Check mark - `repo`, `write:org` and `read:org`
   - Add a note in the text box provided (eg: Workshop token), scroll down and click `Generate token`
    <img width="1077" alt="Screenshot 2022-05-16 at 8 21 35 PM" src="https://user-images.githubusercontent.com/17411453/168621229-03081cd0-98fe-4e68-a9d5-a1326f28d719.png">
   - Copy the token. Keep the tab open in case you loose the token. 

Add to Actions secret
  - In your forked repository, go to `Settings`
  - Click on `Secrets` option listed on the left side. Then click on `Actions` option.
  - Click on `New repository secret`
  - In Value text box, paste the PAT token generated in the previous step.
  - In Name, enter `ACTIONS_TOKEN`
  - Click on `Add Secret`
  - You can see that the secret is added.
    <img width="1269" alt="Screenshot 2022-05-16 at 8 33 38 PM" src="https://user-images.githubusercontent.com/17411453/168623826-eff2dca9-cdff-414a-9e85-8c3203b33fc9.png">


## Add init steps : 
https://github.com/Josh-01/vigilant-waffle/blob/master/workshops/workshop-1/1_initialize-project-management.md 

