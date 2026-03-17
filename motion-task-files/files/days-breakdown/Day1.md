### Day 1 breakdown 
WHAT YOU WILL LEARN TODAY
How a React frontend and a Node.js backend are two separate programs that talk to each other. How Git tracks every change you make. What a "terminal" is and why developers live in it.


HOUR 1 — INSTALL EVERYTHING (60 MIN)
- 1
Download and install Node.js LTS from nodejs.org. This also installs npm, the tool that downloads code packages for you.
- 2
Download and install VS Code from code.visualstudio.com. This is your code editor — think of it as Microsoft Word, but for code.
- 3
Download and install Git from git-scm.com. During install, choose "Use Git from the command line and also from 3rd-party software" if asked.
- 4
Create a free account at github.com. Then open a terminal in VS Code (menu → Terminal → New Terminal) and run:
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
- 5
Download and install PostgreSQL from postgresql.org/download. Write down the password you set — you will need it every day.
- 6
Install the 8 VS Code extensions listed in your setup guide (Prettier, ESLint, Thunder Client, etc.). Press Ctrl+Shift+X to open the extensions panel.


HOUR 2 — CREATE YOUR PROJECT (60 MIN)
- 1
On github.com, click "New Repository". Name it taskflow. Check "Add a README". Click Create. Then click the green "Code" button and copy the URL.
- 2
In your VS Code terminal, navigate to your Desktop and clone it:
cd Desktop
git clone https://github.com/YOURUSERNAME/taskflow.git
cd taskflow
- 3
Create the React frontend. This command builds an entire starter app for you automatically:
npx create-react-app client
- 4
Create your backend folder and initialize it:
mkdir server
cd server
npm init -y
npm install express cors dotenv
- 5
Inside the server folder, create a file called index.js. Paste this code in:
const express = require('express');
const app = express();
app.get('/', (req, res) => res.send('Hello World!'));
app.listen(5000, () => console.log('Server running on port 5000'));
- 6
Run node index.js in the terminal. Open a browser and go to localhost:5000. You should see "Hello World!"
