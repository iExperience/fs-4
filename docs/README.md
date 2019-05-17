# iXperience Full Stack 2019 - Day 4

[[toc]]

## Angular

### Installation

Enter in command terminal (make sure you have the lastest version of node or >v8)
```bash
npm install -g @angular/cli
```

## Angular CLI

### Version

First check the version of Angular you have just installed
```bash
ng --version
```

### Creating project

Enter in command terminal
```bash
ng new name-of-your-app
```

### Run app

Run locally(localhost:4200)
```bash
ng serve
```

Open browser when running the dev server 
```bash
ng serve --open
```
Check out docs for all angular CLI commands
```html
<a href="https://angular.io/cli"></a>
```

## Open in VSCode

### Open in VSCode

Cd into the project and open in Visual Studio Code
```bash
cd name-of-your-project
code .
```

## Project Anatomy

### Package.json

Anatomy of package.json
```json
{
  "name": "demo-air-bnb",
  "version": "0.0.0",
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
  "private": true,
  "dependencies": {
    "@angular/animations": "~7.2.0",
    "@angular/common": "~7.2.0",
    "@angular/compiler": "~7.2.0",
    "@angular/core": "~7.2.0",
    "@angular/forms": "~7.2.0",
    "@angular/platform-browser": "~7.2.0",
    "@angular/platform-browser-dynamic": "~7.2.0",
    "@angular/router": "~7.2.0",
    "core-js": "^2.5.4",
    "rxjs": "~6.3.3",
    "tslib": "^1.9.0",
    "zone.js": "~0.8.26"
  },
  "devDependencies": {
    "@angular-devkit/build-angular": "~0.13.0",
    "@angular/cli": "~7.3.8",
    "@angular/compiler-cli": "~7.2.0",
    "@angular/language-service": "~7.2.0",
    "@types/node": "~8.9.4",
    "@types/jasmine": "~2.8.8",
    "@types/jasminewd2": "~2.0.3",
    "codelyzer": "~4.5.0",
    "jasmine-core": "~2.99.1",
    "jasmine-spec-reporter": "~4.2.1",
    "karma": "~4.0.0",
    "karma-chrome-launcher": "~2.2.0",
    "karma-coverage-istanbul-reporter": "~2.0.1",
    "karma-jasmine": "~1.1.2",
    "karma-jasmine-html-reporter": "^0.2.2",
    "protractor": "~5.4.0",
    "ts-node": "~7.0.0",
    "tslint": "~5.11.0",
    "typescript": "~3.2.2"
  }
}

```

### Index.html

Anatomy of index.html - SPA: app-root component embeded into html body tag
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>DemoAirBnb</title>
  <base href="/">

  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root></app-root>
</body>
</html>

```

### app.module.ts

Main enrty point of the app - All components, services and modules must be declaired here
```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### app.component

Main app component: 
app.component.ts
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  name = 'Byron';
}
```

app.component.html
```html
<div>
  <h1>Hello {{name}}</h1>
</div>
```

## Bootstrap

### Installing Bootstrap

cd to project root directory
```bash
npm install bootstrap jquery --save
```

add bootstrap to angular.json
```json
"styles": [
    "src/styles.scss",
    "node_modules/bootstrap/dist/css/bootstrap.min.css"
],
```

## Generating Angular Components

### Generate dash-board component

^c to stop serve
```bash
ng generate component components/dash-board
```

### Component Anatomy

dash-board.component.ts
```ts
import { Component, OnInit } from '@angular/core';

@Component({
 selector: 'app-dash-board',
  templateUrl: './dash-board.component.html',
  styleUrls: ['./dash-board.component.css']
})
export class DashBoardComponent implements OnInit {

  constructor(
    //Import services here
  ) { }

  ngOnInit() {
  }

}
```

dash-board.component.html
```html
<p>
  dash-board works!
</p>
```

dash-board.component.css - Empty on generation
```css

```

### Displaying dash-board as main container
Embed dash-board selector in app.component.html
```html
<div>
  <app-dash-board></app-dash-board>
</div>
```

### User Component

users.component.ts
```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-users',
  templateUrl: './users.component.html',
  styleUrls: ['./users.component.css']
})
export class UsersComponent implements OnInit {

  users: Array<any>;

