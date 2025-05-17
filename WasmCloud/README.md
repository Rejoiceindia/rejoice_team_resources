# 🚀 wasmCloud + TypeScript: Local Hello App Setup

This guide walks you through setting up a **local wasmCloud environment** using **WSL (Windows Subsystem for Linux)** and deploying a **Hello App** TypeScript WebAssembly app using `wash`.

---

## 📚 Table of Contents

1. [WSL Installation (Ubuntu)](#-1-install-wsl-on-windows)
2. [Install wasmCloud CLI (`wash`)](#-2-install-wash-cli)
3. [Installing Node.js and Typescript](#-3-installing-node-js-and-typescript)
4. [Set Up Hello App](#-4-create-a-hello-world-app)
5. [Run wasmCloud Dev Host](#-5-run-the-local-wasmcloud-dev-host)
6. [Troubleshooting](#-6-troubleshooting)
7. [Resources](#-7-resources)

---

## 📦 1. Install WSL on Windows

1. Open **PowerShell as Administrator** and run:
This installs Ubuntu as your WSL distro.
   ```powershell
   wsl --install -d Ubuntu
2. When Ubuntu opens, complete the setup (username & password).

    
## 📦 2. Install wasmCloud CLI (`wash`)

1. You need to update git to the latest version using the Ubuntu Git Maintainers' Personal Package Archive (PPA):
    ```shell
    sudo add-apt-repository ppa:git-core/ppa
    ```
    ```shell
    sudo apt-get update
    ```
    ```shell
    sudo apt-get install git
    ```
2. When your WSL environment is ready, you can use the standard Ubuntu/Debian installation method:
    ```shell
    curl -s https://packagecloud.io/install/repositories/wasmcloud/core/script.deb.sh | sudo bash
    ```
    ```shell
    sudo apt install wash
    ```
3. Verify that wash is installed by running:
    ```shell
    wash --version
    ```
## 📦 3. Installing Node.js and Typescript
wasmCloud recommends installing Node.js via nvm (Node Version Manager).

Requirements:
- **npm v14.17+**
- **TypeScript v5.6+**

1. Install nvm:
    ```shell
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
2. Apply changes to the current shell:
    ```shell
    source ~/.bashrc
3. Verify nvm is installed:
    ```shell
    nvm --version
4. Install the latest LTS version of Node.js (which includes npm):
    ```shell
    nvm install --lts
5. Verify installations:
    ```shell
    node -v
    npm -v
6. Install TypeScript (globally):
    ```shell
    npm install -g typescript
7. Verify TypeScript:
    ```shell
    tsc -v
    ```
Verify If the versions are full the required versions (`npm v14.17+` and `TypeScript v5.6+`)

8. (*Optional*) If the **npm** version is less then run this command
    ```shell
    npm install -g npm@latest
    ```
After running this verify the versions again by running the **Step 5** commands


## 📦 4. Set Up Hello App
1. Now that we have installed wash and typescript toolchain, we can create a new component project.
    ```shell
    wash new component hello --template-name hello-world-typescript
    ```
    After a moment, wash will create a new directory called hello with all of the required project files for building a component in Typescipt

2. Navigate to the hello project directory:
    ```shell
    cd hello
3. Install the npm packages for your project:
    ```shell
    npm install
## 📦 5. Run wasmCloud Dev Host
1. From project directory, run:
    ```shell
    wash dev
    ```
2. The wash dev command automatically **builds your WebAssembly component and deploys it to a local wasmCloud environment.** This will take a moment, and the terminal output will update you on the process. The last step should look like this:
    ```text
    ✅ Successfully started host, logs writing to /home/.wash/dev/kSKCGi/wasmcloud.log
    🚧 Building project...
    ...
    ✨ HTTP Server: Access your application at http://127.0.0.1:8000
    👀 Watching for file changes (press Ctrl+c to stop)...
3. By default, the application will run on our local port 8000. In a new terminal tab, we can curl our application:
    ```shell
    curl http://127.0.0.1:8000
    ```
4. The application should return:
    ```text
    Hello from Typescript!
    ```
   
**You just ran a WebAssembly application in wasmCloud!**

## 📦 6. TroubleShooting

Rebuild not working? Stop the dev server and re-run:
```shell
wash dev
```
Check logs for errors in:
```shell
~/.wash/dev/<session-id>/wasmcloud.log
```

## 📦 7. Resources
- [wasmCloud Docs](https://wasmcloud.com/docs)
- [Hello World Guide](https://wasmcloud.com/docs/tour/hello-world/?lang=typescript&os=windows)

