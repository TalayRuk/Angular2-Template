### To display a variable in a template, use curly brackets:
```
<h3>One of my favorite bands is: {{ favoriteBand }}</h3>

```

### To create a variable for a template to use, add a property to the component class. Include a default value if you like.

```
export class AppComponent {
  favoriteBand: string = 'The Cure';
}

```

### We can use any type of data within our components, including creating our own classes and displaying objects by running their methods.

```
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
  <div class="container">
    <h3>One of my favorite albums is: </h3>
    <p>{{ favoriteAlbum.title }}</p>
    <p>By {{ favoriteAlbum.artist }}</p>
    <p>Released in {{ favoriteAlbum.released }}</p>
  </div>
  `
})

export class AppComponent {
  favoriteAlbum: Album = new Album("Disintegration", "The Cure", 1989);
}

export class Album {
  constructor (public title: string, public artist: string, public released: number) {  }
}

```

### We can also show arrays of data in our templates by using for loops:

```

    <div class="pie" *ngFor="let currentPie of favoritePies">
      <p>{{currentPie}}</p>
    </div>

```
- *ngFor is an example of a directive.

////////////////////////////////////////////

### We can start an Angular app by creating a class declaration for the Model first. This is a plan for the type of data we want to keep track of in our app. Then, we can start by simply visualizing a static list of instances of our Model in the App Component.

```
app/app.component.ts
----------------------

import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
  <div class="container">
    <h1>My First Angular 2 App</h1>
    <h3 *ngFor="let currentTask of tasks">{{ currentTask.description }}</h3>
  </div>
  `
})

export class AppComponent {
  public tasks: Task[] = [
      new Task("Create To-Do List app.", 0),
      new Task("Learn Kung Fu.", 1),
      new Task("Rewatch all the Lord of the Rings movies.", 2),
      new Task("Do the laundry.", 3)
  ];
}

export class Task {
  public done: boolean = false;
  constructor(public description: string, public id: number) {   }
}

```

### Use an output binding when you want to trigger an event from a DOM element. For example, Angular has a built-in click event emitter that we can use by attaching it to any HTML element in our templates:

```
@Component({
  selector: 'my-thing',
  template: `
    <h3 (click)="doStuff()"></h3>
  `
})

export class SomeComponent { 
  doStuff() {

  }
}

```

### When this <h3> is clicked, the above output binding would trigger the doStuff method in the component class tied to his template.

### To add an edit form, use ngModel in an <input> tag and connect it to the property of the model object that you are interested in editing.

```
<input [(ngModel)]="selectedTask.description">
```

### Then, don't forget to include the FormsModule in app.module.ts. Import it, then include it in the imports array.
```
app/app.module.ts
--------------------
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule }   from '@angular/forms';
import { AppComponent }   from './app.component';

@NgModule({
  imports: [
    BrowserModule,
    FormsModule
  ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})

export class AppModule { }

```
### Show and hide DOM elements using the *ngIf directive!

```
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
    <div *ngIf="thing">
      <h1>Thing is true and therefore it is displayed!</h1>
    </div>
  `
})

export class AppComponent { 
  thing = "something that is not false";
}

```

### This piece of HTML would cause the <h1> to be displayed if the component class property thing evaluates to true (or to anything that is not false).

- We can trigger things to show or hide by using a click event to trigger a method.

```
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
    <div *ngIf="thing">
      <h1>Thing is true and therefore it is displayed!</h1>
    </div>
    <button (click)="show()">SHOW</button>
    <button (click)="hide()">HIDE</button>
  `
})

export class AppComponent { 
  thing = "something that is not null";
  show() {
    this.thing = "not null";
  }
  hide() {
    this.thing = null;
  }
}

```

### To create a child component, add a new file with three things:

- The import statements at the top
- The component decorator
- The component class declaration

```
import { Component } from '@angular/core';

@Component({
  selector: 'pies',
  template: `
    <h1>HTML HERE</h1>
  `
})

export class PiesListComponent {

}

```

### Remember, the name of the component class should be in UpperCamelCase: export class PiesListComponent { } and the file name should be in lower dash case: pies-list.component.ts.

### Then, include it in app/app.module.ts.

### We need an import statement, and we need to include the component in the declarations array.

```
app/app.module.ts.
----------------------
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule }   from '@angular/forms';
import { PiesListComponent } from './pies-list.component';
import { AppComponent }   from './app.component';

@NgModule({
  imports: [
    BrowserModule,
    FormsModule
  ],
  declarations: [ 
    PiesListComponent,
    AppComponent,
  ],
  bootstrap:    [ AppComponent ]
})

export class AppModule { }

```

### Now, we can use the new child component's selector tag in any other component template to load it:

