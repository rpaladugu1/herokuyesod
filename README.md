Heroku Yesod
============

This repository contains necessary changes to deploy a basic Yesod app to Heroku. 


###Prerequisites: cabal 1.20 

###Following changes have been made to code to make it work on Heroku:
* .halcyon-magic folder has been created as per [GitHub]/mietek/haskell-on-heroku
   * This folder contains alex and happy dependencies for Yesod install 
* Helpers folder contains Heroku code as per [GitHub]/yesodweb/yesod
  * Made changes to project *cabal file* to include Heroku dependecy
  * Made changes to *Application.hs* as per directions by importing *heroku.hs* from Helpers folder and making changes to     makeFoundation function
* Brought *Procfile* to root folder and changed as per [GitHub]/mietek/haskell-on-heroku
* In *config/postgresql.yml* removed production section
* Added *app.json* file as per [GitHub]/mietek/haskell-on-heroku
* Added *cabal.config* file as per [GitHub]/mietek/haskell-on-heroku
  * This file is created with *cabal freeze* command hence *cabal 1.20* dependency

### Deployment steps to Heroku. You can test it first and then do these steps to your project. 
*  yesod init 
*  git init . && git add . && git commit -m 'Yesod basic app'
*  heroku create -b https://github.com/mietek/haskell-on-heroku -s cedar-14
*  heroku addons:add heroku-postgresql:dev --app name
  * take note of the color name in the url this outputs
*  heroku pg:promote HEROKU_POSTGRESQL_colorname_URL --app name
* Make the above changes to your code 
*  git checkout -b deploy
  * Make any other changes to your code 
*  git commit -m "changes"
*  git push -f heroku deploy:master
*  git checkout <original branch> i.e. master
*  git branch -D deploy

###Test Deployment
----------
If you have a Heroku account already, you can test the deployment first then worry about the above changes later. 
To test the deployment, just click the link below and this example will be deployed in your Heroku account. 
Deploys to [Heroku](http://heroku.com/) in two clicks, using [_Haskell on Heroku_](http://haskellonheroku.com/).

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/mietek/herokuyesod/tree/haskell-on-heroku/)
