Heroku Yesod
============

This repository contains necessary code changes to deploy a basic Yesod app to Heroku. 

### Prerequisites: >= cabal 1.20 

### Following changes have been made to code to make it work on Heroku:
* .halcyon-magic folder has been created as per [haskell-on-heroku](http://github.com/mietek/haskell-on-heroku)
   * This folder contains alex and happy dependencies for Yesod install 
* Helpers folder contains Heroku code as per [Pat Brisbin](http://pbrisbin.com/posts/parsing_database_url/) and directions from  [yesodweb/yesod](https://github.com/yesodweb/yesod/wiki/Deploying-Yesod-Apps-to-Heroku)
  * Made changes to project *cabal file* to include Heroku dependecy
  * Made changes to *Application.hs* as per directions by importing *heroku.hs* from Helpers folder and made changes to     makeFoundation function
* Brought *Procfile* to root folder and changed as per [haskell-on-heroku](http://github.com/mietek/haskell-on-heroku)
* In *config/postgresql.yml* removed production section
* Added *app.json* file as per [haskell-on-heroku](http://github.com/mietek/haskell-on-heroku)
* Added *cabal.config* file as per [haskell-on-heroku](http://github.com/mietek/haskell-on-heroku)
  * This file was created with *cabal freeze* command hence *cabal 1.20* dependency

### Deployment steps to Heroku. 
First do a test deployment to your Heroku account and then come back and do these steps manually to test the process. 

* yesod init 
* git init . 
* heroku create -b https://github.com/mietek/haskell-on-heroku -s cedar-14
* heroku addons:add heroku-postgresql:dev --app name
  * take note of the color name in the url this outputs
* heroku pg:promote HEROKU_POSTGRESQL_colorname_URL --app name
* Make the above changes to your code 
* git add . && git commit -m 'Yesod basic app'
* git checkout -b deploy
  * Make any other changes to your code and do git add . &&  git commit -m "changes"
* git push -f heroku deploy:master (i.e. first time )
* git checkout <original branch> i.e. master
* git branch -D deploy

### Test Deployment

If you have a Heroku account already, you can test the deployment first and then worry about the above changes later. 
To test the deployment, just click the link below and this example will be deployed to your Heroku account. 
Deploys to [Heroku](http://heroku.com/) in two clicks, using [_Haskell on Heroku_](http://haskellonheroku.com/).

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/mietek/herokuyesod/tree/haskell-on-heroku/)


### Acknowledgements
I would like to acknowledge Miëtek Bak for his help in deploying this app and for creating a simple process to deploy haskell apps to heroku and others who contributed to this process in various forms.
