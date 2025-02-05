# Exercise - Functions as Props

## Exercise Overview

We are going to create a simple task manager application that displays a list of tasks and includes buttons to mark tasks as complete or delete them. We'll iterate over an array of tasks using manual mapping, and we'll pass the task title as a parameter to the complete function.

## Set Up And Run A New React App

1. Open the terminal to the `exercise` directory--the simplest way to do so is to right-click on the `exercise` folder in VS Code and select "Open in Integrated Terminal".

2. In the terminal, type `npm create vite task-manager-app`. Here we are naming our project task-manager-app.

3. Choose React and then JavaScript from the menus, using arrow keys and Enter/Return.

4. Now you want to either:

- change directory to the new project folder by typing `cd task-manager-app` in the terminal
- or, **preferably**, open the project folder in VS Code by choosing File > Open Folder from the menus and selecting the task-manager-app folder, then open the terminal with Terminal > New Terminal from the menus (or Ctrl+`).

5. Install dependencies by entering `npm install` in the terminal.

6. Run the app by typing `npm run dev` in the terminal. This will provide a clickable link to open the app in your default browser, or you can navigate to the localhost URL in your browser.

## Creating the App Component

Open /src/App.jsx. This file is an example component that Vite starts us with. You can delete everything in this file. Then at the top of the file, you can create a functional component named App. Don't forget to export it.

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

Back inside /src/App.jsx, below our heading, place a <div>.

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

In VS Code, in the File Explorer to the left, right-click on the /src/ folder and select New File. Name the file Task.jsx.

Open /src/Task.jsx and create a function called Task that returns a <div> inside of parentheses. Don't forget to export the function at the bottom of the file.

Inside the `div`, let's write some placeholder text: `This is a Task.`

```jsx
function Task() {
  return <div>This is a Task</div>;
}

export default Task;
```

Let's try to import this Task into our App component. Open /src/App.jsx again and after importing React, create a new line to import our Task: `import Task from './Task';`

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

Open /src/App.jsx and create two functions to handle actions: `completeTask` and `deleteTask`.

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

Head back to /src/Task.jsx. Let's update the Task component to display task details and include buttons to mark tasks as complete and delete them.

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

Here is the finished code for App.jsx:

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

Here is the finished code for Task.jsx:

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
