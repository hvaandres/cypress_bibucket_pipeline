**Cypress | Bitbucket Pipeline Configuration | --clone**

This project is based on Cypress & [docker containers](https://hub.docker.com/r/cypress/base/) where you can choose different [configurations](https://github.com/cypress-io/cypress-docker-images). Also, the master branch is the one that will run the Bitbucket Pipeline.

*I recommend you to take a look at this other [project](https://github.com/hvaandres/Cypress_Testing_Reports) if you want to know how to do it with Github Actions*

---

## Developer Tools

1. [Bitbucket Pipeline](https://support.atlassian.com/bitbucket-cloud/docs/get-started-with-bitbucket-pipelines/)
2. [Cypress.io](https://www.cypress.io/)
3. [Docker](https://www.docker.com/)

---

## Start a new project 

You will have to make sure that you follow the next steps, if you want to get this project done on your own:

1. Create a directory in your local machine
2. Create a Bitbucket Repository
3. Clone the repository inside of your Repo
4. CD inside of your directory
5. Create a Node.js project
6. Install cypress
7. Run cypress
8. Go back to Bitbucket > Open your repo > Go to Pipelines > Setting up your project with Node.js
9. Add your node.js commands to run the pipeline
10. Commit the new file & check the pipeline to see if this set-up is working for you
11. Go back to your project and open your project in visual studio and pull the new changes

```
mkdir [project_name]
cd [project_name]
npm init -y
npm install cypress --save-dev

npx cypress open or ./node_modules/.bin/cypress open

control + c [stop_running_cypress]

```

## Bitbucket YAML file

```
#  Template NodeJS build

#  This template allows you to validate your NodeJS code.
#  The workflow allows running tests and code linting on the default branch.

image: node:10.15.3
options:
  max-time: 15
pipelines:
  default:
  - step:
      name: Pipeline Cypress E2E
      caches:
        - npm
        - cypress
      image: cypress/base:10
      script:
        - npm ci
        - npx cypress run
      artifacts:
        - cypress/reports/**
        - cypress/videos/**

definitions:
  caches:
    npm: $HOME/.npm
    cypress: $HOME/.cache/Cypress

```

## Cloning your Bitbucket repo to Github

You will have to do the following steps:

```
git clone --mirror [Bitbucket_Repo_URL]
# Make a bare mirrored clone of the repository

cd repository-to-mirror.git
git remote set-url --push origin [Github_Repo_URL]
# Set the push location to your mirror

git push --mirror

```

## Bitbucket Pipeline Example

![Bitbucket Example](https://github.com/hvaandres/cypress_bibucket_pipeline/blob/Dev/Screen%20Shot%202021-01-23%20at%2011.20.12%20PM.png)

