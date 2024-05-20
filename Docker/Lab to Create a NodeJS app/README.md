# Lab to Create a NodJS app

**Docker file creation breakdown** 
* Define Parent Image
  
  use the `FROM` instruction to set the parent image to the `node:10-alpine` Node.js 10 Alphine image 
* Create Directory structure

  Use `RUN` to create the `/home/node/app/node_modules` directory and set `node` as the owner/group. 
* Move Directory structure
  
  Use `WORKDIR` to set `/home/node/app as the active directory.   
* Copy files 

  use `COPY` to move the `package*.json` metadata files to the working directory. 
* Configure the NPM 

  user `RUN` to SET the `npm` registry via the `npm config set registry` command. 
* Install required pakages 

  Use `RUN` to have npm install any prerequisite packages for our application. 
* Copy more files 

  Use `COPY` to copy over the remaining files from the Dockerfile's working directory. 
* Switch users 

  Use `USER` to switch to the `node` user.
* Expose port

  Use `EXPOSE` to ensure we can access the application on the container port `8080`
* Run the application 

  Use `CMD` to run the `node` executable against the `index.js` file.


Download the [demo app](https://github.com/usganesh)
untar the file using `7zip` or `winrar` in windows or with below command in `linux` 

        tar -xf demo-app.tar

after untar the file, Ceate the docker file base on the above instruction inside the app directory. after creating the docker file start building the docker using below command. 

        docker build . -t njsappimage
        docker run -dt --name app -p 8080:8080 njsappimage
