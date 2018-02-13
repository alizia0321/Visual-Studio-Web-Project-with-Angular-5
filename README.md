# Visual-Studio-Web-Project-with-Angular-5
Using an Empty template and no check box for adding folders, files or references for MVC, Web API, etc.
How To:
<pre>
Step 1 
  * Create an empty template ASP.NET Web Application

Step 2
  * Create an Angular project from Angular CLI (If doing a merge with VS in next step make sure that this 
    project folder is the same folder as where the project file is in the project above)
    ^ Step A - Development Environment
        -- Verified that I was running:
            * at least node 6.9.x and 
            * npm 3.x.x 
        -- by running
            * node -v
                  v6.11.2
            * npm -v
                  5.6.0
        -- I then checked to see if Angular CLI was installed
            * ng -- version
                  1.6.7
        -- If applicable install 
            * node and npm with one download from https://nodejs.org/en/download/
            * Angular CLI by running the following command: 
                  ^ npm install -g @angular/cli
        -- If applicable upgrade Angular CLI
            * Global package:
                  ^ npm uninstall -g @angular/cli
                  ^ npm cache clean' or if on npm version > 5 then 'npm cache verify
                  ^ npm install -g @angular/cli@latest
        -- If applicable upgrade NPM
            * npm install npm@latest -g 
    ^ Step B - Create a new project
        -- If merging with Visual Studio, navigate to the solution file folder that was created in Step 1
           otherwise, pick any folder.
        -- ng new <project name> --skip-git (no need for git since will apply source control from Visual Studio)
            * Parameters
                  ^ Project name should be the exact same name as the project
                  ^ Skip git since will add to GitHub through Visual Studio
            * This installs packages but it came back with errors such as needing Admin privileges to run 
              the scandir on folders that did not even exist. 
              Therefore, had to run the following command 1st:
                  ^ npm cache verify
                          -- Found this on github at: https://github.com/npm/npm/issues/17747. 
                            Per this site could probably have also run:  
                                npm cache clean –force 
                            but the force switch is only needed for the previous versions of NPM 
                            (less than version 5)
        -- ng new <project name> --skip-git (run this again if had errors as described above from cache
            * This creates an Angular project that is completely standalone. 
              If that is all you needed you could stop here and just develop here. 
              But since we want to develop from Visual Studio instead continue with the following steps.

    ^ Step C – “Serve” the application (To verify the application installed without any issues)
        -- Go to the project directory and launch the server.
            * cd my-app
            * ng serve --open	(Using the --open (or just -o) option will automatically open your browser 
              on http://localhost:4200/.)
                  ^ The ng serve command launches the server, watches your files, and rebuilds the app as 
                    you make changes to those files.
                  ^ The app greets you with a message:
                  
    ^ Step Optional – Editing Files
        -- There is no need to edit any files, all files are ready to copy over to a VS project
        -- If want to however, the following is an example of how that works
            * Edit the root Angular component by editing the src/app/app.component.ts and 
              src/app/app.component.css files which was created by the CLI.
                  ^ The CLI creates the first Angular component for you. This is the root component and it 
                    is named app-root.
                  ^ Open the component ts file and change the title property from 'app' to 'My First Angular 
                    App':
                          -- When saving you can see the compiler compiling from the command window, when 
                          finished the command window prompt says Webpack: Compiled Successfully and the web 
                          page refreshes on its own.
                  ^ Open the component css file to add style
                          -- Open the css file and add css to the header 
                                  h1 {
                                    color: #369;
                                    font-family: Arial, Helvetica, sans-serif;
                                    font-size: 250%;
                                  }

Step 3
Merging
  * After creating the CLI project in the same folder as where the Visual Studio’s .proj file is (by 
    ^ right clicking on solution name (not project name), 
    ^ selecting “Open Folder in File Explorer” from context menu, 
    ^ shift+right clicking in open space, 
    ^ clicking on “open command window here” from the context menu, 
    ^ typing the following: ng new <project name>  --skip-git
        -- <project name> should be the exact same name as the project
        -- skip git since will add to GitHub through Visual Studio
  go into Visual Studio to include the files from the CLI project into the VS project

  * Click on the Show All Files button
  * Include all angular-cli generated outputs into the project 
    ^ The following should have already been in the VS project for an ASP.NET Web Application, so do not 
      need to be re-included. 
        -- Connected Services
        -- Properties
        -- References
        -- Bin
        -- Obj
        -- Packages.config
        -- Web.config
    ^ Therefore, include all the other files and folders generated by the CLI.  BUT
    ^ DO NOT Include folder "node_modules" 
  * Configure visual studio project to build angular app with CLI
    ^ Right click on the MVC project and properties and go to Build Events and enter the following command 
      in the “Pre-build event command line:” box (of course the echos are optional):
      
        echo "Using ng build on $(ProjectName)" &&^
        ng build  

    ^ Run Build Solution to verify the build process works
        -- The output window should show the output from the ng build showing the webpack js bundle files
        -- Bundle files are created by the ng build process and by default are created in the dist folder (as 
             configured in the .angular-cli.json file (located at the root of the application).
    ^ o	Configure the index file as the start up and edit it to look in the dist folder for the webpack bundle files
        -- Right click on the index file and click on Set As Start Page
        -- Copy the includes from the dist/index.html file and then add a “/dist/" prior to the name of each file.
           Eg.
              From: <script type="text/javascript" src="inline.bundle.js"></script>
              To:   <script type="text/javascript" src="/dist/inline.bundle.js"></script>
    ^ Launch the Browser from Visual Studio to verify the Angular Application displays


</pre>
