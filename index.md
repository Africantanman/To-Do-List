<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>TodoTracker</title>
  <style>
    body {
      padding: 15px;
      background-color: rgb(67, 192, 230);
      font-family: Arial;
    }
    #title {
      padding: 10px;
      font-size: 35px;
      text-align: center;
      border: 4px solid rgb(177, 229, 241);
      width: 245px;
    }
    #todo-header {
      font-size: 25px;
      text-decoration-line: underline;
      text-decoration-style: double;
    }

    ul {
      list-style: none;
      padding-left: 0;
      width: 250px;
    }

    li {
      colour: #333;
      background-color: rgba(255, 255, 255, .5);
      padding: 10px;
      margin-bottom: 15px;
      border-radius: 5px;
      text-align: center;
    }

  </style>
</head>
<body>
  <h1 id="title">Todo Tracker</h1>

  <form>
    <input type="text" id="user-todo" placeholder="New Todo" required>
  </form>

  <h2 id="todo-header">Todos</h2>
  <ul>

  </ul>

  <button id="clear">Clear All</button>

  <script>
    var form = document.querySelector('form');
    var todoList = document.querySelector('ul');
    var button = document.querySelector('button');
    var input = document.getElementById('user-todo');

    
    var todosArray = localStorage.getItem('todos') ? JSON.parse(localStorage.getItem('todos')) : [];

    localStorage.setItem('todos', JSON.stringify(todosArray));

    var storage = JSON.parse(localStorage.getItem('todos'));

    form.addEventListener('submit', function (e) {
      e.preventDefault();

      todosArray.push(input.value);
      
      localStorage.setItem('todos', JSON.stringify(todosArray));
      todoMaker(input.value);
      input.value = "";
    });

    var todoMaker = function(text) {
      var todo = document.createElement('li');
      todo.textContent = text;
      todoList.appendChild(todo);
    }

    for (var i = 0; i < storage.length; i++) {
      todoMaker(storage[i]);
    }

    button.addEventListener('click', function() {
      
      localStorage.clear();
      while (todoList.firstChild) {
        todoList.removeChild(todoList.firstChild);
      }
    })

  </script>
</body>
</html>