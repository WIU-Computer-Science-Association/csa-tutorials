# Sevices

## What are services?
Services are injectable classes that can be referenced from many components.  A service can be listed as a provider by either a module or a component.  When it is listed as a provider it is instantiated and this instance of the service can then be 'injected' into your components.  

## Purpose of services
Services can be used either for shared functionality (i.e. creating a service that can interface with an api) or to share data.  If two components require the same data you can store that in a service so the components have access to that shared data.  

## Defining a service
A service is essentially just a class with the `@Injectable()` annotation at the top. 
Let's look at an example service.
```Typescript
import { Injectable } from '@angular/core';

@Injectable()
export class ExampleService{
    constructor() {}
}
```
Files for services follow the naming scheme of \<cabob-cased-name\>.service.ts. For this service the file name should be `example.service.ts`. 

## Providing a service
We can list our example service as a provider from our app module.  This will make the service accessible to every component in that module.  If we listed the service as a provider in a component the service would only be accessible by that component or any nested components.  
Inside of the ngmodule or component definition we can add an array of provided services. For instance if we wanted to provide the ExampleService from our app module we could do this:
```Typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { AppRoutingModule } from './app-routing.module';
import { HeaderComponent } from './header/header.component';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { ExampleService } from './services/example.service';

@NgModule({
  declarations: [
    AppComponent,
    HeaderComponent,
    HomeComponent,
    AboutComponent,
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    AppRoutingModule
  ],
  providers: [
      ExampleService
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## Injecting services
Now we can inject our service into a component within the app module. This is done by adding a decleration of a variable with the same type as the service in our constructor. Angular will inject the instance of that service into the variable.
```Typescript
constructor(private exampleService: ExampleService) {}
```

Note: In typescript declaring an instance variable in your constructor with either private or public will add that variable to the class and make it instantiate with whatever argument is given to that part of the constructor. For example if we want to make a class to represent a point which has an x and y coordinate we can define it like this:
```Typescript
export class Point {
    constructor(public x: number, public y: number){}
}
```
That is all you need.  x and y will be instance variables of the object. You can refer to these variables as `this.x` and `this.y` within the class.

Let's make our example service more useful. We can add a private message to the service that our components can access.

```Typescript
import { Injectable } from '@angular/core';

@Injectable()
export class ExampleService{

    private message = 'Hello World';

    constructor() {}

    getMessage(): string {
        return message;
    }
}
```

Now we can inject this service into our Header and About components.

```Typescript
import { Component, OnInit } from '@angular/core';
import { ExampleService } from './example.service';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  constructor(public exampleService: ExampleService) { }

  ngOnInit() {
  }

}
```
In the html for the Header component we can display the message from the example service.

```HTML
<p>{{ exampleService.getMessage() }}</p>
```
Note: We can use {{ }} for string interpolation in our html. 
This will display the message from our example service in the home component. 

Try doing the same thing for the about component.

A more interesting use of services is to get data from an api and use that in your website. I have included a service called `kanye.service.ts`. This service uses the public https://kanye.rest api to get kanye quotes. 

## Challenges
1. Add KanyeService to the list of providers in the app module.
2. Inject the KanyeService in your home component.
3. Display the quotes from this service in the html.

Note: since the KanyeService returns Observable\<string\> we cannot simply display that in the html. I recomend doing something like this in your ngOnInit: 
```Typescript
public quote: Observable<string>;

ngOnInit() {
  this.quote = this.kanyeService.getQuote();
}
```
Don't forget to import Observable from rxjs. 

Then in the html:
```HTML
<p>{{ quote | async }}</p>
```

We use the async pipe with Observables and Subjects since they are retrieved asynchronously. For more information on observables check out [this](https://angular.io/guide/observables).

4. Find a public api and create a service that can get data from there. You will need to use the HttpClient to achieve this. Look at the KanyeService as reference and follow this [guide](https://angular.io/guide/http) to learn more about the HttpClient.