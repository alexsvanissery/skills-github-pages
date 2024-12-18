<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student and Teacher Login</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f0f0;
        }
        .container {
            width: 100%;
            max-width: 400px;
            margin: 50px auto;
            background: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 5px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input, select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        .menu {
            margin-top: 20px;
        }
        .menu a {
            display: block;
            padding: 10px;
            background-color: #007bff;
            color: white;
            text-decoration: none;
            text-align: center;
            margin-bottom: 10px;
            border-radius: 5px;
        }
        .menu a:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>

<div class="container" id="loginPage">
    <h1>Login</h1>
    <form id="loginForm">
        <div class="form-group">
            <label for="username">Username:</label>
            <input type="text" id="username" name="username" required>
        </div>
        <div class="form-group">
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>
        </div>
        <div class="form-group">
            <label for="role">Role:</label>
            <select id="role" name="role" required>
                <option value="student">Student</option>
                <option value="teacher">Teacher</option>
            </select>
        </div>
        <button type="button" onclick="login()">Login</button>
    </form>
</div>

<div class="container" id="profilePage" style="display: none;">
    <h1 id="profileTitle">Profile</h1>
    <div id="profileDetails">
        <img src="profile-placeholder.png" alt="Profile Photo" style="width: 100px; height: 100px; border-radius: 50%; margin-bottom: 10px;">
        <p><strong>Name:</strong> <span id="profileName"></span></p>
        <p><strong>Branch:</strong> <span id="profileBranch"></span></p>
        <p><strong>Admission Number:</strong> <span id="profileAdmission"></span></p>
        <p><strong>Batch:</strong> <span id="profileBatch"></span></p>
        <p><strong>Boarding Point:</strong> <span id="profileBoarding"></span></p>
        <p><strong>Bus Number:</strong> <span id="profileBus"></span></p>
    </div>
    <div class="menu">
        <a href="#" onclick="navigateTo('liveLocationPage')">Live Location</a>
        <a href="#" onclick="navigateTo('ticketBookingPage')">Ticket Booking</a>
        <a href="#" onclick="navigateTo('viewBookedTicketsPage')">View Booked Tickets</a>
        <a href="#" onclick="logout()">Logout</a>
    </div>
</div>

<!-- Live Location Page -->
<div class="container" id="liveLocationPage" style="display: none;">
    <h1>Live Location</h1>
    <p>Bus live location will appear here (placeholder).</p>
    <button onclick="navigateBack()">Back</button>
</div>

<!-- Ticket Booking Page -->
<div class="container" id="ticketBookingPage" style="display: none;">
    <h1>Ticket Booking</h1>
    <form>
        <label for="busRoute">Select Bus and Route:</label>
        <select id="busRoute">
            <option value="bus1">Bus 1 - Route A</option>
            <option value="bus2">Bus 2 - Route B</option>
            <option value="bus3">Bus 3 - Route C</option>
        </select>
        <button type="button" onclick="bookTicket()">Book Ticket</button>
    </form>
    <button onclick="navigateBack()">Back</button>
</div>

<!-- View Booked Tickets Page -->
<div class="container" id="viewBookedTicketsPage" style="display: none;">
    <h1>View Booked Tickets</h1>
    <p>Bus Name: <span id="bookedBus"></span></p>
    <p>Route: <span id="bookedRoute"></span></p>
    <p>Booking Date & Time: <span id="bookedTime"></span></p>
    <button onclick="navigateBack()">Back</button>
</div>

<script>
    const userDatabase = [
        { username: "student1", password: "pass123", role: "student", name: "John Doe", branch: "CSE", admission: "12345", batch: "2024", boarding: "Stop 1", bus: "Bus 1" },
        { username: "teacher1", password: "teach123", role: "teacher", name: "Jane Smith", branch: "ECE", admission: "T6789", batch: "2024", boarding: "N/A", bus: "N/A" }
    ];

    function login() {
        const username = document.getElementById('username').value;
        const password = document.getElementById('password').value;
        const role = document.getElementById('role').value;

        const user = userDatabase.find(u => u.username === username && u.password === password && u.role === role);

        if (user) {
            document.getElementById('loginPage').style.display = 'none';
            document.getElementById('profilePage').style.display = 'block';
            document.getElementById('profileTitle').innerText = `${role.charAt(0).toUpperCase() + role.slice(1)} Profile`;
            document.getElementById('profileName').innerText = user.name;
            document.getElementById('profileBranch').innerText = user.branch;
            document.getElementById('profileAdmission').innerText = user.admission;
            document.getElementById('profileBatch').innerText = user.batch;
            document.getElementById('profileBoarding').innerText = user.boarding;
            document.getElementById('profileBus').innerText = user.bus;
        } else {
            alert('Invalid credentials. Please try again.');
        }
    }

    function logout() {
        document.getElementById('profilePage').style.display = 'none';
        document.getElementById('loginPage').style.display = 'block';
        document.getElementById('loginForm').reset();
    }

    function navigateTo(pageId) {
        const pages = ['liveLocationPage', 'ticketBookingPage', 'viewBookedTicketsPage'];
        pages.forEach(page => {
            document.getElementById(page).style.display = 'none';
        });
        document.getElementById(pageId).style.display = 'block';
    }

    function navigateBack() {
        const pages = ['liveLocationPage', 'ticketBookingPage', 'viewBookedTicketsPage'];
        pages.forEach(page => {
            document.getElementById(page).style.display = 'none';
        });
        document.getElementById('profilePage').style.display = 'block';
    }

    function bookTicket() {
        const selectedRoute = document.getElementById('busRoute').value;
        document.getElementById('bookedBus').innerText = selectedRoute.split(' - ')[0];
        document.getElementById('bookedRoute').innerText = selectedRoute.split(' - ')[1];
        document.getElementById('bookedTime').innerText = new Date().toLocaleString();
        alert('Ticket booked successfully!');
        navigateTo('viewBookedTicketsPage');
    }
</script>

</body>
</html>
