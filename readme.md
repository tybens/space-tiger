# SpaceTiger - A cos333 project



## Resources
- [Flask and React One Server App](https://blog.appseed.us/flask-react-full-stack-seed-projects/)


## Setup and Installation
### Installation Steps:

```bash
# clone the repo
git clone https://github.com/tybens/SpaceTiger
```

if yarn isn't installed, install it [here](https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable)
```bash
# install the NodeJS packages required for frontend
cd frontend && yarn && cd ..

# install the python packages required for backend
python3 -m venv venv # create python virtual env
source venv/bin/activate # activate it
pip install -r requirements.txt # install requirements into the virtual env
```

### Environment Variables:
The url connection to the TEST and PROD databases are stored in environment variables. To set them, on Mac run

```bash
export TEST_DB_URL=our_spacetiger_url
```

and on Windows run

```bash
setx TEST_DB_URL "...our SpaceTiger url..."
```

### Development Steps:

How to run our app as a two-server process which makes frontend development much nicer.
```bash
# run the backend
python3 app.py

# *in a separate terminal* run the frontend
cd frontend
yarn start
```

How to simulate the production environment as a one-server app. 
```bash
# ---build the frontend---
cd frontend
yarn build # build frontend

# ---run the server---
export FLASK_ENV=development # setup flask development environment variables
export FLASK_APP=app.py
flask run # run the server
```

Now whenever you save the app.py file the server will dynamically re-start because it is in debugging mode. Unfortunately because we are doing a one-server application, it is necessary to re-build the front-end to see the changes rendered.
 

## Publishing Steps:

Pushing to the main branch will automatically publish to our Render hosting. 

## Git: 

### Rebasing Tutorial
Rebase changes the base of the dev's branch from one commit to aonther, so it looks like they created their branch from the most recent commit (or whatever commit they want).

[See here for more details](https://www.simplilearn.com/what-is-git-rebase-command-article)


After you commit your changes to your feature branch `<some-feature-branch>`

checkout the main branch (or whatever branch you want to update your  merge to)
```Bash
git checkout main
```
Pull in the new stuff
```Bash
git pull origin main
```

Checkout your feature and rebase main to it

```Bash
git checkout <some-feature-branch>
git rebase main
```

Git will whine about merge conflicts, fix them and repeat these steps until git stops whining:

```Bash
git add <file-name>   # stage the merged conflicts
git rebase --continue # move to the next commit 
```

Then (`--force-with-lease`, if a PR is already made and the remote branch already exists NOT IF OTHER PEOPLE HAVE BASED work off of it i.e. they have already pulled `<some-feature-branch>` branch and merged it into their work or something) push the merged conflicts to the remote branch:

```Bash
git push --force-with-lease origin <some-feature-branch>
```

And make a PR / request merge to main using GitHub's UI