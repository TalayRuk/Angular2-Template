# Angular Setup Checklist


1. mkdir the project directory
2. touch index.html in the top level of the project directory.
3. touch package.json file for npm dependencies.
4. $ bower init to create the bower manifest file, keeping all the defaults.
5. touch .gitignore file.
6. mkdir resources folder, including subfolders for :
    - mkdir resources/images
    - mkdir resources/styles
        -touch resources/styles/styles.css ;to make sure the files are connected up correctly 
           - for example, turn all the <h1> tags blue.
    - mkdir resources/js. 
7. mkdir app 
    - add the root component: touch app/app.component.ts.
8. add the entry point files: 
    - touch app/app.module.ts 
    - touch app/main.ts.
9. Create the Angular configuration files in the top level of your project directory: 
    - touch tsconfig.json
    - touch typings.json
    - touch systemjs.config.js.
10. touch gulpfile.js to the top level of your project directory.
11. Install any bower dependencies, such as Bootstrap. - bower install bootstrap --save
12. Run the 4 development commands.
    - Development Commands
        1.npm install
        2. bower install
        3. gulp build
        4. gulp serve


index.html content
```
<html>
  <head>
    <title>Angular 2 Skeleton</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="build/js/vendor.min.js"></script>
    <link rel="stylesheet" href="build/css/vendor.css">
    <!-- 1. Load libraries -->
     <!-- Polyfill(s) for older browsers -->
    <script src="node_modules/core-js/client/shim.min.js"></script>
    <script src="node_modules/zone.js/dist/zone.js"></script>
    <script src="node_modules/reflect-metadata/Reflect.js"></script>
    <script src="node_modules/systemjs/dist/system.src.js"></script>
    <!-- 2. Configure SystemJS -->
    <script src="systemjs.config.js"></script>

    <link rel="stylesheet" href="build/css/styles.css">
    <script>
      System.import('app').catch(function(err){ console.error(err); });
    </script>
  </head>
  <!-- 3. Display the application -->
  <body>
    <my-app>Loading...</my-app>
  </body>
</html>

```
- touch package.json file for npm dependencies.
```
{
  "name": "angular2-skeleton",
  "version": "1.0.0",
  "scripts": {
    "start": "tsc && concurrently \"npm run tsc:w\" \"npm run lite\" ",
    "lite": "lite-server",
    "postinstall": "typings install",
    "tsc": "tsc",
    "tsc:w": "tsc -w",
    "typings": "typings"
  },
  "license": "ISC",
  "dependencies": {
    "@angular/common": "2.0.0-rc.6",
    "@angular/compiler": "2.0.0-rc.6",
    "@angular/compiler-cli": "0.6.0",
    "@angular/core": "2.0.0-rc.6",
    "@angular/forms": "2.0.0-rc.6",
    "@angular/http": "2.0.0-rc.6",
    "@angular/platform-browser": "2.0.0-rc.6",
    "@angular/platform-browser-dynamic": "2.0.0-rc.6",
    "@angular/router": "3.0.0-rc.2",
    "@angular/upgrade": "2.0.0-rc.6",
    "core-js": "^2.4.1",
    "reflect-metadata": "^0.1.3",
    "rxjs": "5.0.0-beta.11",
    "systemjs": "0.19.27",
    "zone.js": "^0.6.17",
    "angular2-in-memory-web-api": "0.0.18",
    "bootstrap": "^3.3.6"
  },
  "devDependencies": {
    "bower-files": "^3.11.3",
    "browser-sync": "^2.11.1",
    "del": "^2.2.0",
    "gulp": "^3.9.1",
    "gulp-concat": "^2.6.0",
    "gulp-sass": "^2.2.0",
    "gulp-shell": "^0.5.2",
    "gulp-sourcemaps": "1.6.0",
    "gulp-uglify": "^1.5.3",
    "gulp-util": "^3.0.7",
    "concurrently": "^2.2.0",
    "lite-server": "^2.2.2",
    "typescript": "^1.8.10",
    "typings":"^1.3.2"
  }
}

```
- Run bower init to create the bower manifest file, keeping all the defaults.

- touch .gitignore file.

```
node_modules/
npm-debug.log
bower_components/
app/*.js
app/*.js.map
.DS_Store
build/
typings/

```

- mkdir resources folder, including
  - mkdir resources/images
  - mkdir resources/js
  - mkdir resources/styles/styles.css  to the styles folder with a single obvious style rule to make sure the files are connected up correctly - for example, turn all the h1> tags blue.
  
```
  resources/styles/styles.css
  -------------------------------
    h1 {
      color: blue;
    }

```

- mkdir app  and inside of it, add the root component:
  - touch app/app.component.ts

```
app/app.component.ts
---------------------------
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
  <div class="container">
    <h1>My First Angular 2 App</h1>
  </div>
  `
})

export class AppComponent {

}

```

- Also in the app folder, add the entry point files:
 - touch app/app.module.ts
 - touch app/main.ts
 
```
app/app.module.ts
----------------------------------------------------------

import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }   from './app.component';

@NgModule({
  imports: [BrowserModule],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})

export class AppModule { }

***********************************

app/main.ts
----------------------------------------------------------

import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app.module';

const platform = platformBrowserDynamic();

platform.bootstrapModule(AppModule);

```

- Create the Angular configuration files in the top level of your project directory:
  - touch tsconfig.json
  - touch typings.json and
  - touch systemjs.config.js

```
tsconfig.json
----------------------------------------------------------

{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "removeComments": false,
    "noImplicitAny": false
  }
}

***********************************

typings.json
----------------------------------------------------------

