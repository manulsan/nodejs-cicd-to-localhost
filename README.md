# Getting Started
This is simple demo to show CI/CD working process at the GitHub and also how to deploy application to local host via "Git Actions"
Most of demo seems to co-work with cloud service like AWS,DigitalOcean, etc....
This is for simple host user 

   "local host" -------------------->  Github  --------------------> "remote host"

  "app coding host"                "action on event"                  "app working host"
  
      "git push"                     "build/deploy"                       app is running
      
  reference source : https://www.youtube.com/watch?v=6-RtA6FlbgQ  
  main differences between "source" and "my stuffs" is deployment
  "source" deploy app to digitalocean and "my stuffs" deploy to "my computer-linux(ubutu 20.04)
## Requirements
   - Hosts
      1. "local host" - for app dev/coding job
      2. "remote host" - for app running ("loca lhost" can be "remote host")
      3. Backend nodejs applicaton, refers https://www.w3schools.com/nodejs/nodejs_mongodb.asp
      4. Frontend react application, refers https://www.w3schools.com/react/default.asp
      5. GitHub Actions and Runners, refers https://docs.github.com/en/actions

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
  - git add .
  - git commit -m "Application is ready"
  - git push origin main

## Setup "remote host" working environment
  ### OS : ubuntu 20.04
  ### Setup new user for  Runners job
  - sudo passwd            // setting up default root user
  - su -
  - adduser alexyoon  
  - sudo usermod -aG sudo alexyoon
  - su - alexyoon
  - cd /var/www
  - mkdir actions_runner
  ### Setup nginx on ubuntu
  - // reference  => https://www.nginx.com/resources/wiki/start/topics/tutorials/install/  
  - sudo apt-get update  //Update Software Repositories
  - sudo apt-get install nginx  // install nginx from ubuntu repositories
  - nginx -v           // verify the installation
  - sudo systemctl status nginx
  - sudo systemctl restart nginx
  - sudo ufw app list           // display available nginx profiles
  - sudo ufw allow 'nginx http' // if  there is no list, execute left command
  - sudo ufw reload 
  - sudo ufw allow 'nginx https' // for encrypted(https) traffics
  - sudo ufw allow 'nginx full'  // for both
  - curl http://127.0.0.1        // for nginx test .   or curl -i 127.0.0.1 
  
  ### Setup nodejs on ubuntu
  - sudo apt update
  - sudo apt install nodejs
  - nodejs -v
  - sudo apt install npm   // install node.js package manager

## Configure  "GitHub Actions"
  ### At git repo
  - goto https://github.com/manulsan/nodejs-cicd-to-localhost/actions/new
  - click "Settings" 
  - click "Actions"=>"Runners" // refers https://docs.github.com/en/actions/hosting-your-own-runners
  - click button named "New self-hosted runner"
  - select os "linux" adn follow-up the commands at the webpage at the "remote host linux"

  - Making actions
    - click Actions => Make new Actions
    - refer the .github/workflows/node.js.yml  

## Configure "remote host"   logined by alexyoon  
  - cd /var/www/
  - make cations-runners
  - "At /var/www/actions-runner"
  - sudo ./svc.sh install  
  - sudo ./svc.sh start
  - "check runner status at repo "Settings" => "Runners" , check "Idle" status then ok"
  - "change nginx config file"
     - localtion:/etc/nginx/site-available/default
     - refers repo/nginx_config/*
  - sudo service nginx restart   // check nginx is well congigured and working well.
  - sudo visudo -f /etc/sudoers.d/alexyoon
     alexyoon ALL=(ALL) NOPASSWD: /usr/sbin/service nginx start, /usr/sbin/service nginx stop,/use/sbin/service nginx restart
       
  - "----- for application manager -----"
     - cd /var/www/_actions_runner/_work/nodejs-cicd-to-locahost/nodejs-cicd-to-locahost
     - sudo npm install pm2@latest -g
     - pm status
     - pm2 start npm --name "mywebsite" -- run start   // start package.json
     - pm2 save


