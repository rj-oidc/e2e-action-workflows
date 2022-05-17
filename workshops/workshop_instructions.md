# Constellation Workshop Instructions: End to end software workflows with GitHub Actions

<------image here----->

:bookmark: The following instructions will take on the assumption that you will be completing the steps on the GitHub UI. Feel free to use the terminal or any other GUIs you are comfortable with.

# Set up

This section will focus on setting up the organisation and repository. It will do the following :

1. Setup community health files, as per the [documentation](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).
2. Setup labels for the entire org

This helps in initialising the organization and repository with relevent information which would be used in later part of SDLC.

## Create an organization

1. Log into your GitHub account and create an organization for yourself where we will create/fork all workshop related repos. Eg : `TauhidWorkshopOrg`.

## Fork e2e-action-workflows repository into the org

1. Fork [e2e-action-workflows](https://github.com/Josh-01/vigilant-waffle). 

    - Open the [e2e-action-workflows](https://github.com/Josh-01/vigilant-waffle) in a browser
    - Sign in to your GitHub account from top right if not signed-in already.
    - Fork this repository into your user account (using `Fork` option on top right of the screen). This repository will get forked as `<org_name>/e2e-action-workflows`
    
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
  - In your organization, go to `Settings`
  - Click on `Secrets` option listed on the left side. Then click on `Actions` option.
  - Click on `New organization secret`
  - In Value text box, paste the PAT token generated in the previous step.
  - In Name, enter `ACTIONS_TOKEN`
  - Click on `Add Secret`
  - You can see that the secret is added.
    <img width="992" alt="image" src="https://user-images.githubusercontent.com/58063491/168744641-32ec16ed-a93a-469d-ae94-59c132b7fdbc.png">


## Add init steps : 
[Initialize the repos](workshop-1/1_initialize-project-management.md)