{
  "globalDependencies": {
    "core-js": "registry:dt/core-js#0.0.0+20160725163759",
    "jasmine": "registry:dt/jasmine#2.2.0+20160621224255",
    "node": "registry:dt/node#6.0.0+20160831021119"
  }
}

***********************************

systemjs.config.js
----------------------------------------------------------

/**
 * System configuration for Angular 2 samples
 * Adjust as necessary for your application needs.
 */
(function (global) {
  System.config({
    paths: {
      // paths serve as alias
      'npm:': 'node_modules/'
    },
    // map tells the System loader where to look for things
    map: {
      // our app is within the app folder
      app: 'app',
      // angular bundles
      '@angular/core': 'npm:@angular/core/bundles/core.umd.js',
      '@angular/common': 'npm:@angular/common/bundles/common.umd.js',
      '@angular/compiler': 'npm:@angular/compiler/bundles/compiler.umd.js',
      '@angular/platform-browser': 'npm:@angular/platform-browser/bundles/platform-browser.umd.js',
      '@angular/platform-browser-dynamic': 'npm:@angular/platform-browser-dynamic/bundles/platform-browser-dynamic.umd.js',
      '@angular/http': 'npm:@angular/http/bundles/http.umd.js',
      '@angular/router': 'npm:@angular/router/bundles/router.umd.js',
      '@angular/forms': 'npm:@angular/forms/bundles/forms.umd.js',
      // other libraries
      'rxjs':                       'npm:rxjs',
      'angular2-in-memory-web-api': 'npm:angular2-in-memory-web-api',
    },
    // packages tells the System loader how to load when no filename and/or no extension
    packages: {
      app: {
        main: './main.js',
        defaultExtension: 'js'
      },
      rxjs: {
        defaultExtension: 'js'
      },
      'angular2-in-memory-web-api': {
        main: './index.js',
        defaultExtension: 'js'
      }
    }
  });
})(this);

```  

- touch gulpfile.js to the top level of your project directory.
### We can still use npm and gulp to manage our development workflow with a server, and we can still use Bower to manage our frontend dependencies. Here is a sample package.json and gulpfile.js to get you started. 
**There's no need to worry about concatenating and minifying your JavaScript, the TypeScript compiler takes care of that for us, no need for environment variables at this point, and there's no need to browserify anymore..** 
_But we do want a simple build task to pull in our Bower dependencies and put them into our usual vendor.css and vendor.min.js files. We also want to have a task to compile any SASS we're using, and a basic serve task. We are using the same tasks from last week._


```
gulpfile.js
------------------------------------------------------

////////////////////// DEPENDENCIES AND VARIABLES //////////////////////
var gulp = require('gulp');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var lib = require('bower-files')({
  "overrides":{
    "bootstrap" : {
      "main": [
        "less/bootstrap.less",
        "dist/css/bootstrap.css",
        "dist/js/bootstrap.js"
      ]
    }
  }
});

var browserSync = require('browser-sync').create();
var sass = require('gulp-sass');
var sourcemaps = require('gulp-sourcemaps');

gulp.task('jsBower', function () {
  return gulp.src(lib.ext('js').files)
    .pipe(concat('vendor.min.js'))
    .pipe(uglify())
    .pipe(gulp.dest('./build/js'));
});

gulp.task('cssBower', function () {
  return gulp.src(lib.ext('css').files)
    .pipe(concat('vendor.css'))
    .pipe(gulp.dest('./build/css'));
});

gulp.task('bower', ['jsBower', 'cssBower']);

gulp.task('build', ['bower', 'cssBuild']);

gulp.task('serve', function() {
  browserSync.init({
    server: {
      baseDir: "./",
      index: "index.html"
    }
  });

  gulp.watch(['bower.json'], ['bowerBuild']);
  gulp.watch(['*.html'], ['htmlBuild']);
  gulp.watch("scss/*.scss", ['cssBuild']);

});

gulp.task('bowerBuild', ['bower'], function(){
  browserSync.reload();
});

gulp.task('htmlBuild', function(){
  browserSync.reload();
});

gulp.task('cssBuild', function() {
  return gulp.src(['scss/*.scss'])
    .pipe(sourcemaps.init())
    .pipe(sass())
    .pipe(sourcemaps.write())
    .pipe(gulp.dest('./build/css'))
    .pipe(browserSync.stream());
});

gulp.task('cssBuild', ['sassBuild'], function(){
  browserSync.reload();
});

gulp.task('tsBuild', ['ts'], function(){
  browserSync.reload();
});

////////////////////// GLOBAL BUILD TASK //////////////////////
// global build task with individual clean tasks as dependencies.
gulp.task('build', ['ts'], function(){
  // we can use the buildProduction environment variable here later.
  gulp.start('bower');
  gulp.start('sassBuild');
});

```

## Finally, don't forget to add your <script and link> tags to the index.html file, before your final app.js file. The TypeScript compiler will give you errors about jQuery but it will work just fine in the browser if we install it with Bower and then build with our gulpfile. This will pull jQuery, and any of our other frontend dependencies, into our vendor.css and vendor.min.js files to be used in the browser.

### index.html

```
    <link rel="stylesheet" href="build/css/vendor.css">
    <script src="build/js/vendor.min.js"></script>
    <script type="text/javascript" src="build/js/app.js"></script>
```

### Notice that Gulp and the TypeScript compiler can both share the same build folder.

- Install any bower dependencies, such as Bootstrap.
- Run the 4 development commands.

```
Development Commands
-------------
- npm install
- bower install
- bower install bootstrap --save
- gulp build
- gulp serve

```

- Troubleshooting
  - If the above steps have been completed and there are still errors relating to dependencies, try deleting the node_modules and bower_components folders and then rerunning the npm and bower install commands.
