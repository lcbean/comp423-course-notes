# Setting Up a Dev Container for Go

* Primary author: [Lindsay Bean](https://github/lcbean)
* Reviewer: [Amelia Spell](https://github.com/amspell04)

In this tutorial, you will learn how to set up a dev container for the programming language Go, as well as how to create your first Go project. We will go over how to create a git repository, set up your development container, and run a simple "Hello COMP423" program in Go! 

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
echo "Instructions to setup development container thanks to: https://lcbean.github.io/comp423-course-notes/tutorials/go-setup/" >> README.md
git add README.md
git commit -m "Initial commit with README"
```

## Step 2: Create a Remote Repository on GitHub

A. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page. 

B. Fill in the following details: 

* **Repository Name**: new-go-project

* **Description**: "My first Go project!"

* **Visibility**: Public

C. Do **not** initialize the repository with a README, .gitignore, or license

D. Click **Create Repository** 


## Step 3: Link your Local Repository to GitHub

A. Add the GitHub repository as a remote by running the following in your terminal: 

```
git remote add origin https://github.com/<your-username>/new-go-project.git

```

!!! note

    Remember to plug in your username! 

B. Check your default branch name with the subcommand ``` git branch ```. If it is not ```main```, rename it to ```main``` with the following command:

```
git branch -M main
```
!!! note 
    Old versions of ```git``` choose the name ```master``` for th primary branch, but these days ```main``` is the standard primary branch name. 



C. Push your local commits to the GitHub repository: 
```
git push --set-upstream origin main
```

D. Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use ```git log``` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository

    
# Part II: Setting up the Development Environment

## Step 1: Add Development Container Configuration

A. In VS Code, open the new-go-project directory you made previously. You can do this via: File > Open Folder. 

B. Install the **Dev Containers** extension for VS Code from the extensions tab. 

C. Create a ```.devcontainer``` directory in the root of your project with the following file inside: 
```
.devcontainer/devcontainer.json
```

Place the following code in your ```devcontainer.json``` file: 
```
{
  "name": "New Go Project",
  "image": "mcr.microsoft.com/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["ms-vscode.go"]
    }
  }
}

```

!!! info "What does it all mean?"

    The ```devcontainer.json``` file defines the configuration for your development environment. In this file, we are specifying the following: 

    * ```name```: Descriptive name for the dev container. 
    * ```image```: Which Docker image to use, in this case, a base image from Microsoft for the latest version of a Go environment.
    * ```customizations```:  Adds useful configurations to VS Code, like installing the Go extension. 
    * ```extensions```: Installs any specified extensions automatically, in this case the official Go VSCode plugin made by the Go Team at Google.
    

## Step 2: Reopen the Project in a VSCode Dev Container

A. Use the shortcut ```Ctrl+Shift+P``` (or ```Cmd+Shift+P``` on a Mac)

B. Start typing "Dev Containers: Reopen in Container" and select the option when it comes up. Note that it may take some time for the image to load once this option is selected.

C. Once setup is complete, close the current terminal tab (you can click the trash can icon in VSCode), open a new terminal, and try running ```go version``` to ensure the dev container is running a recent version of Go.

!!! note
    As of this tutorial, the output should be ```go version go1.23.4 linux/arm64```


# Write Your first Project in Go!

Now that you are working in your dev container, it's time to write a simple Hello World program. 

A. Start by opening a terminal in your new-go-project directory

B. Make sure you are working in your dev container! 
!!! tip "Hint"
    You can check your dev container status by looking at the bright blue rectangle at the bottom left corner of your screen. If you are connected, it should say **"Dev Container: New Go Project..."**.

C. Enable dependency tracking for your code with a go.mod file by running the ```go mod init``` command, giving it the name, or path, of the module your code will be in. In this case, the path will be that of the the directory ```new-go-project``` where your source code is kept. The command should look like:

``` go mod init new-go-project```

!!! info "Why the go mod command?"
    When your code imports packages contained in other modules, you manage those dependencies through your code's own module, which is defined by a ```go.mod``` file that tracks the modules that provide those packages. This file stays with your code, including in the source code repository. The ```go mod``` command essentially tells Go that this is a Go module, and the ```go.mod``` file will contain the name of the module and what version of Go was used to build it. 

D. In your project directory in VSCode, create a file ```hello.go``` in which you will write your code

E. Paste the following code into the ```hello.go``` file and save the file: 
```

package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}

```

!!! info "How does this work?"
    * Declare a main **package**, which is a way to group functions and is made up of all the files in directory.
    * The fmt package contains functions for formatting text, including printing to the console.
    * Implement a main function to print a message to the console. This will execute by default when you run the main package. 

F. Go back to your terminal and enter the 

G. Now you can run your code with the following command:

``` 
go run hello.go 
```

This should output ```Hello COMP423``` in your terminal!

H. In cases where you want to compile your code for testing, but do not want to execute the code, you can run ```go build```to compile the source code into an executable binary. This command is different from ```go run ``` as it does **not** execute the program. 

!!! tip 
    For best practice, run ```go mod tidy``` to clean up unused dependencies before building

!!! note 
    If you do not provide an argument to the ```go build``` command, it will automatically compile the program in your current directory and include all ```.go``` files in the directory. In the case of this tutorial, the command will product an executable file named ```new-go-project```. Go automatically decides the name of the generated executable by using the module created earlier with ```go mod init```. If you want to specify the name of output file: ```go build -o insertname```. If you want to compile only ```hello.go```, run ```go build hello.go```

* Now that you have created an executable, run ```./new-go-project```. The output of the binary should match the output from when you ran the program with ```go run hello.go```: ```Hello COMP423```

I. Now, all that's left to do is commit and push your changes to your github repository! 

``` 
    git add . 
    git commit -m "Hello COMP423"
    git push origin main
```

!!! tip
     The go commands covered in this tutorial are few of many go commands you can use to get things done with Go. You can use ```go help``` to get a list of the others!

## Sources: 
* [Go Tutorial](https://go.dev/doc/tutorial/getting-started)
* [How To Build and Install Go Programs](https://www.digitalocean.com/community/tutorials/how-to-build-and-install-go-programs)

