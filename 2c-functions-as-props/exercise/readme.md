# Exercise - Functions as Props

## Exercise Overview

We are going to create a simple task manager application that displays a list of tasks and includes buttons to mark tasks as complete or delete them. We'll iterate over an array of tasks using manual mapping, and we'll pass the task title as a parameter to the complete function.

## Set Up A New Create-React-App Project

Open VS Code and then open your terminal from the menus at the top of the screen under View > Terminal or use the shortcut key Ctrl+`.

In Terminal type npx create-react-app task-manager. Here we are naming our project task-manager. Wait while a new project is setup... It will display "Happy hacking!" when it's done.

Then in Terminal type cd task-manager to enter the project folder.

## Start Node Test Server

In terminal type npm start to start a node test server. This should open a new tab in your browser to localhost:3000.

## Creating the App Component

Open /src/App.js. This file is an example component that create-react-app starts with. You can delete everything in this file. Then at the top of the file, you can create a functional component named App. Don't forget to export it.

Create a <div> inside of the return() statement.

```jsx
function App() {
  return <div></div>;
}

export default App;
```

Then inside the <div> create a heading <h1>Task Manager</h1>.

```jsx
function App() {
  return (
    <div>
      <h1>Task Manager</h1>
    </div>
  );
}
```

Save the file and visit the browser to make sure our heading is appearing.

Back inside /src/App.js, below our heading, place a <div>.

```jsx
function App() {
  return (
    <div>
      <h1>Task Manager</h1>
      <div></div>
    </div>
  );
}
```

## Creating the Task Component

In VS Code, in the File Explorer to the left, right-click on the /src/ folder and select New File. Name the file Task.js.

Open /src/Task.js and create a function called Task that returns a <div> inside of parentheses. Don't forget to export the function at the bottom of the file.

Inside the `div`, let's write some placeholder text: `This is a Task.`

```jsx
function Task() {
  return <div>This is a Task</div>;
}

export default Task;
```

Let's try to import this Task into our App component. Open /src/App.js again and after importing React, create a new line to import our Task: `import Task from './Task';`

Then, inside of the <div>, render your Task component with <Task />.

```jsx
import Task from "./Task";

function App() {
  return (
    <div>
      <h1>Task Manager</h1>
      <div>
        <Task />
      </div>
    </div>
  );
}

export default App;
```

Save and check the browser. You should see the text: "This is a Task"

## Passing Functions as Props and Iterating Manually

Let's use props to pass functions from our App component to our Task component. We will create functions to mark tasks as complete and delete them. We'll also iterate over an array of tasks manually. **You could, alternately, use a `.map`, before the JSX or inline in it.**

Open /src/App.js and create two functions to handle actions: `completeTask` and `deleteTask`.

```jsx
import Task from "./Task";

function App() {
  const tasks = [
    { id: 1, title: "Morning Walk", description: "Take a 30-minute walk in the park" },
    { id: 2, title: "Grocery Shopping", description: "Buy groceries for the week" },
    { id: 3, title: "Read a Book", description: "Finish reading 'The Great Gatsby'" },
  ];

  const completeTask = (taskTitle) => {
    alert(`${taskTitle} completed!`);
  };

  const deleteTask = () => {
    alert("Task deleted!");
  };

  const taskElements = [];
  for (const task of tasks) {
    taskElements.push(<Task key={task.id} task={task} complete={() => completeTask(task.title)} delete={deleteTask} />);
  }

  return (
    <div>
      <h1>Task Manager</h1>
      <div>
        {taskElements}
      </div>
    </div>
  );
}

export default App;
```

**Explanation**:

Tasks Array: We have an array of tasks, each containing id, title, and description.

Functions: We create completeTask to display an alert with the task title (e.g., "Morning Walk completed!") and deleteTask to display an alert with the message "Task deleted!".

Manual Mapping: We manually iterate over the tasks array using a for...of loop and push a <Task /> component into the taskElements array for each task.

Anonymous Arrow Function: We use an anonymous arrow function to call completeTask with the task title as a parameter.

Rendering: We render taskElements inside the return statement.

## Updating the Task Component

Head back to /src/Task.js. Let's update the Task component to display task details and include buttons to mark tasks as complete and delete them.

```jsx
function Task(props) {
  return (
    <div>
      <h2>{props.task.title}</h2>
      <p>{props.task.description}</p>
      <button onClick={props.complete}>Complete</button>
      <button onClick={props.delete}>Delete</button>
    </div>
  );
}

export default Task;
```

**Explanation**:

Displaying Props: We use {props.task.title} and {props.task.description} to display the task title and description.

Button Handlers: We use onClick={props.complete} and onClick={props.delete} to call the functions passed as props when the buttons are clicked.

Here is the finished code for App.js:

```jsx
import Task from "./Task";

function App() {
  const tasks = [
    { id: 1, title: "Morning Walk", description: "Take a 30-minute walk in the park" },
    { id: 2, title: "Grocery Shopping", description: "Buy groceries for the week" },
    { id: 3, title: "Read a Book", description: "Finish reading 'The Great Gatsby'" },
  ];

  const completeTask = (taskTitle) => {
    alert(`${taskTitle} completed!`);
  };

  const deleteTask = () => {
    alert("Task deleted!");
  };

  const taskElements = [];
  for (const task of tasks) {
    taskElements.push(<Task key={task.id} task={task} complete={() => completeTask(task.title)} delete={deleteTask} />);
  }

  return (
    <div>
      <h1>Task Manager</h1>
      <div>
        {taskElements}
      </div>
    </div>
  );
}

export default App;
```

Here is the finished code for Task.js:

```jsx
function Task(props) {
  return (
    <div>
      <h2>{props.task.title}</h2>
      <p>{props.task.description}</p>
      <button onClick={props.complete}>Complete</button>
      <button onClick={props.delete}>Delete</button>
    </div>
  );
}

export default Task;
```
