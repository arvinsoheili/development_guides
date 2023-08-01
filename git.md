# GIT

This guide will help you connect a project from the base to the gate and work with it using Git.

### Create a New Empty Repository

The first step is to create a new empty repository on GitHub.

### Connecting Local Project to an Existing Git Repo

To connect your local project to Git, follow these steps:

1. Open your terminal and navigate to the root directory of your project.
2. Run the following command to initialize Git: 

    ```
    git init
    ```
    3. Run the following command to add the remote origin URL:

    ```
    git remote add origin https://github.com/directory/name.git
    ```

   Note: Replace `https://github.com/directory/name.git` with the actual remote origin URL.

4. Run the following command to rename the default branch from `master` to `main`:

    ```
    git branch -M main
    ```

5. Run the following command to stage all changes:

    ```
    git add .
    ```
