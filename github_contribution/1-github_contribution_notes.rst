Development Notes: GitHub Contributions
=======================================


Setup
-----

1. Fork project on Github

2. Clone forked project locally::

    # Copy forked project URL on GitHub
    git clone <forked-project-URL>

3. Set up remotes to keep fork and original synced::

    # Copy original project URL on GitHub
    cd <project-folder>
    git remote add upstream <original-project-URL>

4. Create a new branch for development work::

    git checkout -b <new-branch-name>
    # Check the projects contribution guidelines or past contributions
    # for good branch names
    git push -u origin <new-branch-name>


Development Workflow
--------------------

Keeping in sync::

    # Make sure you're on the right branch
    git checkout <new-branch-name> // if needed
    # Sync any changes made on other local machines (i.e. home and work computers)
    git pull origin <new-branch-name>
    # Sync master
    git pull upstream master
    git push origin master
    # Sync new branch with master
    git merge master
    git push origin <new-branch-name>

Committing changes::

    # Make changes
    git add ...
    git commit -m ...
    git push origin <new-branch-name>
    # Make sure you push to origin!


Pull Request
------------

1. Make sure all your changes match the project's requirements for good PRs

    a. Tests pass
    b. Change documentation
    c. etc.

2. Click "Compare and pull request" on original project

3. Fill out PR name and description, then "Create pull request"

4. Take part in discussion and wait for accept/reject