  constructor(
    private userService: UserService
  ) {
    this.users = [
      {
        name: 'Byron',
        lastName: 'de Villiers',
        email: 'byron@mail.com',
        cellPhone: 828073593
      },
      {
        name: 'John',
        lastName: 'Doe',
        email: 'john@mail.com',
        cellPhone: 746541230
      },
      {
        name: 'Jeff',
        lastName: 'Briggs',
        email: 'jess@mail.com',
        cellPhone: 471234567
      }
    ];
  }

  ngOnInit() {
  }

}
```

users.component.html
```html
<h3>Users</h3>
<div class="table-responsive">
  <table class="table table-striped table-sm">
    <thead>
      <tr>
        <th>Name</th>
        <th>Last Name</th>
        <th>Email</th>
        <th>Cell Phone</th>
      </tr>
    </thead>
    <tbody>
      <tr class="table-row" *ngFor="let user of users">
        <td>{{user.name}}</td>
        <td>{{user.lastName}}</td>
        <td>{{user.email}}</td>
        <td>+27 0{{user.cellPhone}}</td>
      </tr>
    </tbody>
  </table>
</div>
```
users.component.css
```css
.table-row{
    cursor: pointer;
}

.table-row:hover{
    background-color: rgba(0, 123, 255, 0.5);

}
```

### Service Provider Component

service-provider.component.ts
```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-service-providers',
  templateUrl: './service-providers.component.html',
  styleUrls: ['./service-providers.component.css']
})
export class ServiceProvidersComponent implements OnInit {

  serviceProviders: Array<any>;

  constructor( ) {
    this.serviceProviders = [
      {
        name: 'Joe',
        lastName: 'Soap',
        email: 'joe@mail.com',
        cellPhone: 828073593,
        numberOfListings: 5
      },
      {
        name: 'John',
        lastName: 'Doe',
        email: 'john@mail.com',
        cellPhone: 828073545,
        numberOfListings: 15
      }
    ];
  }

  ngOnInit() {
  }

}
```

service-provider.component.html
```html
<h3>Service Provider</h3>
<div class="table-responsive">
  <table class="table table-striped table-sm">
    <thead>
      <tr>
        <th>Name</th>
        <th>Last Name</th>
        <th>Email</th>
        <th>Cell Phone</th>
      </tr>
    </thead>
    <tbody>
      <tr class="table-row" *ngFor="let sp of serviceProviders">
        <td>{{sp.name.toUpperCase()}}</td>
        <td>{{sp.lastName}}</td>
        <td>{{sp.email}}</td>
        <td>+27 0{{sp.cellPhone}}</td>
        <td>{{sp.numberOfListings}}</td>
      </tr>
    </tbody>
  </table>
</div>
```
service-provider.component.css
```css
.table-row{
    cursor: pointer;
}

.table-row:hover{
    background-color: rgba(0, 123, 255, 0.5);

}
```

## Generating Object Models

### Generate User Model

terminal
```bash
ng generate model models/user
```

### Define User Model

models/user.ts
```ts
export class User {
    name: string;
    lastName: string;
    email: string;
    cellPhone: number;
}
```


### Generate Service Provider Model

terminal
```bash
ng generate model models/service-provider
```

### Define Service PRovider Model

models/service-provider.ts
```ts
export class ServiceProvider {
    name: string;
    lastName: string;
    email: string;
    cellPhone: number;
    numberOfListings: number;
}
```

## Generating Angular Services

### Generate User Service

terminal
```bash
ng generate service services/user
```

### Define User Service

service//user/user.service.ts
```ts
import { Injectable } from '@angular/core';
import { User } from '../../models/user';

@Injectable({
  providedIn: 'root'
})
export class UserService {

  users: Array<User>;

  constructor() {
    this.users = [
      {
        name: 'Byron',
        lastName: 'de Villiers',
        email: 'byron@mail.com',
        cellPhone: 828073593
      }
    ];
  }

  getUsers(): Array<User> {
    return this.users;
  }
}
```
### Generate Service Provider Service

terminal
```bash
ng generate service services/service-provider
```

### Define Service Provider Service

service/service-provider/service-provider.service.ts
```ts
import { Injectable } from '@angular/core';
import { ServiceProvider } from '../../models/service-provider';

@Injectable({
  providedIn: 'root'
})
export class ServiceProviderService {

  serviceProviders: Array<ServiceProvider>;

  constructor() {

    this.serviceProviders = [
      {
        name: 'Joe',
        lastName: 'Soap',
        email: 'joe@mail.com',
        cellPhone: 828073593,
        numberOfListings: 5
      },
      {
        name: 'John',
        lastName: 'Doe',
        email: 'john@mail.com',
        cellPhone: 828073545,
        numberOfListings: 15
      }
    ];

  }

