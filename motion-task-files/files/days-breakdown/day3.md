### Day 3 breakdown 

WHAT YOU WILL LEARN TODAY
What React "state" is (variables that make the page update automatically). How to navigate between pages in React without refreshing. How your frontend communicates with your backend using axios. How to store a login token in the browser.

HOUR 1 — SET UP ROUTING (60 MIN)
- 1
In the client folder, install routing and HTTP packages:
npm install axios react-router-dom

- 2
Delete everything inside src/App.js and replace it with a Router setup. Import BrowserRouter, Routes, Route from react-router-dom. Create 3 routes: / (redirects to /login), /login, and /register, and /dashboard.

- 3
Create a src/pages/ folder. Inside it, create 3 empty files: Login.jsx, Register.jsx, and Dashboard.jsx. Each file should export a basic component that just returns a heading for now: return <h1>Login Page</h1>.

- 4
Create src/api.js — this is the single place you configure your API connection so you don't repeat the URL everywhere:
import axios from 'axios';
const api = axios.create({ baseURL: 'http://localhost:5000/api' });
api.interceptors.request.use(config => {
  const token = localStorage.getItem('token');
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});
export default api;


HOUR 2 — BUILD THE REGISTER PAGE (60 MIN)
- 1
In Register.jsx, add two pieces of state using useState: one for email, one for password. Each one will store what the user types into the form fields.
- 2
Build the form: two <input> fields (email + password) and a submit button. Each input should have an onChange handler that updates its state. Example: onChange={(e) => setEmail(e.target.value)}
- 3
Add a handleSubmit function. When the form is submitted, call api.post('/auth/register', { email, password }). Wrap it in a try/catch block. On success, use navigate('/login') to redirect.
- 4
Add an error state. If the API call fails (wrong email, already exists), set the error state and display it as a red paragraph above the form.
- 5
Add a link at the bottom: "Already have an account? <Link to="/login">Login</Link>"


HOUR 3 — BUILD THE LOGIN PAGE (60 MIN)
- 1
The Login page is almost identical to Register. Copy the same structure. The difference is in handleSubmit: after calling api.post('/auth/login'), you get a token back in the response. Save it: localStorage.setItem('token', response.data.token).
- 2
After saving the token, redirect to the dashboard: navigate('/dashboard').
- 3
In Dashboard.jsx, add a logout button. When clicked, it should run: localStorage.removeItem('token') then navigate('/login').
- 4
Test the full flow in the browser: go to /register, create an account, get redirected to login, log in, get redirected to dashboard, click logout, get sent back to login.
- 5
Commit: git add . && git commit -m "Day 3: auth frontend complete" && git push

