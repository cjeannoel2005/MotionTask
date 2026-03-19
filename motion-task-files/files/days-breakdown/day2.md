### Day 3 breakdown 
WHAT YOU WILL LEARN TODAY
What a database table is (like a spreadsheet with strict rules). What an API route is (a URL your frontend calls to get or save data). What a "middleware" is. How passwords should never be stored as plain text.

HOUR 1 — SET UP POSTGRESQL (60 MIN)
- 1
Open pgAdmin (installed with PostgreSQL). Connect to your local server. Right-click "Databases" → Create → Database. Name it taskflow.

- 2
Click the taskflow database, then click the "Query Tool" button (looks like a lightning bolt). Paste and run this SQL to create your two tables:
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE tasks (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  is_complete BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT NOW()
);

- 3
In your server folder, create a .env file (this stores secrets and never gets uploaded to GitHub):
DATABASE_URL=postgresql://postgres:YOURPASSWORD@localhost:5432/taskflow
JWT_SECRET=makethisalongrandombunchofcharacters

- 4
Create a .gitignore file in your server folder with this content: node_modules/ and .env — this stops secrets from uploading to GitHub.

- 5
Install database and auth packages:
npm install pg bcrypt jsonwebtoken
- 6
Create server/db.js — this is the connection between your code and PostgreSQL:
const { Pool } = require('pg');
require('dotenv').config();
const pool = new Pool({ connectionString: process.env.DATABASE_URL });
module.exports = pool;


HOUR 2 — BUILD THE API ROUTES (60 MIN)
- 1
Create server/routes/auth.js. Build the POST /register route: accept email + password, hash the password with bcrypt.hash(password, 10), insert the user into the database, return a success message.

- 2
In the same file, build the POST /login route: find the user by email, compare the password with bcrypt.compare(), if it matches sign a JWT token with jwt.sign({ userId: user.id }, process.env.JWT_SECRET) and return it.

- 3
Create server/middleware/auth.js — this checks the token on every protected route:
const jwt = require('jsonwebtoken');
module.exports = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) return res.status(401).json({ error: 'No token' });
  req.user = jwt.verify(token, process.env.JWT_SECRET);
  next();
};
- 4
Create server/routes/tasks.js. Build these 4 routes, all protected by your auth middleware: GET / (fetch user's tasks), POST / (create task), PUT /:id (update task), DELETE /:id (delete task). Each route queries the database using pool.query().
- 5
Update server/index.js to use these routes:
app.use(express.json());
app.use(require('cors')());
app.use('/api/auth', require('./routes/auth'));
app.use('/api/tasks', require('./middleware/auth'), require('./routes/tasks'));


HOUR 3 — TEST EVERY ROUTE (60 MIN)
- 1
Open Thunder Client in the VS Code sidebar (the lightning bolt icon). Create a new request. Set method to POST, URL to localhost:5000/api/auth/register. In the "Body" tab, select JSON and enter: {"email":"test@test.com","password":"password123"}. Hit Send. You should get a success response.

- 2
Test POST /api/auth/login the same way. Copy the token from the response — you'll need it for the next tests.

- 3
Test GET /api/tasks. In the "Headers" tab, add: Key = Authorization, Value = Bearer YOURTOKEN. You should get an empty array back — that's correct, no tasks yet.

- 4
Test POST /api/tasks with the auth header and body {"title":"My first task"}. Then test the GET again — you should see your task in the response.

- 5
Commit your work: git add . && git commit -m "Day 2: database and API complete" && git push
