### Day 5 breakdown 

WHAT YOU WILL LEARN TODAY
Tailwind works by adding short class names directly to your HTML elements instead of writing separate CSS files. p-4 means padding 16px. text-lg means large text. bg-blue-500 means a blue background. You'll see instant results.

HOUR 1 — INSTALL TAILWIND (60 MIN)

- 1
In your client folder, install Tailwind:
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

- 2
Open the newly created tailwind.config.js and update the content array to tell Tailwind which files to scan:
content: ["./src/**/*.{js,jsx,ts,tsx}"]

- 3
Open src/index.css, delete everything in it, and replace with these 3 lines:
@tailwind base;
@tailwind components;
@tailwind utilities;

- 4
Restart your React dev server (Ctrl+C then npm start again). Tailwind should now work — test it by adding className="text-blue-500 text-2xl" to any element and watching it turn blue and large.


HOUR 2 — STYLE THE AUTH PAGES (60 MIN)
- 1
Style the Login and Register pages to be centered cards. Wrap the form in: className="min-h-screen bg-gray-50 flex items-center justify-center" on the outer div, and className="bg-white p-8 rounded-xl shadow-sm border border-gray-200 w-full max-w-md" on the card.
- 2
Style the inputs: className="w-full border border-gray-300 rounded-lg px-3 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
- 3
Style the submit button: className="w-full bg-blue-600 text-white rounded-lg py-2 text-sm font-medium hover:bg-blue-700 transition-colors"
- 4
Add labels above each input, styled with className="block text-sm font-medium text-gray-700 mb-1". Add a mb-4 div wrapping each label+input pair to create spacing between fields.

HOUR 3 — STYLE THE DASHBOARD (60 MIN)
- 1
Style the Dashboard layout. A top navbar: className="bg-white border-b border-gray-200 px-6 py-4 flex justify-between items-center". Main content area below: className="max-w-2xl mx-auto px-4 py-8".

- 2
Style each TaskCard: className="bg-white border border-gray-200 rounded-lg p-4 mb-3 flex items-center gap-3". For completed tasks, add opacity-60 to the card class.

- 3
Style the delete button: a small red trash icon or an "×" styled with className="ml-auto text-gray-400 hover:text-red-500 text-lg cursor-pointer".

- 4
Style the AddTaskForm: a horizontal row with an input that stretches to fill space and an "Add" button beside it. Use className="flex gap-2" on the wrapper, flex-1 on the input.

- 5
Make it mobile responsive — check it at different window sizes. Most Tailwind classes already work on all screens. Add px-4 sm:px-6 to main containers for comfortable side spacing on small screens.

- 6
Commit: git add . && git commit -m "Day 5: Tailwind styling complete" && git push
