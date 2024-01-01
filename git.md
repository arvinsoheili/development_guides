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
    6. Run the following command to set your Git user email:

    ```
    git config --global user.email "email address"
    ```

   Note: Replace `"email address"` with your actual email address.
   

7. Run the following command to set your Git user name:

    ```
    git config --global user.name "farshad badri"
    ```
    

   Note: Replace `"farshad badri"` with your actual name.
8. Run the following command to push the changes to the remote repository:

    ```
   git pull origin main --allow-unrelated-histories
    ```

9. Run the following command to make the initial commit:

    ```
    git commit -m "initial commit"
    ```

10. Run the following command to push the changes to the remote repository:

    ```
    git push -u origin main
    ```

    


