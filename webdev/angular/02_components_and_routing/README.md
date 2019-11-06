# 02 Components And Routing

## Creating A Header Component
We can use the angular cli to generate a new component.  Run the command `ng generate component header --module app`.  This will create a new directory called `header` inside of this directory is a typescript file, html file, css file, and spec file.  These files make up the logic, view template, styling, and tests for our header component respectively.  For now lets look at the `header.component.html` file.

Look in the resources directory for the `header/header.component.html` file.  Copy the contents of this into your `header.component.html` file.  This will create an unordered list of links in the header component.  These links will direct you to different parts of the site when we set up routing.

Now modify the `app.component.html` file so that the only line is `<app-header></app-header>`.  This will make our header component appear at the top of the page.  Try running your project with `ng serve` and seeing what it looks like.  Your site will be available at `http://localhost:4200`.  You should see a bulleted list containing our two links.  You can style this by following [this](https://www.w3schools.com/Css/css_navbar.asp) tutorial on styling.  If you are not interested in the styling I have provided a css file at `resources/header/header.component.css`.

## Setting Up The Router Module
We will create a seperate module file for storing our routes.  You can generate this by running the command `ng generate module app-routing-module --module app --flat` this will generate a new module for you named app-routing.module.ts.  

Inside of that module add this import `import { RouterModule, Routes } from '@angular/router';`.  We need this to initialize the RouterModule for the project.  

Create a constant array of type Routes.  This is where we will store our routes.  You can declare it like this: `const routes: Route = [];`.

Our module needs to import and export the RouterModule to make it available to the project.  Inside the @ngModule annotation add this to the imports array `RouterModule.forRoot(routes)` and add `RouterModule` to the exports array.

You can find a template of this setup in the resources directory named `app-routing.module.ts`.  If you copy this file into your project don't forget to add `AppRoutingModule` to the imports array of your `app.module.ts` file.

## Adding A Route
In angular, Routes are a path that lead to a component in your project.  For instance we can have the path `home` lead to a home component.  Whenever someone goes to, for example, `http://localhost:4200/home` the home component will be loaded into the site and displayed wherever the `<router-outlet></router-outlet>` tag is.  

First, we should add a router outlet to the `app.component.html` file.  Add `<router-outlet></router-outlet>` below the `<app-header></app-header>` tag.

Next, we need to create a route that directs to a home component.  Generate your home component using the angular cli: `ng generate component home --module app`.  Then go to the `app-routing.module.ts` file and add a Route to your routes list: `{ path: 'home', component: HomeComponent }`.  The path of this route is `/home` and the component it uses is `HomeComponent`. 

Try running the project now and click the home link.

## Challenges 

1. Create an about component, add a route to that component, and create a link to it on the header.
2. Make the empty path redirect to the home component. Look through the angular routing tutorial for how to do this.
3. Create a page not found component and make all invalid paths go to that component.
4. Add a footer component with links to your github or other social media.  Use icons for the links. (You can add icons to your assets directory and reference them from there i.e `<img src="/assets/icons/octocat.svg">`) This component should appear at the bottom of every page like the header. There are a lot of good icons [here](https://unpkg.com/browse/simple-icons@1.19.1/icons/)
