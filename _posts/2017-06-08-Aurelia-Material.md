---
layout: post
title:  "Integrating Bootstrap Material Design into Aurelia"
date:   2017-06-08 10:03 PM
categories: Code Aurelia
---

## Introduction
If you aren’t familiar with material design by google, I recommend reading about it [here](https://material.io). Google created a design philosophy [to help teams unite style, branding, interaction, and motion under a cohesive set of principles.](https://design.google.com/articles/design-is-never-done/).  [Federico Zivolo]( https://github.com/FezVrasta) created one of my favorite implementations of this design philosophy.   

Paper Elements or [Material Design for Bootstrap](http://fezvrasta.github.io/bootstrap-material-design/) looks and feels amazing. I love how the buttons pop out so that my users never miss them and how the input fields have little sliding bars whenever they click on them. It is my go to choice when it comes to providing CSS for any websites that I build.   

However, it is a little tricky to integrate this CSS library if you’re building an [Aurelia](http://aurelia.io/) App. There are a couple of pit falls that you have to jump over.

## Packages You Need
There are several packages you need to download
* jquery
* bootstrap
* bootstrap material design
* arrive   

If you're using jspm as your package manager you can use the following command   
`jspm install -y npm:bootstrap npm:bootstrap-material-design npm:arrive npm:jquery`   
Arrive is required if elements on the web page are dynamically created.

## Loading CSS in the Correct Order

The first pitfall is getting around the async nature of css. Bootstrap has to be loaded before Material and then ripples. In index.html use system and css to load them one at a time:    
```
<script>
System.import('bootstrap/css/bootstrap.css!').then(function(){    
    System.import('bootstrap-material-design/dist/css/bootstrap-material-design.css!')
    .then(function(){
        System.import('aurelia-bootstrapper');
    });
});
</script>
```    
Ripples has to be loaded in the root html page that the app serves up. In this case it’s the shell.html.
```
<template>
  <require from="nav-bar.html"></require>
  <require from="bootstra-material-design/dist/css/ripples.css"></require>

  <nav-bar router.bind="router"></nav-bar>

  <div class="page-host">
    <router-view></router-view>
  </div>
</template>
```
## Systemjs/plugin-css
One common issue is that plugin-css doesn't get configured correctly. The command `jspm install -y github:systemjs/plugin-css@^0.1.35` installs the correct version. However, package.json has to be configured differently. plugin-css has to be listed as just "css". To be robust it is best to include both in the package.json file. This is because one will install the correct file into the project while the other will be the correct reference for the config.json.
```
  "jspm": {
    "dependencies": {
        ...
        "css": "github:systemjs/plugin-css@^0.1.35",
        "systemjs/plugin-css": "github:systemjs/plugin-css@0.1.35",
        ...
    },
```

## $.material.init();

The last step is calling `$.material.init();` and including arrive in the root class of the application. shell.ts should look something like this:
```
import {Router, RouterConfiguration} from 'aurelia-router';
import 'arrive';
import 'bootstrap';
import 'bootstrap-material-design';

export class Shell {
  public router: Router;

  public configureRouter(config: RouterConfiguration, router: Router) {
    config.title = 'Aurelia';
    config.map([
      { route: ['', 'home'], name: 'home', moduleId: 'home', nav: true, title: 'Home' },
      { route: ['todo'], name: 'todo', moduleId: 'todo', nav: true, title: 'To Do List' }
    ]);
    this.router = router;
  }

  attached(){
    if($.material){
      $.material.init();
      console.log('material inti run');
    }else{
      console.warn('jquery.material was undefined.');
    }
      
  }
}`
```
If typescript is the language of choice, there isn’t a typings file for material. Here is an example of what can be used in it’s place:
```
`/// <reference path ="../typings/index.d.ts" />
declare class Material {
    init(params?: any): any;
}

interface JQueryStatic{
    material: Material;
}`
```
Make sure to update your tsconfig.json file to find the custom typings files you create.

## Final Thoughts
This should get bootstrap material design into your project. In you run into any issues, I have a test project on my github [here](https://github.com/jessdev/Aurelia-With-Bootstrap-Material-Design). I am also available via my contact page. Otherwise, Have fun!