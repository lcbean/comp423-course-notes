# Setting Up a Dev Container for Go

* Primary author: Lindsay Bean https://github/lcbean
* Reviewer: Amelia Spell https://github.com/amspell04 

# Prerequisites

Before beginning this tutorial, make sure you have:

* **A Github account**: If you dont have one yet, make sure to sign up at [Github](https://github.com)
* **Git installed**: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you haven't already. 
* **Visual Studio Code (VSCode) Text Editor**: Download and install [VSCode](https://code.visualstudio.com/download)
* **Docker installed**: [Install Docker](https://www.docker.com/products/docker-desktop/). This is required to run the dev container. 
* **Command-line basics**



# Part I: Creating a Repository Git

## Step 1: Create a Local Directory and Initialize Git

A. Start by opening your local terminal or command prompt

B. Create a new directory for your project by running the following lines of code: 

```
mkdir new-go-project
cd new-go-project
```
C. Initialize a git repository: 
```
git init
```

D. Create a README file for your Go project: 
```
echo "# My first Go project" > README.md
echo "Instructions to setup development container thanks to: https://github.com/lcbean/comp423-course-notes" >> README.md
git add README.md
git commit -m "Initial commit with README"
```

## Step 2: Create a Remote Repository on GitHub

A. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page. 

B. Fill in the following details: 

* **Repository Name**: new-go-project
* **Description**: "My first Go project!"
* **Visibility**: Public

C. Do not initialize the repository with a README, .gitignore, or license

D. Click **Create Repository** 


## Step 3: Link your Local Repository to GitHub

A. Add the GitHub respository as a remote by running the following in your terminal: 

```
git remote add origin https://github.com/<your-username>/new-go-project.git

```

B. Check your default branch name with the subcommand ``` git branch ```. If it is not ```main```, rename it to ```main``` with the following command:

```
git branch -M main
```
!!! tip 
    Note that old versions of ```git``` choose the name ```master``` for th primary branch, but these days ```main``` is the standard primary branch name. 



C. Push your local commits to the GitHub repository: 
```
git push --set-upstream origin main
```

D. Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use ```git log``` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository

    
# Part II: Setting up the Development Environment

## Step 1: Add Development Container Configuration

A. In VS Code, open the new-go-project directory you made previously. You can do this via: File > Open Folder. 

B. Install the **Dev Containers** extension for VS Code. 

C. create a ```.devcontainer``` directory in the root of your project with the following file inside: 
```
.devcontainer/devcontainer.json
```

The ```devcontainer.json``` file defines the configuration for your development environment. In this file, we are specifying the following: 

* ```name```: Descriptive name for the dev container. 
* ```image```: Which Docker image to use, in this case, a base image from Microsoft for the latest version of a Go environment
* ```customizations```:  Adds useful configurations to VS Code, like installing the Go extension. 
* ```postCreateCommand```: A command to run after the container is created. We will use ```go version``` to prove a recent version of Go

Place the following code in your ```devcontainer.json``` file: 
```
{
  "name": "New Go Project",
  "image": "mcr.microsoft.com/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["ms-python.python"]
    }
  },
  "postCreateCommand": "go version",
}

```

## Step 2: Reopen the Project in a VSCode Dev Container

A. Use the shortcut ```Ctrl+Shift+P``` (or ```Cmd+Shift+P``` on a Mac)

B. Type "Dev Containers: Reopen in Container," and select the option when it comes up. Wait while the image is downloaded. 

C. Once setup is complete, close the current terminal tab (you can click the trach can icon in VSCode), open a new terminal, and try running ```go version``` to ensure the dev container is running a recent version of Go.


# Write Your first Project in Go!

Now that you are working in your dev container, it's time to write a simple Hello World program. 

A. Start by opening a terminal in your new-go-project directory
B. Make sure you are working in your dev container! 
C. Enable dependency tracking for your code with a go.mod file by running the ```go mod init``` command
    * This gives it the name of the module your code will be in, in this case, the path to the github repository where your code is stored

``` got mod init https://github.com/<your-username>/new-go-project```

D. In VSCode, create a file hello.go in which you will write your code

E. Paste the following code into the hello.go file and save the file: 
```

package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}

```

F. Go back to your terminal and run your code:
``` go run . ```

!!! Note: The go run command is one of many go commands you can use to get things done









## Sources: 
* [Go Tutorial](https://go.dev/doc/tutorial/getting-started)

