# OS-Climate Data Commons Developer Guide: Setup Initial Environment

This section covers how to  setup your development environment as a contributor to OS-Climate Data Commons developing a data ingestion or processing pipeline. The setup is based around use of OS-Climate GitHub, and a Jupyter Hub / Elyra service provided as a management development platform built to support the needs of our contributors.

## 1. Create new GitHub repository for pipeline development

In order to have a standardized structure that can be easily understood by data scientists, devops engineers and developers, repositories should be created by using one of the project templates:

- [Template for Data Science projects][1]
- [Template for Data Pipeline projects][4]

You can click the `Use the template` button provided in the repository and create the structure for your repo this way.   *Take care to select **OS-Climate** as the owner; the default is to create under your own GitHub ID, which may not be your intention if you are contributing to OS-Climate.*

![Repository Template](../images/developer_guide/aicoe-project-template.png)

 Having a defined structure in a project ensures all the pieces required for the ML and DevOps lifecycles are present and easily discoverable and allows managing library dependencies, notebooks, test data, documentation, etc. For more information on this topic, we recommend reading and understanding the [Cookiecutter Data Science][2] documentation, on which our standard repository template is inspired.

## 2. Make your repository open-source friendly

1. Add the APL 2.0 Open Source license to your repository. This is done by going into your repository, creating a new file called "LICENSE", clicking the button `Choose a license template` on the right, selecting the Apache License 2.0 template and then committing the proposed change.

![Open Source license](../images/developer_guide/repo-choose-license.png)

2. Explain what the repository is about in the "README.md" file created in the repository root.

3. Document the contribution structure of your repository for you and your trusted collaborators in the "OWNERS" file found in the repository root.

4. Confirm whether DCO / CLA covers this repository.

## 3. Access the development environment with Elyra images on JupyterHub

With your GitHub credentials and once you are part of the team odh-env-users, you will be able to access the development environment.

1. Click this [link][2] to access and select githubidp for authentication.

![Jupyter Hub Login](../images/developer_guide/jupyterhub-login.png)

2. Select the image called `Elyra Notebook Image` and `Large` for container size.

![Jupyter Hub Server Start](../images/developer_guide/jupyterhub-startserver.png)

3. Your server should start automatically after a couple of minutes and the Jupyter launcher appear.

![Jupyter Hub Launcher](../images/developer_guide/jupyterhub-launcher.png)

## 4. Set your credentials environment variables

From the File menu, create a new text file called `credentials.env`. You can copy this file from [this link](https://github.com/os-climate/os_c_data_commons/blob/main/docs/credentials.env). This example file includes a link to the JWT token retrieval client for Trino access.

To secure and restrict the access to data based on user profiles, we have defined role-based access controls to specific schemas in Trino based on your team assignments. Therefore, authentication with the Trino service has been federated with GitHub SSO and on a weekly basis you will need to retrieve a JWT token from this [Token Retrieval Client][3]. Get the token and cut / paste the token string as your TRINO_PASSWD in the credentials file.

Care should be taken to never commit the credentials.env file to your repository. Our template repos have this file listed in the .gitignore, so that it cannot be committed. If any changes are made to the repository structure or .gitignore file, it is important to make sure that this exclusion is still in place. If credentials are ever exposed publicly, please contact security@lists.os-climate.org immediately.

## 5. Access your repo using Jupyterlab Git Extension

Once you are in the Jupyterlab UI, you can use the Git extension provided to clone this repo.

1. Click the Git extension button from Jupyterlab UI and select `Clone a repository`:

![Cloning a Git repository](../images/developer_guide/jupyterhub-gitclone.png)

2. Enter the HTTPS address of the repository you want to clone. If it is private and you have access, enter your credentials when requested.

3. You are ready to go!

## Next Step

[Explore notebooks and manage dependencies](./explore-notebooks-and-manage-dependencies.md)

[1]: https://github.com/os-climate/data-science-template
[2]: https://jupyterhub-odh-jupyterhub.apps.odh-cl2.apps.os-climate.org/
[3]: https://das-odh-trino.apps.odh-cl2.apps.os-climate.org/
[4]: https://github.com/os-climate/data-pipeline-template
