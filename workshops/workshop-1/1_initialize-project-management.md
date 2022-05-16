1. Create Project Board

2. Create .github repo
    To get started, make sure you've created the .github repository within your organization or user account. .github is a special repository for Github-specific community health files, as per the [documentation](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file). [Link to create the repo](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file#creating-a-repository-for-default-files)
    
3. Create issue templates : Copy files from [here](https://github.com/Josh-01/vigilant-waffle/tree/master/workshops/workshop-1/workflows/files
) to .github repo 

4. Create CODEOWNERS file [doc](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners#codeowners-file-location)

5. Create labels 

  - To make sure everything works, you'll need to ensure a personal access token with the public_repository scope is available via the BOT_TOKEN environment variable. The account used to create the PAT must also have permission to edit labels on the repository you want to manage.
  - `manage-your-labels` uses a config file stored at [manage-your-labels.yml](https://github.com/Josh-01/vigilant-waffle/blob/master/.github/manage-your-labels.yml) within the top-level directory of the .github repo for label management.
  - With a valid configuration set up, create a new Actions workflow within the .github repo and set it up like so: [workflow](https://github.com/Josh-01/vigilant-waffle/blob/master/workshops/workshop-1/workflows/1_create-labels.yml)

