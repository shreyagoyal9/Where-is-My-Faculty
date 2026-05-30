
AUTHOR: SHANSIT SUMAN & SHREYA GOYAL

How to Run in my device:
1) open the folder in your VS code.
2) change directory to backend (cd backend)
3) give command to node/nodemon to run the backend (node server.js)
(verify if it's running properly: 
Server running on port 5000
MongoDB connected successfully)
4) open new terminal/Split terminal
5) change directory to frontend (cd frontend)
6) give cmd to run the frontend in development mode (npm run dev)
(verify if frontend running properly: it'll provide you a localhost url)
7) NOW YOU ARE GOOD TO GO, JUST CLICK ON THAT http://localhost:5173/ URL 


## Project Structure

```
Where-is-My-Faculty/
│
├── backend/
│   ├── config/
│   │   └── db.js
│   │
│   ├── controllers/
│   │   ├── adminController.js
│   │   ├── clubController.js
│   │   ├── facultyController.js
│   │   └── studentController.js
│   │
│   ├── middleware/
│   │   ├── auth.js
│   │   ├── clubAuth.js
│   │   └── facultyAuth.js
│   │
│   ├── models/
│   │   ├── Admin.js
│   │   ├── Club.js
│   │   ├── Event.js
│   │   ├── Faculty.js
│   │   └── Student.js
│   │
│   ├── routes/
│   │   ├── admin.js
│   │   ├── club.js
│   │   ├── faculty.js
│   │   └── student.js
│   │
│   ├── uploads/
│   │   └── (uploaded images)
│   │
│   ├── index.js
│   ├── server.js
│   ├── package.json
│   └── package-lock.json
│
├── frontend/
│   ├── public/
│   │   ├── admin-dashboard.html
│   │   ├── club-dashboard.html
│   │   ├── faculty-dashboard.html
│   │   ├── student-dashboard.html
│   │   ├── login & register pages
│   │   ├── js/
│   │   │   └── script.js
│   │   └── img/
│   │       └── (static images)
│   │
│   ├── css/
│   │   └── style.css
│   │
│   ├── src/
│   │   └── input.css
│   │
│   ├── index.html
│   ├── tailwind.config.js
│   ├── postcss.config.js
│   ├── package.json
│   └── package-lock.json
│
└── README.md
```
```
