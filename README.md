# git-docker-two-remotes
Explanation of how to setup a scenario for a docker project with two git repositories.

# Structure

```
.
+-- .gitignore
+-- docker-compose.yml
+-- docker
|   +-- container_1
|   |   +-- Dockerfile
|   |   +-- volume_1
|   |   |   +-- file.txt
|   |   |   +-- code
|   |   |   |   +-- index.html
```

On the above example, the folder *./docker* contains the containers configuration files and inside *./docker/container_1/volume_1/code* are the application code itself. 
The idea here is that the container will share de *code* folder with the local machine.

## Problem to solve

The company I'm working for needs to store only the application code in a specific GIT repository. The docker configuration files don't need to be there, since they only want to receive the containter image file ready. But I want to keep track of all files.

## Solution

The solution is to store the whole thing in one repository and create another just for the *./docker/container_1/volume_1/code* folder.

To do this, I'll use **git subtree**

# How to

First, I created the respository to store everything (docker + application source), and cloned it:
```bash
git clone https://github.com/saulosch/complete-repo-with-docker-and-project-files.git
```
Then 

cd teste-repo-1
git subtree add --prefix=code https://github.com/saulosch/teste-repo-2.git master
git subtree push --prefix=code https://github.com/saulosch/teste-repo-2.git master
