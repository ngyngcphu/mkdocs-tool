# Git Workflow

## Introduction
This training is based on the git-workflow that the TickFlow team worked on and other references on the internet.

## The main branches
A repository must have at least these two main branches:
<div class="annotate" markdown>

1. **main**: where the source code is stable and has been released to production.  
2. **develop**: where the source code is latest, ready to be merged into the **main** branch for the next release.

</div>

**<u>Note</u>**: All branches above are protected to prevent direct commit.  

Follow these steps:  
 1. Clone a repository on github, example: [https://github.com/ngyngcphu/mkdocs-tool](https://github.com/ngyngcphu/mkdocs-tool)  
 2. Connect repository from local to remote:  
    ```
    git remote add origin <remote_url>
    ```  
 3. Push branch **main** up to remote:  
    ```
    git push origin main
    ```  
 4. Create branch **develop** from **main**:  
    ```
    git checkout -b develop main
    ```  
 5. Push branch **develop** up to remote:  
    ```
    git push origin develop
    ```  
 6. Set protection rules for 2 branches: **main** and **develop** at `Settings->Branches->Add branch protection rule`.  

## The supporting branches
Besides the main branches, there will be support branches so that team members can work in parallel, easily track features, prepare for release or quickly fix production issues. These support branches will be **deleted** after using, including:  
1. Feature branches  
2. Release branches  
3. Hotfix branches
### Feature branches
- Branch off from: **develop**
- Merge back into: **develop**
- Branch naming convention: **feature/**

Feature branches are used to develop new features for the upcoming releases. Each feature will be a separate branch, created from the latest source code of **develop**, example: **feature/project**, **feature/member**,... After completing the features, features branch will be merged into **develop** and deleted.  
Follow these steps:  
1. Create a feature branch, ex: **feature/part_1** from **develop**:  
    ```
    git checkout -b feature/part_1 develop
    ```  
2. Make some changes to **feature/part_1**  
3. Commit and push **feature/part_1** up to remote:  
    ```
    git push origin feature/part_1
    ```  
After completing all the code in **feature/part_1**, make a Pull requests to **develop**, add reviewers.  
**<u>Note</u>**: All conversations on code must be resolved before a pull request can be merged into a branch.  
After pull request has been merged into **develop** branch on remote. At local, checkout **develop**, delete **feature/part_1** and pull latest code from remote.
```
git checkout develop
git branch -D feature/part_1
git pull origin develop
```
**Note**: A pull request must not exceed **20 files changed**. If the feature is too big (> 20 files changed), it should be split into sub-branches, like that: **sub-feature-part_1/search-project**,...Then, make a pull request from **sub-feature-part_1/search-project** to **feature/part_1**.
