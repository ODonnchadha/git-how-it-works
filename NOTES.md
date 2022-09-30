## How Git Works

- COURSE OVERVIEW:
    - How and why commands work. Created with GIT 2.32.

- GIT IS NOT WHAT YOU THINK:
    - "Procelain" commands: git add. git commit. git push/pull. git branch.
    - "Plumbing" commands: git cat-file. git hash-object. git count-objects.
    - Know the concepts. Learn the model. 
    - Versions: git switch versus git checkout.
    - Wrapping your head around GIT. Leyered, like an onion. A distributed revision control system.
        - The stupid content tracker:
            - A persistent map. Keys to values.
            ```javascript
                echo "Apple Pie" | git hash-object --stdin
            ```
            - Every object in GIT has its own SHA1. Collisions? Perhaps. Good luck.
        - Persistence?
            ```javascript
                git init
                git branch -m main
                echo "Apple Pie" | git hash-object --stdin -w
                open .git
                git cat-file [object hash] -p
            ```
            - Create a rewpository with a master branch with a hidden .git directory. Rename to main. Save to repository.
            - within objects\23. 23 is the start of the object hash. stored in BLOB via type: (git cat-file [object hash] -t)
        - First commit:
            ```javascript
                tree .
                git init
                git status
                git add menu.txt
                git add recipes/
                git status
                git commit -m "First commit."
                git status
                git log
                open .git
                git cat-file -p [object hash]
            ```
            - To commit, place first in staging. Always verify after with status. Then commit. Log allows the history with associated hash.
            - A commit is compressed, like a BLOB. A vcommit is a simple, short piece of text. And the hash of a tree. So, trees and BLOBs.
            - A BLOB is the content of a file. Permissions are stored within the tree pointer.
        - Versioning made easy!
            ```
                git cat-file -p [object hash]
            ```
            - After a second commit, we now have a parent. With a brand new tree. 
            - A new BLOB with every file change. Optimization layer: (GIT can manage a delta with a tiny file change.)
        - Annotated tags:
            - Similiar to a commit. Another type of .git database object.
        - What GIT really is:
            - A high-level (virtual/version) file system built on top of the native file system.

- BRANCHES DEMYSTIFIED:
    - The next layer. What a branch really is:
    ```javascript
        git branch
        cat .git/refs/heads/main
        git branch [BRANCH_NAME]
        git branch
        git add recipes/apple_pie.txt
        git commit -m "Added apple pie recipe."
        git switch [BRANCH_NAME]
        git checkout [BRANCH_NAME]
        git add recipes/apple_pie.txt
        git status
        git commit -m "Add tweaked apple pie recipe."
    ```
    - GIT places branches within refs/heads. A branch is just a references to a commit.
    - Use 'git branch' to display the branches. NOTE the * that states current branch.
    - NOTE: HEAD is just a reference to a branch.
    - 'switch' is a relatively recent command.
    - (1) GIT changes HEAD to the switched directory. 
    - (2) After switch, the files and folders within the working directory are replaced with the files and folders of the commit.
- Let's merge:
    ```javascript
        git switch main
        git merge [BRANCH_NAME]
    ```
    - Merge changes from one branch into main branch. Receiving BOTH MODIFIED warning.
    ```
        <<<<<<< HEAD
        Granny Smith apples
        =======
        1 tablespoon cinnamon
        10 Granny Smith apples
        >>>>>>> [BRANCH_NAME]
    ```
    ```javascript
        git status
        git add recipes/apple_pie.txt
        git status
        git commit
    ```
    - Receive "both modified" status. Add the file 
- REBASING MADE SIMPLE:

- DISTRIBUTED VERSION CONTROL:
