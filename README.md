## Ex03 To-Do List using JavaScript
## Date:28-03-2025
## NAME:KEERTHANA S
## REG NO: 2122223040092
## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
## STEP 1
Build the HTML structure (index.html).

## STEP 2
Style the App (style.css).

## STEP 3
Plan the features the To-Do App should have.

## STEP 4
Create a To-do application using Javascript.

## STEP 5
Add functionalities.

## STEP 6
Test the App.

## STEP 7
Open the HTML file in a browser to check layout and functionality.

## STEP 8
Fix styling issues and refine content placement.

## STEP 9
Deploy the website.

## STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
# todo.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <link rel="stylesheet" href="todo.css">
</head>
<body>
    <div class="container">
        <h1>To Do List</h1>
        <div class="input-area">
            <input type="text" id="taskInput" placeholder="Enter a task">
            <button id="addTask">Add Task</button>
        </div>
        <ul class="task-list" id="taskList"></ul>
        <button id="clearAll" class="clear-btn">Clear All</button>
    </div>
    <script src="todo.js"></script>
</body>
</html>

```
# todo.css
```

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Poppins', sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: linear-gradient(135deg, #74ebd5 0%, #ACB6E5 100%);
}

.container {
    background: #ffffff;
    padding: 30px 25px;
    border-radius: 16px;
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.2);
    width: 360px;
}

h1 {
    text-align: center;
    margin-bottom: 25px;
    color: #333;
    font-size: 28px;
}

.input-area {
    display: flex;
    margin-bottom: 20px;
}

.input-area input {
    flex-grow: 1;
    padding: 12px 10px;
    border: 2px solid #ccc;
    border-radius: 8px;
    font-size: 16px;
    transition: 0.3s;
}

.input-area input:focus {
    border-color: #74ebd5;
    outline: none;
}

.input-area button {
    margin-left: 8px;
    padding: 12px 18px;
    background: #4CAF50;
    color: white;
    font-size: 16px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background 0.3s;
}

.input-area button:hover {
    background: #45a049;
}

.task-list {
    list-style: none;
    padding: 0;
    margin-bottom: 15px;
}

.task-list li {
    background: #f9f9f9;
    margin-bottom: 12px;
    padding: 12px 15px;
    border-radius: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    animation: fadeIn 0.5s;
}

.task-list li.completed {
    background: #d4edda;
    text-decoration: line-through;
    color: #555;
}

.task-list li span {
    flex-grow: 1;
    cursor: pointer;
}

.task-list li button {
    border: none;
    padding: 8px 12px;
    margin-left: 6px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 14px;
    transition: background 0.3s;
}

.task-list li .edit-btn {
    background-color: #2196F3;
    color: #fff;
}

.task-list li .edit-btn:hover {
    background-color: #0b7dda;
}

.task-list li .delete-btn {
    background-color: #f44336;
    color: #fff;
}

.task-list li .delete-btn:hover {
    background-color: #da190b;
}

.clear-btn {
    width: 100%;
    padding: 12px;
    background-color: #ff9800;
    color: white;
    border: none;
    font-size: 16px;
    border-radius: 8px;
    cursor: pointer;
    transition: background 0.3s;
}

.clear-btn:hover {
    background-color: #e68900;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(-10px);}
    to { opacity: 1; transform: translateY(0);}
}


```
# todo.js
```
document.addEventListener('DOMContentLoaded', () => {
    const taskInput = document.getElementById('taskInput');
    const addTaskBtn = document.getElementById('addTask');
    const taskList = document.getElementById('taskList');
    const clearAllBtn = document.getElementById('clearAll');

    loadTasks();
    addTaskBtn.addEventListener('click', () => {
        if (taskInput.value.trim()) {
            createTask(taskInput.value.trim());
            taskInput.value = '';
            saveTasks();
        }
    });

    taskInput.addEventListener('keypress', (e) => {
        if (e.key === 'Enter') addTaskBtn.click();
    });

    clearAllBtn.addEventListener('click', () => {
        if (confirm('Delete all tasks?')) {
            taskList.innerHTML = '';
            saveTasks();
        }
    });

    function createTask(text, completed = false) {
        const li = document.createElement('li');
        if (completed) li.classList.add('completed');

        li.innerHTML = `
            <span>${text}</span>
            <div class="actions">
                <button class="edit-btn">Edit</button>
                <button class="delete-btn">X</button>
            </div>
        `;

        li.querySelector('span').addEventListener('click', () => {
            li.classList.toggle('completed');
            saveTasks();
        });

        li.querySelector('.edit-btn').addEventListener('click', () => {
            const newText = prompt('Edit task:', li.querySelector('span').textContent);
            if (newText !== null && newText.trim()) {
                li.querySelector('span').textContent = newText.trim();
                saveTasks();
            }
        });

        li.querySelector('.delete-btn').addEventListener('click', () => {
            li.remove();
            saveTasks();
        });

        taskList.appendChild(li);
    }

    function saveTasks() {
        const tasks = [...taskList.children].map(li => ({
            text: li.querySelector('span').textContent,
            completed: li.classList.contains('completed')
        }));
        localStorage.setItem('tasks', JSON.stringify(tasks));
    }

    function loadTasks() {
        const tasks = JSON.parse(localStorage.getItem('tasks')) || [];
        tasks.forEach(task => createTask(task.text, task.completed));
    }
});


```
## OUTPUT
![image](https://github.com/user-attachments/assets/dbd1435e-1bdb-466e-b17c-09188e39ac96)

## RESULT
The program for creating To-do list using JavaScript is executed successfully.
