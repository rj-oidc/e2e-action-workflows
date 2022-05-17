# Constellation Workshop Instructions: End to end software workflows with GitHub Actions

![Screenshot 2022-05-17 at 10 05 52 PM](https://user-images.githubusercontent.com/17411453/168863150-ce397bf3-1c1b-464f-8039-2cfd38b11e46.png)

:bookmark: The following instructions will take on the assumption that you will be completing the steps on the GitHub UI. Feel free to use the terminal or any other GUIs you are comfortable with.

# Set up

This section will focus on setting up the organisation and repository which we will use for the workshop. 

## Create an organization

1. Log into your GitHub account and create an organization for yourself where we will create/fork all workshop related repos. Eg : `E2EAuto`.
 -> Go to top right corner -> Your organizations
<img width="442" alt="image" src="https://user-images.githubusercontent.com/58063491/168848388-f3d73027-7bd9-4b47-881d-de8cb37e55dd.png">
 -> `New organization`
<img width="897" alt="image" src="https://user-images.githubusercontent.com/58063491/168848466-03e598b5-2a06-4468-a709-0c2552fb1249.png">
 -> Choose a plan -> Choose **Free**
<img width="1424" alt="image" src="https://user-images.githubusercontent.com/58063491/168848586-4d90be47-d7d2-4303-ac38-e7ba7398e54f.png">
 
 -> Create
 
 
## Fork e2e-action-workflows repository into the org

1. Fork [e2e-action-workflows](https://github.com/Josh-01/vigilant-waffle). 

    - Open the [e2e-action-workflows](https://github.com/Josh-01/vigilant-waffle) in a new tab
    - Sign in to your GitHub account from top right if not signed-in already.
    - Fork this repository into the new org (using `Fork` option on top right of the screen). This repository will get forked as `<new_org_name>/e2e-action-workflows`
    
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


## Exercise 1 :
[Project Management Automation](exercise-1/1_repo-project-management.md)

