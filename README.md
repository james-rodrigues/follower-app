# DeployDemo

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 1.2.4.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `-prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).
Before running the tests make sure you are serving the app via `ng serve`.

## Summary of Lesson Learnt
1. Available Optimization Techniques
    * Minification - Removes comments and whitespace ( Cn be done using various tools)
    * Uglification - Rename components to have smaller names (Can be done using various tools)
    * Bundling - Bundle various files into one bundle for faster access
    * Dead code elimination - Remove redundant code from the codebase
    * Ahead of Time (AOT) Compilation - Can be done using Angular CLI (`ng build --prod`)
2. JIT vs AOT Compilation
    * Angular compilation converts javascript files into javascript files
    * `*.component.html` also have been converted in JS files for DOM creation
    * This is known as JIT compilation.
        * Drawbacks of JIT compilation
            * Inefficient for Production
            * Happens for every user
            * More components, slower
            * Angular compiler needs to be shipped along with the bundle( increases bundle size )
            * Template error are caught during runtime
    * AOT Compilation deals precompiled JS scripts which dont need to be compiled again and again
        * Benefits of AOT compilation
            * Faster Startup
            * Smaller bundle size
            * Template errors are cuaght during compile time
            * Better Security ( prevents HTML injection attacks )
3. Angular compiler can used to compile your .ts into .js using the command `node_modules/.bin/ngc`. You can get template exeception at this compilation step only.
4. `ng build` command helps to build the angular application without any optimization techniques applied. `dist` folder is created which contains all deployables files.
5. `ng build --prod` command helps to build the angular application with all optimization techniques mentioned above.
    Code Size is smaller compared to the build command. `dist` folder is created with all deployables with names containing hashcode as per the content of the file.
6. `environments` folder can be used to provide environment specific properties in your components. To run the app with environment specific properties use `ng serve --env=<envName>` and to build use `ng build --env=<envName>`. Note : carefully check the import statement for the environment variable in the .ts file. check `navbar.component.ts` and `environments\environment.ts`. 
7. Custom environment can be created by creating a new environment file in `environments` folder. check `environment.test.ts`. All properties in all environment should be the same. The new environment file needs to be registered in `.angular-cli.json`. The build and run commands remain the same.
8. When environment variables have been changed, they are not replaced by hot module replacement of Angular app. You need to restart the server again
9. `tslint` is npm package that is used by angular to good readable codes. Rules are configured in `tslint.json`. You may choose to enable and diable the rules in this json file.
    * to list the lint errors : `ng lint`
    * to fix the common lint errors : `ng lint --fix`
    Use `TSLint` plugin to avoid linting issues. (Ctrl + Shift + P - to auto fix all lint issues in a file)

## Deployment Steps for various options
1. Github Pages
    * Create a repository on github for your app
    * git remote add origin https://github.com/james-rodrigues/follower-app.git - to add the existing folder of your project to the github repository
    * git push -u origin master - to push the contents of the projects to github repository
    * npm i -g angular-cli-ghpages - NPM package for github pages deployment install globally
    * ng build --prod --base-href="https://james-rodrigues.github.io/follower-app/" - T build the app and set the base url of the app. url formation : `https://<username>.github.io/<app-name>/`
    PostFix `/` is important
    * ngh - to instruct the github cli to deploy the app to the required
    * Alternatively, you can add a script in package.json. check `package.json`. Command : `npm run deploy:gh`

2. Firebase
    * Login in console.firebase.google.com using your gmail credentials
    * Create a project with the app-name or your repository
    * npm i -g firebase-tools - NPM package for firebase deployment
    * firebase login - to login with google credentials for firebase
    * firebase init - to initialize the repository with firebase files . Currently only select the option as Hosting rest all will be default
    * Edit the `firebase.json` file. check `firebase.json`
    * ng build --prod - to build the app
    * firebase deploy - to deploy app on firebase
    * Alternatively, you can add a script in package.json. check `package.json`. Command : `npm run deploy:gh`
    * Note:  check the rewrites property in firebase.json to avoid redirection issues.

3. Heroku 
    * Install Heroku CLI on your machine
    * Create a Heroku account or Login using existing credentails
    * Verify heroku version on your machine `heroku --version`
    * `heroku login` - login with your credentials
    * `heroku create` - to create a app name for your project
    * `heroku open` - to open the app created in browser
    * Install `express` npm package to run 
    * Move `@angular/cli`, `@angular-compiler/cli` and `typescript` dependencies from devDependencies to dependencies



## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
