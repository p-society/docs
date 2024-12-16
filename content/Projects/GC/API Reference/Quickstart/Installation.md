# GC-Broadcast API Installation

This document provides instructions on how to set up and start a running instance of gc-broadcast-api on your local system. The instructions are written to be followed in sequence so make sure to go through each of them step by step without skipping any sections.
# Installation Steps Summary

Installation is not difficult, but there are many steps. This is a brief explanation of what needs to be done:

1. Install `git`
2. Download the code from GitHub using `git`
3. Install `node.js` (Node), the runtime environment the application will need to work.
4. Configure the Node Package Manager (`npm`) to automatically use the correct version of Node for our application.
5. Use `npm` to install TypeScript, the language the application is written in.
6. Install other supporting software such as the database using either:
   1. Docker
   2. A manual setup
7. Configure the application
8. Start the application

These steps are explained in more detail in the sections that follow.

# Prerequisites

In this section we'll explain how to set up all the prerequisite software packages to get you up and running.

## Install git

The easiest way to get the latest copies of our code is to install the `git` package on your computer.

Follow the setup guide for `git` on official [git docs](https://git-scm.com/downloads). Basic `git` knowledge is required for open source contribution so make sure you're comfortable with it. [Here's](https://youtu.be/apGV9Kg7ics) a good tutorial to get started with `git` and `github`.

## Setting up this repository

First you need a local copy of `gc-broadcast`. Run the following command in the directory of choice on your local system.

1. On your computer, navigate to the folder where you want to setup the repository.
2. Open a `cmd` (Windows) or `terminal` (Linux or MacOS) session in this folder.
   1. An easy way to do this is to right-click and choose appropriate option based on your OS.
3. **For Our Open Source Contributor Software Developers:**

   1. Next, we'll fork and clone the `gc-broadcast` repository.
   1. In your web browser, navigate to [https://github.com/p-society/gc-broadcast/](https://github.com/p-society/gc-broadcast/) and click on the `fork` button. It is placed on the right corner opposite the repository name `p-society/gc-broadcast`.
![[Pasted image 20241216131541.png]]
   1. You should now see `gc-broadcast` under your repositories. It will be marked as forked from `p-society/gc-broadcast`

   1. Clone the repository to your local computer (replacing the values in `{{}}`):
      ```bash
      $ git clone https://github.com/{{YOUR GITHUB USERNAME}}/gc-broadcast.git
      cd gc-broadcast
      git switch dev
      ```
      - **Note:** Make sure to check out the `develop` branch
   
## Install node.js

Best way to install and manage `node.js` is making use of node version managers. We recommend using `volta`, which will be described in more detail later.

Follow these steps to install the `node.js` packages in Windows, Linux and MacOS.

1. For Windows:
   1. first install `node.js` from their website at https://nodejs.org
      1. When installing, don't click the option to install the `necessary tools`. These are not needed in our case.
   2. then install [fnm](https://github.com/Schniz/fnm). Please read all the steps in this section first.
      1. All the commands listed on this page will need to be run in a Windows terminal session in the `gc-broadcast` directory.
      2. Install `fnm` using the `winget` option listed on the page.
      3. Setup `fnm` to automatically set the version of `node.js` to the version required for the repository using these steps:
         1. First, refer to the `fnm` web page's section on `Shell Setup` recommendations.
         2. Open a `Windows PowerShell` terminal window
         3. Run the recommended `Windows PowerShell` command to open `notepad`.
         4. Paste the recommended string into `notepad`
         5. Save the document.
         6. Exit `notepad`
         7. Exit PowerShell
         8. This will ensure that you are always using the correct version of `node.js`
2. For Linux and MacOS, use the terminal window.
   1. Use Volta: https://volta.sh/
## Install TypeScript

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It adds optional types, classes, and modules to JavaScript, and supports tools for large-scale JavaScript applications.

To install TypeScript, you can use the `npm` command which comes with `node.js`:

```bash
npm install -g typescript
```

This command installs TypeScript globally on your system so that it can be accessed from any project.

## Install Yarn

Yarn is a fast, reliable, and secure package manager for JavaScript. It is an alternative to npm, offering enhanced speed and features like dependency locking and offline caching, making it suitable for managing large-scale projects.

To install Yarn, you can use the `npm` command (which comes with Node.js) or install it directly via other package managers:

### Install via npm:

```bash
npm install -g yarn
```

This command installs Yarn globally on your system, allowing you to use it across any project.

### Alternative Installation Methods:

- **Homebrew (macOS):**
    
    ```bash
    brew install yarn
    ```
    
- **Chocolatey (Windows):**
    
    ```bash
    choco install yarn
    ```
    
- **Linux:** Use your distribution's package manager or install Yarn via the Yarn repository.
    

Once installed, you can verify Yarn's installation by running:

```bash
yarn --version
```

This will display the installed version of Yarn, confirming that it is ready to use.
## Install Required Packages

Run the following command to install the packages and dependencies required by the app:

```
yarn
```

The prerequisites are now installed. The next step will be to get the app up and running.

# Installation Using Docker

#WIP

# Installation without Docker

There are more steps, but the outcome is the same. A working GC-Broadcast-API instance.

## Install the Required Packages

Install the packages required by `gc-broadcast` using this command:

```
yarn
```

## Install MongoDB

GC-Broadcast makes use of `MongoDB` for its database needs. We make use of `mongoose ODM` to interact with the MongoDB database from within the code.

### Setting up the mongoDB database

We're listing some common approaches to set up a running instance of MongoDB database:

1. `System native database approach:` (Highly Recommended) You can install MongoDB natively on your system and create/connect to the database. Follow the setup guide on official [MongoDB Docs](https://www.mongodb.com/docs/manual/administration/install-community/) for your respective operating system.
2. `Hosted database approach:` MongoDB Atlas is the easiest way to get a running instance of mongodb database. It is a hosted(remote) mongodb database provided by mongodb itself. If you're a beginner and don't want too much of a hassle setting up the database you should use this approach but you should eventually switch to local instance. Follow the setup guide on official [MongoDB Atlas Docs](https://www.mongodb.com/docs/atlas/getting-started/). Mongodb Atlas is just one of the many hosted database solutions. Some issues that you might face while using this are slower tests, slower API requests, dependence on Internet connection etc.
3. `Docker container approach:` If you are fluent in working with docker you should use this approach. Docker is a great way to manage and run applications without natively installing anything on your system. With this you can set up the mongodb database inside a docker container and manage it as per your will. Follow this [video tutorial](https://www.youtube.com/watch?v=uklyCSKQ1Po) to set up a mongodb docker container. You can learn about docker from [Docker docs](https://docs.docker.com/).

## Install Redis

GC-Broadcast makes use of `Redis` for caching frequently accessed data items in the primary database. We make use of `ioredis` to interact with the `redis-server` from within the code. The main Idea is the in production this will act as an in-memory cache. So it is recommended that you set it up locally. However for simplicity purposes, we have added a rediscloud instance of our own in dev branch.

### Setting Up Redis

1. `For Linux Users`: If you are using a Linux distribution, follow these steps to set up Redis:

   1. Open a terminal.

   2. Update the package list:

      ```bash
      sudo apt update
      ```

   3. Install Redis Server:

      ```bash
      sudo apt install redis-server
      ```

   4. Start the Redis service:

      ```bash
      sudo service redis-server start
      ```

   5. Test if Redis is running by running the Redis CLI:
      ```bash
      redis-cli
      ```
   6. Use these parameters when running the setup script if you have configured the server on your local machine:
      1. Redis Host: `localhost`
      1. Redis Port: `6379` (default Redis port)

2. `For Windows Users using WSL`: If you'd rather not deal with the hassle of setting up WSL on your computer, there's another option: you can use a hosted database like Redis Cloud. More details about this are provided below, mainly for when you're working on development tasks. But it's a good idea to set up Redis on your own computer if you can. Right now, Redis isn't supported directly on Windows – you can only install and use it through WSL. If you're a Windows user and want to get Redis working using the Windows Subsystem for Linux (WSL), just follow these steps:

   1. Install WSL (Windows Subsystem for Linux) following the official [WSL Installation Guide](https://docs.microsoft.com/en-us/windows/wsl/install).

   2. Open a WSL terminal.

   3. Update the package list:

      ```bash
      sudo apt update
      ```

   4. Install Redis Server:

      ```bash
      sudo apt install redis-server
      ```

   5. Start the Redis service:

      ```bash
      sudo service redis-server start
      ```

   6. Test if Redis is running by running the Redis CLI:

      ```bash
      redis-cli
      ```

   7. Use these parameters when running the setup script if you have configured the server on your local machine:
      1. Redis Host: `localhost`
      2. Redis Port: `6379` (default Redis port)

3. **Connecting to Redis Cloud**:

   To connect to a Redis cloud service, you will need the host and port information provided by your cloud service provider. Use these values in your application to establish a connection. Typically, the host and port strings are provided in the following format:

   1. Host: `your-redis-host.redisprovider.com`
   1. Port: `6379` (default Redis port)

   Replace `your-redis-host.redisprovider.com` with the actual host provided by your Redis cloud service. You can then use these values in your application's configuration to connect to your Redis cloud instance. You may also have to enter Redis Password and Username for using cloud instance.

Remember to adjust any paths or details as needed for your specific environment. After following these steps, you will have successfully set up Redis.

# Configuration

It's important to configure GC-Broadcast API to complete it's setup.

A configuration file named `.env` is required in the root directory of `gc-broadcast` for storing environment variables used at runtime. It is not a part of the repo and you will have to create it.

## Automated Configuration of `.env`

You can use our interactive setup script to populate the `.env` file using the command below.

This will create a new `.env` file for you, and if one already exists, it will make the updates you require.

# For Development

```
yarn env dev
```

# For Production
```
yarn env prod
```


# Running the application

## Running the Application

Once you have installed all necessary dependencies and set up your project, you can start the application in development mode using the following command:

```bash
yarn dev
```

This command is typically configured in the project's `package.json` file under the `scripts` section. It runs the application in development mode, often enabling features like hot-reloading, live updates, and detailed error reporting for a smooth development experience.

After running the command, the terminal will usually display a URL (e.g., `http://localhost:3000`) where you can access the application in your web browser. 🎉