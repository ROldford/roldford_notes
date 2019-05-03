Development Notes: Python
=========================


Global Prerequisites
--------------------

Homebrew - easy package manager for MacOS::

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

pipenv - makes canonical environment management easy::

    brew install pipenv

pyenv - allows for installation of multiple Python interpreters for tox testing::

    brew install pyenv
    pyenv install <python version>

cookiecutter - templated setup of Python projects::

    brew install cookiecutter

travis - command line app for Travis caution::

    brew install travis

Project Setup
-------------
1. Generate cookiecutter project using cookiecutter-pipenv template::

    cookiecutter gh:elgertam/cookiecutter-pipenv
    # follow prompts
    cd <project-name>

2. Create local git repo::

    git init
    git add .
    git commit -m "Initial commit"

3. Setup repo on GitHub::

    # Create repo on GitHub site without Readme, license, .gitignore
    # Copy remote repository URL
    git remote add origin <repository URL>
    git remote -v
    git push -u origin master

4. Install dev requirements::

    pipenv install --dev

5. Add ``__main__.py`` to main code folder (see example file)

6. Add repo on Travis and setup config for future PyPI deployment::

    # Sign up on Travis using GitHub login
    # Activate repo on Travis
    python3 travis_pypi_setup.py --password <PyPI password>
    pipenv lock --requirements --dev > requirements.txt
    # Edit .travis.yml to use desired Travis versions (see example file)

7. Add repo to ReadTheDocs (RTD)::

    # Sign up on RTD using GitHub login
    # Activate repo on RTD

8. Set up bumpversion config file .bumpversion.cfg (see example file)

9. Edit setup.py

    a. Set tags to match project plan (i.e. Python versions, etc)
    b. Add entry point for ``__main__.py``::

        setup(
            ...,
            entry_points = {
                'console_scripts': [
                    'cycle_calendar_generator = cycle_calendar_generator.__main__:main']},
            ...,
        )

10. Setup tox.ini for desired Python versions

    - The default tox.ini is good, but might hit more versions than you need.

11. Commit and push

Workflow
--------
Normal development should take place in the pipenv shell::

    pipenv shell

**Integration Testing**

If using ``subprocess.run()``, make sure to use the ``-m`` flag in ``*args``::

    subprocess.run(['python3', '-m', <other arguments>])

**Installing dependencies**::

    pipenv install <dependency name>
    # or for development dependencies
    pipenv install --dev <dependency name>
    # same dependency name as on PyPI
    pipenv lock --requirements --dev > requirements.txt
    # for Travis compatibility
    # Update setup.py (requirements or test_requirements) for testing compatibility if needed

**Testing**:

1. setup.py testing (current Python version)::

    python3 setup.py test

2. tox testing (multiple versions)::

    # must be outside pipenv shell
    deactivate
    tox

**New version deployment**::

    # Make sure all tests pass (especially tox!)
    # update HISTORY.rst
    git add HISTORY.rst
    git commit -m "Version update: <new version>"
    bumpversion <major|minor|patch>
    git push && git push --tags
    # Travis will test commits and deploy tagged commit to PyPI
