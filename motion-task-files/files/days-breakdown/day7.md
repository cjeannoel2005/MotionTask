### Day 7 breakdown 

WHAT YOU WILL LEARN TODAY
Deployment means taking code off your laptop and putting it on a server that is always on and accessible to anyone on the internet. You will deploy the backend (with its database) to Railway and the frontend to Vercel. Both are free.

HOUR 1 — DEPLOY THE BACKEND TO RAILWAY (60 MIN)

- 1
Create a free account at railway.app using your GitHub account.

- 2
Click "New Project" → "Deploy from GitHub repo" → select your taskflow repo. Choose the server folder as the root directory.

- 3
Add a PostgreSQL database to your Railway project: click "+ New" → "Database" → "Add PostgreSQL". Railway will create a live database and automatically give you a DATABASE_URL environment variable.

- 4
Add your environment variables in Railway: go to your server service → "Variables" tab → add JWT_SECRET (same long random string from your .env file). The DATABASE_URL is already set automatically.

- 5
Railway needs to know how to start your server. Add a start script to server/package.json: "start": "node index.js". Commit and push this change.

- 6
Once deployed, Railway gives you a public URL (like taskflow-production.up.railway.app). Open that URL in your browser — you should see "Hello World!" which means your backend is live.

- 7
Re-run your database migration on Railway: in the Railway dashboard, open the PostgreSQL service → "Data" tab → run your CREATE TABLE SQL again to create the tables in the live database.

HOUR 2 — DEPLOY THE FRONTEND TO VERCEL (60 MIN)
- 1
In src/api.js, update the baseURL to use an environment variable so it works both locally and in production:
baseURL: process.env.REACT_APP_API_URL || 'http://localhost:5000/api'

- 2
Commit and push this change to GitHub.

- 3
Create a free account at vercel.com using your GitHub account. Click "Add New Project" → import your taskflow repo. Set the root directory to client.

- 4
Before deploying, go to "Environment Variables" and add: REACT_APP_API_URL = your Railway backend URL (e.g. https://taskflow-production.up.railway.app/api).

- 5
Click Deploy. Vercel builds your React app and gives you a public URL like taskflow.vercel.app.

- 6
Test the live site completely: register a new account, log in, add a task, complete it, delete it, log out. All from the Vercel URL.

HOUR 3 — FINAL TOUCHES & RESUME (60 MIN)
- 1
Update your README.md with the live Vercel URL at the top. Add a "Live Demo" badge or link as the first line. Push to GitHub.

- 2
Make sure your GitHub repository is public. Clean up any stray console.log statements. Check the GitHub repo page looks professional — the README should render nicely with sections and code blocks.

- 3
Pin the repository to your GitHub profile: go to your profile → click "Customize your pins" → select taskflow. This makes it the first thing visitors see.

- 4
Add to your resume under Projects:

TaskFlow — Full-Stack Task Management App
React, Node.js, Express, PostgreSQL, JWT Auth, Tailwind CSS
Built a full-stack web app with user authentication, RESTful API, and PostgreSQL database. Deployed to Railway (backend) and Vercel (frontend).

Include both the GitHub URL and the live Vercel URL.
5
Take a screenshot of the live app for your portfolio. If you have a portfolio site, add the project there too.