```
@Component({
  selector: 'my-app',
  template: `
    <pies></pies>
  `
})

```

## Data Down, Actions Up
### When we are using child components, we need them to share data, so we pass data down from the parent components to the child components. But when we need to interact with that data, interaction happens with the child components and events are passed upwards to notify the parents so that data can be changed.

#### Here is an example of passing data down to

```
app/child.component.ts
------------------------
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'child',
  template: `
    <h3>{{ childThing }}</h3>
  `
})

export class ChildComponent {
  @Input() childThing: string;
}

```

### And when we load this in the parent we would connect it up in the template like this:

```
app/parent.component.ts
-------------------------
import { Component } from '@angular/core';

@Component({
  selector: 'child',
  template: `
    <child
      [childThing]="parentThing"
    ></child>
  `
})

export class ParentComponent {
  parentThing = "Hello!";
}

```

### Then, we could output something from the child on a click event like this:

```
app/child.component.ts
--------------------------
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'child',
  template: `
    <h3 (click)="clicked('I have been clicked.')">{{ childThing }}</h3>
  `
})

export class ChildComponent {
  @Input() childThing: string;
  @Output() clickSender = new EventEmitter();
  clicked(thingToSend) {
    // sends the string "I have been clicked" to the parent.
    this.clickSender.emit(thingToSend);
  }
}

```

### Where it would be received like this:
```
app/parent.component.ts
----------------------------
import { Component } from '@angular/core';

@Component({
  selector: 'child',
  template: `
    <child
      [childThing]="parentThing"
      (clickSender)="receiveFromChild($event)"
    ></child>
  `
})

export class ParentComponent {
  parentThing = "Hello!";
  receiveFromChild(aSentence) {
    // prints out whatever is sent from the child on click.
    console.log(aSentence);
  }

```

## To add a component for creating a new instance of a model, it looks like this:

```
app/new-task.component.ts
---------------------------
import { Component, Output, EventEmitter } from '@angular/core';
import { Task } from './task.model';

@Component({
  selector: 'new-task',
  template: `
    <h1>New Task</h1>
    <div>
      <label>Enter Task Description:</label>
      <input #newDescription>
    </div>
    <div>
      <label>Enter Task ID:</label>
      <input #newId>
      <button (click)="
        addClicked(newDescription.value, newId.value);
        newDescription.value='';
        newId.value='';
      ">Add</button>
    </div>
  `
})

export class NewTaskComponent {
  @Output() newTaskSender = new EventEmitter();
  addClicked(description: string, id: number) {
    var newTaskToAdd: Task = new Task(description, id);
    this.newTaskSender.emit(newTaskToAdd);
  }
}

```

### Variables for input fields are set up with this syntax: <input #thingy>.

### Then, on the click of a button, we can pass their values into a method and clear the form with this syntax:

```
<button (click)="
        addStuff(thingy.value);
        thingy.value='';
      ">Create</button>
```

#### This method, which is triggered by the click of a button on our form, can pass the new data to the parent component by emitting an event emitter in the normal way.

/////////////////////pipe///////////////////////////////////
```
app/task-list.component.ts
---------------------------------
<div *ngFor="let currentTask of childTaskList | completeness:selectedCompleteness">

```
### This really is the same process as attaching an event handler in jQuery. Instead of this:

```
<select (change)="onChange($event.target.value)">...</select>
```
#### We would have this:

```
// html
<select id="my-menu-named-whatever">...</select>
// JavaScript
$(document).ready(function(){
  $('#my-menu-named-whatever').change(function(){
    // this callback function is taking the place of our onChange function.
    // Here is where we would store the value of the menu in our 'selectedCompleteness' property so that our pipe can access it.
  });
})

```
///////////////Terminology//////

# Stateless: Something without a current state. In terms of pipes, it means the pipe may transform input to output without completing further steps unless otherwise instructed.

# Stateful: In terms of pipes, the pipe will check whether the output has changed after each change detection cycle. Meaning it will update as soon as we change anything about a task; not simply when we trigger a value.

##Examples
- Here is an example of a task component with checkboxes.

```
app/task.component.ts
--------------------------
import { Component, Input } from '@angular/core';
import { Task } from './task.model';

@Component({
  selector: 'task-display',
  template: `
  <div>
    <input *ngIf="task.done === true" type="checkbox" checked (click)="toggleDone(false)"/>
    <input *ngIf="task.done === false" type="checkbox" (click)="toggleDone(true)"/>
    <label>{{ task.description }}</label>
  </div>
  `
})
export class TaskComponent {
  @Input() task: Task;
  toggleDone(setCompleteness: boolean) {
    this.task.done = setCompleteness;
  }
}

```


