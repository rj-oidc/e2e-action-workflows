### Initialization

1. #### Create Project Board

2. #### Fork the repo : https://github.com/actions-automation/.github  ( or fork it out from our repo )
  
  - To get started, make sure you've created the .github repository within your organization. `.github` is a special repository for Github-specific community health files, as per the [documentation](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).
  - Initial files: 
       - Create issue templates
       - Create CODEOWNERS file : [doc](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#codeowners-file-location)
    
3. ####  Create labels for all (or some) repositories across the organization

  - To make sure everything works, you'll need to ensure a personal access token with the `public_repository` scope is available via the `BOT_TOKEN` environment variable. The account used to create the PAT must also have permission to edit labels on the repository you want to manage.
     We will use the organization secret `ACTIONS_TOKEN` to populate `BOT_TOKEN`
 
  - `manage-your-labels` uses a config file stored at [manage-your-labels.yml](https://github.com/Josh-01/vigilant-waffle/blob/master/.github/manage-your-labels.yml) within the top-level directory of the .github repo for label management.

  - Run a new Actions workflow within the .github repo and the labels will get created in all the repos based on the config.

4. #### Workflow for pull requests (We can add it if time permits)
   

 ### Resources : 
- https://github.com/actions-automation 
