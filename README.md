# ToDo List in JavaScript

ToDo List Application made purely in JavaScript, CSS, HTML.

## How To Use

Run the follow url in browser

```url
https://yashkumat.github.io/ToDoList/
```

## Usage

Make daily tasks list using this simple application that has following functionalities - 
- Add Task 
- Mark task completed
- Delete completed task
- Delete not completed task with warning

## Lessons Learned

- Add Items

![image](https://raw.githubusercontent.com/yashkumat/ToDoList/main/add_todo.png)

**array.push()**

```javascript
// add item to items
        addItem = () => {
            let item = document.getElementById('item').value;
            if(item != ''){
                item = item.charAt(0).toUpperCase() + item.slice(1);
                items.push(item);
                document.getElementById('item').value = '';
                buildList(items, completed);
            }
        }
```

This function adds item (value in the input field with id 'item') to Items array **if not empty**

- Mark Item Complete

**array.filter()**

```javascript
// complete task
        completeTask = (id) => {
            completed.push(items[id]);
            let value = items[id];

            items = items.filter(function(item) {
                return item !== value
            });

            buildList(items, completed);

        }
```

This function pushes completed item to completed array. Filters (remove) out that item from items array and builds list again.

- Build List 

**DOM Manipulation**

```javascript
// build list not completed items on top and completed items on bottom
        buildList = (items, completed) => {
            let ul = document.getElementById('listGroup');
            let html = '';
            if(items.length > 0){
                items.forEach((item,index) => {
                    html += '<li class="list-group-item d-flex justify-content-between align-items-center"><span id="task'+ index +'">' + item + '</span><div><span class="material-icons completeButton" id="completeButton" onclick="completeTask('+ index +')">done</span> <span class="material-icons deleteButton" id="deleteItem" onclick="deleteItem('+ index +')">delete</span></div></li>';
                });
            }
            if(completed.length > 0){
                completed.forEach((task,id) => {
                    html += '<li class="list-group-item d-flex justify-content-between align-items-center"><span id="taskCompleted">' + task + '</span><div><span class="material-icons completedButton">done</span> <span class="material-icons deleteButton" id="deleteItem" onclick="deleteCompletedItem('+ id +')">delete</span></div></li>';
                });
            }
            if(items.length <=0 && completed.length <= 0){
                html += '<li class="list-group-item d-flex justify-content-between align-items-center"><span>Nothing to do!</span><button type="button" onclick="addFocus()" class="btn btn-outline-primary btn-sm hoverable pt-1" aria-label="Add Item">Add Task</button></li>';
            }
            ul.innerHTML = html;
        }
``` 

This function changes content of unordered list (with id list-group) every time it is called. It display list of item in items array (task to be completed with mark complete and delete button), list of item in completed array (completed tasks with delete button)


- Delete Item

```javascript
// Delete completed item
        deleteCompletedItem = (id) => {
            let value = completed[id];

            completed = completed.filter(function(item) {
                return item !== value
            });

            buildList(items, completed);
        }
```

This function filters out item from completed list and builds list again in frontend.
