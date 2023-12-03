# Local

Note :-

- In this project we are using 2 X Ubuntu for this project.
- Install Jenkins using these [steps](../../01-Jenkins-installation/install.md).

## Project title => Declarative Pipeline Deploying code on remote server

### Steps on Master

#### Required

- to build pipeline
- Jenkins

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

### Steps on Agent

#### Required

- to run jobs
- Java
- docker/docker-compose, if job running with them.

#### Step 1 -

### Steps to connect form Master to Agent

#### Required

- SSH

#### [On Master]()

#### Step 1 - Generate SSH key-pair

- Goto `cd ~`, that is, Home dir.
- Goto `cd .ssh/`
- To generate key-pair -> `ssh-keygen`.
  - This will create `rsa` type of key.
  - If `rsa` dosen't work then `ssh-keygen -t ed25519` this will create key `ed25519` type keys.
- This will create two files `id_rsa` (private key will be in master) and `id_rsa.pub` (public key will be in agent).
- id_rsa id_rsa.pub

#### [On Agent]()

#### Step 2 - Put the Public key on Agent

- Copy the content of public key `id_rsa.pub`.
- Paste it in `authorized_keys` file located inside `.ssh/` dir.

#### [On Master]()

#### Step 3 - Try to connect to Agent from Master

- `ssh user@IP`

### Steps to connect form Jenkins to Agent

#### Step 1 -

Note :- `built-in-node` is master itself.

- Goto Manage Jenkins form Dashboard.
- Click on `Set up agent`.
  - Give a node name `dev-node`.
  - Type -> click on `Permanent Agent`.
  - Click Create.
- Now a form appears.

  - Name
  - Description
  - No of executers = at a time how many jobs to run, depent on no of CPU ypu have.
  - Remote root dir = On the agent machine create a dir and give its full path here, this will the root dir.
  - Lables = this is the tag/lable that is written on jenkinsfile below pipeline in agent. `dev-server`
  - Usage
    - Use this node as much as possible = lable match or it will run on this node.
    - Only build jobs with lable expression matching ... = nodes that have the matching lable will only run on this node.
  - Launch Method = Launch method via SSH
    - Host = agent's public address or IP address.
    - Credentials = Create new Credentials. Add private key in Jenkins.
    - Host key Verification Strategy = Non Verifying verification strategy == after SSh verification is not done.
    - Click on `save`.

- Click on the name of the node you just created.
  - Launch Agent.
  - If Authentication fails. Create new key-pair with different algorithms.
