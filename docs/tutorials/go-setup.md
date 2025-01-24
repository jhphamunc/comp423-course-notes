# **Setting up a dev container for Go**

* Primary author: [Joseph Pham](https://github.com/jhphamunc)

## Prerequisites

1. GitHub Account: Login or create an account [here](https://github.com/)
2. Visual Studio Code (VS Code): Download and install [here](https://code.visualstudio.com/)
3. Git: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if it isn't already installed
4. Docker Installed: Download and install [here](https://www.docker.com/products/docker-desktop/)

## **Creating a new Dev Container in Go**

### Step 1: Create a New Project Directory

1. Open a terminal and create a new directory using this code:  
    ```bash
    mkdir my-new-project
    cd my-new-project 
    ```

2. Initialize a Git Repository:  
    ```bash
    git init  
    ```

### Step 2: Create a Dev Container for Go

1. In VS Code open the my-new-project directory. Which can be done by going to File->Open Folder

2. Install "Dev Container" in the extension portion of GitHub

3. Create a .devcontainer directory in the root of your project with the following file inside of this "hidden" configuration directory:
    ```  
    .devcontainer/devcontainer.json
    ```

4. In this devcontainer file we define the configuration for our development environment. Add this to devcontainer.json
```
{
    "name": "Go Dev Container",
    "image": "mcr.microsoft.com/devcontainers/go:latest",
    "customizations": {
        "vscode": {
            "extensions": [
                "golang.go"
            ]
        }
    },
    "postCreateCommand": "go version"
}
```

- ```name```: The name of the Dev Container project
- ```image```: The official Go Dev Container image which is given by Microsoft
- ```customizations.vscode.extensions```: Ensures that the Go extension is downloaded
- ```postCreateCommand```: runs the ```go version``` command after the container is started

### Step 3: Open the Project in the Dev Container

Reopen the container by using the command palette (Ctrl+Shift+P or Cmd+Shift+P on macOS) and select: **Dev Containers: Reopen in Container**. This might take a minute for the image and downloads to be installed.

Once the new Dev Container is setup, close out of the current terminal and open a new terminal tab within VS Code using ```go version``` to see if the container is running the newest version of Go.

### Step 4: Initialize a new Go Module

1. Create a go.mod file using the mod subcommand found in Go  
```
go mod init github.com/<username>/go-dev-container
```

### Step 5: Write the "Hello COMP423" Program

Using echo we can create a main.go file

```bash
echo 'package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}' > main.go
```

### Step 6: Compile and run main.go

We can directly run the program with the run subcommand:
```bash
go run main.go
```
Output:
```
Hello COMP423
```
Or we can use the build subcommand:
```bash
go build -o hello
```
- This creates an executable file named ```hello```   

Then we can run the file using:
```bash
./hello
```
Output:
```
Hello COMP423
```

### What is the difference between run and build?
- ```go run```:  
    - Compiles and executes the program in one step
    - Only temporary and no binary is saved
- ```go build```:  
    - Compiles the program into a reusable binary (ex "hello")
    - Similar to gcc in COMP211 where we had a.out
- Key Difference:  
    - go run is used for quick testing
    - go build is used when you need to repeatedly run a program