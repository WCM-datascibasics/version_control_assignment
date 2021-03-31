## Chapter 3 Assignment

From this point onwards, you will be managing your assignments with `git` and submitting them through GitHub. The aim of this assignment is to get you familiarized with a common version control workflow.

#### Getting Started
Make sure you've <em>forked</em> this repository under your own GitHub account, and then clone your own repository to your computer. You will push the changes you've made to this document as submission to GitHub.

If the version control concepts or `git` commands are still confusing to you, consider re-reading and following the online notes, or check out an interactive tutorial like [Learn Git Branching](https://learngitbranching.js.org/).

#### The Assignment:
 0. Create a branch in this assignment repository named `submission`, then list all the branches you have (Hint: look at the Branch chapter of notes on how branches work, how to create new ones, and check existing branches):

    ```bash
    
    git branch submission
    git branch
    * main
      submission
    ```

 1. List the current `remote` name and hyperlink destination of this assignment repository (Hint: if you are not sure, add `--help` after your command to check remotes.). 

    ```bash
    
    git remote -v
    origin	https://github.com/matthewbredder/version_control_assignment.git (fetch)
    origin	https://github.com/matthewbredder/version_control_assignment.git (push)
    ```


 2. Add a second remote destination named `upstream` to your assignment repository, `upstream` is a common name used for the repository that people have forked from, in our case, the `upstream` will be at `https://github.com/WCM-datascibasics/version_control_assignment`. List the new list of remotes after you've added the new remote. 
 
    ```bash
    
    git remote add upstream https://github.com/WCM-datascibasics/version_control_assignment
    
    git remote -v
    origin	https://github.com/matthewbredder/version_control_assignment.git (fetch)
    origin	https://github.com/matthewbredder/version_control_assignment.git (push)
    upstream	https://github.com/WCM-datascibasics/version_control_assignment (fetch)
    upstream	https://github.com/WCM-datascibasics/version_control_assignment (push)
    ```

 3. Save your modifications to this file so far and create a commit indicating you've answered the first 2 questions. Then try pushing the changes to the `upstream` destination on GitHub. What happens? Explain in your own words why does this happen? What are the benefits of having this `upstream` remote added when working collaboratively (Hint: read git command outputs!)?
    ```bash
    git push upstream
    #permission was denied
    ```

    > I was not able to commit my changes to the upstream remote since I didn't have the approriate permissions. Having    the upstream remote enables control of who can make modifications.


 4. Now clone the repository for the [class website](https://github.com/WCM-datascibasics/wcm-datascibasics.github.io), and in the class website repository:
    - a. Explore the version history by visualizing it as a graph (remember the dog meme?).
        ```bash
        git log --graph
        * commit 208edcff191317e62ebd8535c01e160b57dac856 (HEAD -> master, origin/master, origin/HEAD)
        | Author: Xihe Xie <axiezai@gmail.com>
        | Date:   Sun Mar 28 22:55:16 2021 -0400
        | 
        |     last lecture
        | 
        * commit f83956f3a53915994f4a38762e18734636f3ec10
        | Author: Xihe Xie <axiezai@gmail.com>
        | Date:   Sun Mar 21 22:56:37 2021 -0400
        | 
        |     added week 8
        | 
        * commit 1446124c74d0c826ef383e292ef8ca9eb74363ad
        | Author: Xihe Xie <axiezai@gmail.com>
        | Date:   Sun Mar 7 23:31:04 2021 -0500
        | 
        |     add week 6
        | 
        * commit 540a90d6e913eb56af5bc88a3e5fa8df928df53b
        | Author: Xihe Xie <axiezai@gmail.com>
        | Date:   Sat Feb 27 18:55:21 2021 -0500
        | 
        |     added week5

        ```

    - b. Who was the last person to modify `README.md`? (Hint: use `git log` with an argument)
        ```bash
        git log README.md
        commit 00e8ae51a08a0f3754ab228f62b51651595c4426
        Author: Xihe Xie <axiezai@gmail.com>
        Date:   Mon Dec 28 16:01:51 2020 -0500

           readme and try new size
        ```
    
    - c. What was the commit message associated with the last modification to the `-Week 2` line of `index.md` file? (Hint: use `git blame` and `git show`, check out their help pages if you are not sure what to do)
    - added ch2 assignment
        ```bash
        git blame index.md
        git log -p c152f3c8
        
        commit c152f3c84fc4b2f30ec1a5768bd1d0de4cef38d8
        Author: Xihe Xie <axiezai@gmail.com>
        Date:   Sun Jan 3 15:00:09 2021 -0500

           added ch2 assignment
        
        ```

 5. In the course website repository (or another repository you want to clone from GitHub), modify one of its existing files, do not `git add` or `git commit` yet:
     - a. What happens when you do `git stash`, be specific about what happens to your uncommitted changes after `stash`.?
       > It says: "Saved working directory and index state WIP on master: 208edcf last lecture", but then the changes I            made disappeared.
       
     - b. What do you see when you run `git log --all --oneline` after stashing your modification?
       > e72b504 (refs/stash) WIP on master: 208edcf last lecture
     - c. Look up what `git stash drop` and `git stash pop` does, either Google or use `--help`. Run `git stash drop` to undo what you did with `stash`, in what scenario might `stash`-ing, `pop`-ing, and `drop`-ing be useful?
       > It could be useful if you stashed something by accident.

 6. One common mistake when learning `git` is to commit large files that should not be managed by `git` or adding sensitive information like security keypairs for Amazon Cloud Services. Navigate back to your assignment repository and try adding a random text file to the repository (use `touch`), making some modifications and commits to your repository, and deleting that file with `rm`. But deleting with `rm` will not delete that file's recorded git history, therefore we need to do a little more. You may want to look at [this](https://help.github.com/articles/removing-sensitive-data-from-a-repository/))

    > I added 2 text files and then got rid of them.


 7. Like many command line tools, `git` provides a configuration file (or dotfile) called `~/.gitconfig`. Create an alias in `~/.gitconfig` so that when you run `git graph`, you get the output of `git log --all --graph --decorate --oneline`. You can do this by directly modifying the `~/.gitconfig` file or by using the `git` command line functionality.
    ```bash
    [alias]
        graph = log --all --graph --decorate --oneline
    ```
    This is also a good opportunity to turn your dotfiles folder into a version controlled repo (Use `git init` in your dotfiles folder), make it private if you have sensitive `ssh` configurations there (IP Addresses), else feel free to make it public. (This is for your own benefit, not part of the assignment grading)

 8. You can define global ignore patterns in `~/.gitignore_global` after running `git config --global core.excludesfile ~/.gitignore_global`. Do this, and set up your global `gitignore` file to ignore OS-specific or editor-specific temporary files, like `.DS_Store`, or `.vscode`. Feel free to Google around for common gitignore entries for Python projects or other projects of your interest.

    ```bash
    # Mac
    .DS_Store

    # VSC
    .vscode/
    ```

 9. Push the `submission` branch of your repository to your GitHub remote. Your remote `main`/`master` branch should be unchanged since your fork. Now go to your GitHub repository settings and add `axiezai` as a collaborator. Now create a pull request to merge the changes from `submission` to `main`/`master`, assign your TA `axiezai` as a reviewer. You will receive feedback and grades through the pull request review.
