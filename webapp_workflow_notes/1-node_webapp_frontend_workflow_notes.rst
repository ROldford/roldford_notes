nDevelopment Notes: Simple React Webapp (Front End, GitHub Pages)
================================================================


Global Prerequisites
--------------------

Homebrew - easy package manager for MacOS::

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

NodeJS - Use JS to make webapp, not embedded scripts::

    brew install node
    # Also installs npm (Node package manager)

Create-React-App - Setup new React project::

    npm install -g create-react-app

.. Add npm-check-updates section

Project Setup
-------------

1. Generate project using create-react-app::

    create-react-app <app-name>
    cd <app-name>
    npm start  # starts and opens development server

2. Setup repo on GitHub::

    # Create repo on GitHub site without Readme, license, .gitignore
    # Copy remote repository URL
    git remote add origin <repository-url>
    git remote -v
    git push -u origin master

3. Use npm to install packages::

    # gh-pages for manual deployment
    # enzyme, sinon, and helper packages for testing
    # bootstrap for easy styling
    # reactstrap to use bootstrap styles in react
    npm install gh-pages --save-dev
    npm install enzyme enzyme-adapter-react-16 enzyme-to-sinon sinon --save-dev
    npm install bootstrap --save
    npm install --save reactstrap react react-dom

4. Update package.json for gh-pages::

    {
      ...,
      "homepage": "https://[your-user-name].github.io/[your-repo-name]/",
      ...,
      "scripts": {
        ...,
        "predeploy": "npm run build",
        "deploy": "gh-pages -d build",
        ...
      },
      ...
    }

5. Update src/index.js for reactstrap by replacing existing css import::

    import 'bootstrap/dist/css/bootstrap.min.css';

6. Setup testing in src/setupTests.js (see example file)

7. Delete unneeded files:

    * index.css
    * logo.svg

8. Empty all content in App.css

    * Don't delete it though! Other parts of the system assume it exists.

9. Add repo on Travis and setup config for future PyPI deployment

    i. Sign up on Travis using GitHub login

    ii. Activate repo on Travis (not needed anymore?)

    iii. Generate a personal access token on GitHub (*public_repo* or *repo* scope)

    iv. In Travis, add the personal access token in repo settings with name *GITHUB_TOKEN*

    v. Edit .travis.yml to use desired Travis versions (see example file)

    vi. Push to update Travis and make first deployment

Workflow
--------

**Manual Deployment**

    npm can handle deployment when package.json is set up as shown above::

        npm run deploy

.. Add package updating workflow
.. https://flaviocopes.com/update-npm-dependencies/

**React Component Development**

    Under construction

**Jest Testing**

    Under construction
