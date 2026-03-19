### Day 4 breakdown 

WHAT YOU WILL LEARN TODAY
How to fetch data when a page loads using useEffect. How to split a page into smaller reusable "components". How to pass data between parent and child components with "props". This is the day the app actually does something useful.

HOUR 1 — FETCH AND DISPLAY TASKS (60 MIN)

- 1
In Dashboard.jsx, add a tasks state initialized as an empty array: const [tasks, setTasks] = useState([]).

- 2
Add a useEffect hook that runs once when the page loads. Inside it, call api.get('/tasks') and put the result into your tasks state: setTasks(response.data). useEffect with an empty array [] as the second argument means "run this once when the component first appears".

- 3
Create a src/components/ folder. Inside it, create TaskCard.jsx. This component receives a single task as a "prop" and renders a card showing the task title and a checkbox for completion status.

- 4
In Dashboard.jsx, render your tasks by mapping over the array: {tasks.map(task => <TaskCard key={task.id} task={task} />)}. The key prop is required by React — always use the database ID.

- 5
Test: when you log in, you should see any tasks you created on Day 2 via Thunder Client appear on the screen.


HOUR 2 — ADD AND DELETE TASKS (60 MIN)
- 1
Create src/components/AddTaskForm.jsx. It has a text input and a submit button. It accepts an onAdd prop (a function) that it calls when the form is submitted with the new task title.
- 2
In Dashboard.jsx, write a handleAddTask function: it calls api.post('/tasks', { title }), then updates the tasks state by adding the new task to the array: setTasks([...tasks, newTask]). Pass this function to AddTaskForm as the onAdd prop.
- 3
In TaskCard.jsx, add a delete button. It should accept an onDelete prop. When clicked, call that prop function with the task's ID.
- 4
In Dashboard.jsx, write a handleDeleteTask function: call api.delete('/tasks/' + id), then update state by filtering out the deleted task: setTasks(tasks.filter(t => t.id !== id)).


HOUR 3 — TOGGLE TASK COMPLETION (60 MIN)
- 1
In TaskCard.jsx, make the checkbox call an onToggle prop function when clicked, passing the task ID and new status.

- 2
In Dashboard.jsx, write handleToggleTask: call api.put('/tasks/' + id, { is_complete: !task.is_complete }). Then update the state by mapping through tasks and flipping the is_complete value on the right task.
- 3
Style completed tasks differently in TaskCard.jsx: if task.is_complete is true, add a strikethrough to the title using inline style: style={{ textDecoration: task.is_complete ? 'line-through' : 'none' }}.

- 4
Test every feature end-to-end: add a task, check it complete, uncheck it, delete it.
5
Commit: git add . && git commit -m "Day 4: task CRUD complete" && git push
