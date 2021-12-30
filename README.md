# Getting Started
This is simple demo to show CI/CD working process at the GitHub and also how to deploy application to local host via "Git Actions"
Most of demo seems to co-work with cloud service like AWS,DigitalOcean, etc....
This is for simple host user 

   "local host" -------------------->  Githug  --------------------> "remote host"
  "app coding host"                "action on event"                  "app working host"
      "git push"                     "build/deploy"                       app is running
      
    reference source : https://www.youtube.com/watch?v=6-RtA6FlbgQ  
## Requirements
   - Hosts
      1. "local host" - for app dev/coding job
      2. "remote host" - for app running ("loca lhost" can be "remote host")

# Work Steps
  - Make repository at the GitHub named nodejs-cicd-to-localhost
  - Clone repo to "local host"
  - Open it with VScode
  - Write node js with react

## Write node js with react  ( edirot VScode)
  - vi app.js
  - npm init -y   // create package.json file
  - nmp i express  // install express
  - npx create-react-app frontend  // create front end  
  - cd frontend
  - rm -fr .git   // remove default git which is automaticly made
  - // npm start     // start frontent
  - cd ..
  - git init
  - cd frontend
  - npm i axios            // install axios
  - vi App.js              // ./frontend/src/App.js file
  - vi package.json        // ./frontend/package.json file   add proxy "proxy": "http://localhost:5000
  - vi package.json        // ./package.json file   add script "start": "node app.js"
  - // open another terminal
  - npm start              // ./frontend/    // run frontend
  - npm start              // ./             // run backend  
  - // check web and all works 
  - // stop app at the terminal with ctrl+c
  - cd ~/project/nodejs-cicd-to-localhost  // main forlder
  - vi .gitignore              // add "node_modules"


  

      
