### Day 6 breakdown 

Real apps don't just work — they handle failure gracefully. Today you will add every detail that makes your app feel production-grade: loading spinners, empty states, form validation, and route guards. This is the work that impresses in code reviews.

HOUR 1 — LOADING STATES & EMPTY STATES (60 MIN)

- 1
Add a loading state to your Dashboard: const [loading, setLoading] = useState(true). Set it to true before the API call and false after. In the return, if loading is true, render a spinner div instead of the task list.

- 2
A simple spinner in Tailwind (no library needed): <div className="animate-spin h-6 w-6 border-2 border-blue-500 border-t-transparent rounded-full mx-auto mt-12"></div>

- 3
Add an empty state: if tasks.length === 0 and not loading, show a friendly message instead of a blank page: a centered illustration area with the text "No tasks yet. Add one above!"

- 4
Add a loading state to the "Add Task" button. When the form is submitting, disable the button and change its text to "Adding...". This prevents double-submitting if the user clicks twice.

HOUR 2 — FORM VALIDATION & ERROR MESSAGES (60 MIN)
- 1
In your Login and Register pages, add client-side validation before calling the API. Check: is the email field empty? Does it contain an "@"? Is the password at least 6 characters? If any check fails, set an error state and show a message — do not call the API.

- 2
Style the error messages using Tailwind: className="bg-red-50 text-red-700 border border-red-200 rounded-lg px-4 py-2 text-sm". Place them above the submit button.

- 3
In the AddTaskForm, prevent submitting an empty task title. Show an inline error if the user tries. Clear the error as soon as they start typing.

- 4
Wrap all API calls in try/catch blocks if they aren't already. In the catch, check for common errors: if the error response is 401 (unauthorized), remove the token and redirect to login. If it's anything else, show a generic "Something went wrong. Please try again." message.

HOUR 3 — PROTECTED ROUTES & README (60 MIN)
- 1
Create src/components/ProtectedRoute.jsx. This component checks if a token exists in localStorage. If yes, it renders the children (the page). If no, it redirects to /login using the Navigate component from react-router-dom.

- 2
Wrap your Dashboard route in App.js with <ProtectedRoute>. Test: when logged out, going to /dashboard should automatically redirect to /login.
- 3
Write your README.md in the root folder. Include: what the project is, what it does, the full tech stack list, how to run it locally (step by step), and a link to the live demo (you'll add this tomorrow). This is the first thing any employer reads.
- 4
Final commit before deployment: git add . && git commit -m "Day 6: error handling and polish complete" && git push

