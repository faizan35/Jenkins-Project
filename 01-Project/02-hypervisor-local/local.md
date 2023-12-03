# Local

Note :-

- In this project we are using Ubuntu for this project.
- Install Jenkins using these [steps](../../01-Jenkins-installation/install.md).

## Project title

### Steps

#### Step 1 - Create a new Job

- On Jenkins homepage click on `New Item`.
- Enter an item/Job name and select `Pipeline`.
- Click on OK

#### Step 2 - Configure your pipeline

- `Description` write a description about the project.
- Check the `GitHub project` checkbox.
  - Paste the URL under `Project url`.
    ```bash
    https://github.com/LondheShubham153/node-todo-cicd.git
    ```
  - under `Advanced` tab, give a name under `Display name`.

#### Step 3 - Write Pipeline script

- Under `Pipeline`.
- Under `Definition` choose `Pipeline script from SCM` this will pick `Jenkinsfile` from the GitHub repo.
- Under `SCM` select Git.
- Put some details about the repo like link, branch, Jenkinsfile path, etc.
- Jenkinsfile is explained under [Jenkins-file-explanation.md](./jenkins-file-explanation.md) file.

#### Step 4 - Setting Docker Credentials

This is known as Credential binding.
**Note :-** You should not expose your passwords.

- From Homepage/Dashboard of Jenkins.
- Goto `Manage Jenkins` -> Under `Security` click on `Credentials`.
- Select the scope, click on `global`.
- Click on `Add Credentials`.
- Write the Username and Password.
- Give an ID
