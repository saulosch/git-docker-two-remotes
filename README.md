# git-docker-two-remotes
Explanation of how to setup a scenario for a docker project with two git repositories. This article shows how I did to solve the following problem.

> *Note:* this explanation consider that you already know the basics of Git commands and also the basics concepts of Docker.

## Problem to solve

The company I'm working for needs to store only the application code in a specific GIT repository. The docker configuration files doesn't need to be there, since they only want to receive the containter image file ready. But I want to keep track of all files.

## Solution

The solution is to store the whole thing in one repository and create another just for the *./docker/container_1/volume_1/code* folder.

To do this, I'll use **git subtree**

## Project structure

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

---

# How to

First, create the respository to store everything (docker + application source), and *clone* it:

```bash
git clone https://github.com/saulosch/complete-repo-with-docker-and-project-files.git
```
After that, you can create all the files in the folders (both, docker and application files), commit it and push to remote repository, normally.

```bash
git push origin master
```

Then, create the respository that will contain only the application source and *push* the content of the proper folder to it with the **subtree** command:

```bash
git subtree push --prefix=docker/container_1/volume_1/code https://github.com/saulosch/partial-repo-with-project-files-only.git master
```

> If one or both repositories already exists, you - obviously - don't need to create them. Considering that they are *synchronized*, just clone the repository with everything and start coding.

Done!

> Note: if you know a different way to solve the problem, be my guest and post a issue, so we can learn from each other. =)
