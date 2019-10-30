# 01 Creating A Project
This tutorial will you through how to create a new angular project.

## Requirements
* npm 
* angular cli
  * Install with npm using the command `npm install -g @angular/cli`

## Ng
ng is the angular cli. From your terminal of choice try running ng to verify that you have successfully installed angular. Run `ng help` to see a list of available commands.

## New Project
To create a new project use the cli. `ng new <project name>` will create a new project. Select y if the cli prompts `? Would you like to add Angular routing? (y/N)`.  This isn't necessary, but later lessons will be using routing so it is easiest to let the cli initialize it for you now.  We will cover how to manually setup the angular router module in the next lesson. At this prompt `? Which stylesheet format would you like to use? (Use arrow keys)` select css. After that the project will start building.  This will create a directory named after the project and install all of the node dependencies.  

The directory structure of your project should look like this:
<pre>
.
├── angular.json
├── browserslist
├── e2e
│   ├── protractor.conf.js
│   ├── src
│   │   ├── app.e2e-spec.ts
│   │   └── app.po.ts
│   └── tsconfig.json
├── karma.conf.js
├── node_modules
│   ...
├── package.json
├── package-lock.json
├── README.md
├── src
│   ├── app
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   ├── app.module.ts
│   │   └── app-routing.module.ts
│   ├── assets
│   ├── environments
│   │   ├── environment.prod.ts
│   │   └── environment.ts
│   ├── favicon.ico
│   ├── index.html
│   ├── main.ts
│   ├── polyfills.ts
│   ├── styles.css
│   └── test.ts
├── tsconfig.app.json
├── tsconfig.json
├── tsconfig.spec.json
└── tslint.json
</pre>
Later lessons will explain the files and directories in the project as they become relevant.  