  getServiceProviders(): Array<ServiceProvider> {
    return this.serviceProviders;
  }

}
```

## Linking Angular Components and Serviceses

### Connect User Component and Service

components/user.component.ts
```ts
import { Component, OnInit } from '@angular/core';
import { User } from '../../models/user';
import { UserService } from '../../services/user/user.service';

@Component({
  selector: 'app-users',
  templateUrl: './users.component.html',
  styleUrls: ['./users.component.css']
})
export class UsersComponent implements OnInit {

  users: Array<User>;

  constructor(
    private userService: UserService
  ) {
    this.users = this.userService.getUsers();
  }

  ngOnInit() {
  }

}
```

### Connect Service Provider Component and Service

components/service-provider.component.ts
```ts
import { Component, OnInit } from '@angular/core';
import { ServiceProvider } from '../../models/service-provider';
import { ServiceProviderService } from '../../services/service-provider/service-provider.service'


@Component({
  selector: 'app-service-providers',
  templateUrl: './service-providers.component.html',
  styleUrls: ['./service-providers.component.css']
})
export class ServiceProvidersComponent implements OnInit {

  serviceProviders: Array<ServiceProvider>;

  constructor(
    private spService: ServiceProviderService
  ) {

    this.serviceProviders = this.spService.getServiceProviders();

  }

  ngOnInit() {
  }

}
```

## Angular Routing Module

### Using the built-in routing module
app-routing-module.ts
```ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { HomeComponent } from './components/home/home.component';
import { UsersComponent } from './components/users/users.component';
import { ServiceProvidersComponent } from './components/service-providers/service-providers.component';

const routes: Routes = [
  { path: 'home', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'service-providers', component: ServiceProvidersComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### Embedding Routing Module Selector Into Dash-Board Component 
dash-board.component.ts
```ts
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-dash-board',
  templateUrl: './dash-board.component.html',
  styleUrls: ['./dash-board.component.css']
})
export class DashBoardComponent implements OnInit {

  navItems: Array<any> = [
    {
      name: 'Home',
      rout: '/home'
    },
    {
      name: 'Users',
      rout: '/users'
    },
    {
      name: 'Service Providers',
      rout: '/service-providers'
    }
  ]

  constructor(
    private router: Router
  ) { }

  ngOnInit() {
    this.router.navigate(['/users']);
  }

  navTo(page) {
    this.router.navigate([page.rout]);
  }

}
```

dash-board.component.html
```html
<div>

  <div>
      <ul>
        <li *ngFor="let navItem of navItems" >
          <button type="button" class="btn btn-primary" 
          (click)="navTo(navItem)">{{navItem.name}}</button>
        </li>
      </ul>
    </div>

  <router-outlet></router-outlet>

</div>
```

## Using Bootstrap UI in Dash-Board Component 

###  Bootstrap styled Dash-Board Component 

dash-board.component.html
```html
<div>

  <nav class="navbar navbar-dark fixed-top bg-dark flex-md-nowrap p-0 shadow">
    <a class="navbar-brand col-sm-4 col-md-3 mr-0" href="#">FS BnB Admin Panel</a>
    <input class="form-control form-control-dark w-100" type="text" placeholder="Search" aria-label="Search">
    <ul class="navbar-nav px-3">
      <li class="nav-item text-nowrap">
        <a class="nav-link" href="#">Sign out</a>
      </li>
    </ul>
  </nav>

  <div style="margin-top:40px; height: calc(100vh - 40px);" class="container-fluid">
    <div style="margin-top:40px; height: calc(100vh - 40px);" class="row">

      <nav class="col-md-2 d-md-block bg-light sidebar">
        <div class="sidebar-sticky">
          <ul class="nav flex-column">
            <li *ngFor="let navItem of navItems" >
              <button type="button" class="btn btn-link" (click)="navTo(navItem)">{{navItem.name}}</button>
            </li>
          </ul>
        </div>
      </nav>

      <main class="col-md-10">
        <div
          class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pt-3 pb-2 mb-3 border-bottom">
          <h1 class="h2">Dashboard</h1>
        </div>
        <router-outlet></router-outlet>
      </main>

    </div>
  </div>

</div>
```
dash-board.component.css
```css
.btn-link {
    text-align: left;
}
```





