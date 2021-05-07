# toDoApp
Reusable toDo App made using HTML, CSS, and JS

This project creates a toDo application which can be cross-utilized and formatted depending on the user needs. 

This project helped me to practice and better understand the following:
1) autocomplete="off" property with HTML <input> element.
2) text-decoration: line-through property.
3) Using 'contextmenu' to select for a right-click event listener.
4) Using local storage.
5) DOM manipulation
6) Creating and implementing logic


A general walkthrough of the JavaScript is given below.

Select the elements to be manipulated by the DOM.
```JavaScript
const form = document.getElementById('form');
const input = document.getElementById('input');
const todos = document.getElementById('todos');
```

Add an event listener to the form.
```JavaScript
form.addEventListener('submit', (e) => {
    e.preventDefault();
    addToDo();
});
```

Add addToDo() function. This will create list-items to store input values that have been submitted. It will also use a nested right-click(contextmenu) event listener to delete list-items.
```JavaScript
 function addToDo(todo){
        let todoText = input.value;
        if(todo){
            todoText = todo.text;
        }

    if(todoText) {
        const todoEl = document.createElement('li');
        if(todo && todo.completed){
            todoEl.classList.add('completed');

        }
        todoEl.innerText = todoText;

        todoEl.addEventListener('click', () => {
            todoEl.classList.toggle('completed');
            updateLS();
        });

        todoEl.addEventListener('contextmenu', (e) => {
            e.preventDefault();
            todoEl.remove();
            updateLS();
        })

        todosUL.appendChild(todoEl);
        input.value = '';
        updateLS();
    } 
};
```

Add updateLS() function.
```JavaScript
function updateLS(){
    const todosEl = document.querySelectorAll('li');

    const todos = [];

    todosEl.forEach(todoEl => {
        todos.push({
            text: todoEl.innerText,
            completed: todoEl.classList.contains('completed')
        })
    });
    localStorage.setItem('todos', JSON.stringify(todos));
}
```

Setup data retreival from local storage.
```JavaScript
const todos = JSON.parse(localStorage.getItem('todos'));
if(todos){
    todos.forEach(todo => {
        addToDo(todo)
    })
}
```

***End walkthrough
