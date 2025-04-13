# Tracking.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cozy Study Leaderboard</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f8f0e3;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        h1 {
            text-align: center;
            color: #f28a8c;
            font-size: 3em;
        }
        .leaderboard {
            max-width: 800px;
            margin: auto;
            background: #fff;
            border-radius: 12px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            padding: 20px;
        }
        .leaderboard h2 {
            text-align: center;
            color: #f28a8c;
            font-size: 2em;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        table th, table td {
            padding: 10px;
            text-align: center;
        }
        table th {
            background-color: #f28a8c;
            color: #fff;
        }
        table tr:nth-child(even) {
            background-color: #f1e3e3;
        }
        .input-section {
            display: flex;
            justify-content: center;
            margin: 20px 0;
        }
        .input-section input {
            padding: 10px;
            font-size: 1.2em;
            margin-right: 10px;
            border-radius: 8px;
            border: 1px solid #ccc;
        }
        .input-section button {
            padding: 10px 20px;
            font-size: 1.2em;
            background-color: #f28a8c;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
        }
        .input-section button:hover {
            background-color: #e0797f;
        }
        .leaderboard-item {
            display: flex;
            justify-content: space-between;
        }
    </style>
</head>
<body>

<h1>Cozy Study Leaderboard</h1>

<div class="leaderboard">
    <h2>Leaderboard</h2>
    <table id="leaderboard">
        <thead>
            <tr>
                <th>Name</th>
                <th>Daily Hours</th>
                <th>Weekly Hours</th>
            </tr>
        </thead>
        <tbody>
            <!-- Leaderboard Entries Will Go Here -->
        </tbody>
    </table>

    <div class="input-section">
        <input type="text" id="nameInput" placeholder="Enter your name">
        <input type="number" id="studyHoursInput" placeholder="Enter study hours" min="0">
        <button onclick="addStudyLog()">Log Study Hours</button>
    </div>
</div>

<script>
    const leaderboard = [];

    function updateLeaderboard() {
        const tbody = document.querySelector("#leaderboard tbody");
        tbody.innerHTML = "";

        leaderboard.sort((a, b) => b.weeklyHours - a.weeklyHours); // Sort by weekly hours, descending

        leaderboard.forEach(entry => {
            const row = document.createElement("tr");
            row.innerHTML = `
                <td>${entry.name}</td>
                <td>${entry.dailyHours}</td>
                <td>${entry.weeklyHours}</td>
            `;
            tbody.appendChild(row);
        });
    }

    function addStudyLog() {
        const name = document.querySelector("#nameInput").value.trim();
        const studyHours = parseInt(document.querySelector("#studyHoursInput").value.trim());

        if (name && !isNaN(studyHours)) {
            const existingEntry = leaderboard.find(entry => entry.name === name);
            if (existingEntry) {
                existingEntry.dailyHours += studyHours;
                existingEntry.weeklyHours += studyHours;
            } else {
                leaderboard.push({
                    name: name,
                    dailyHours: studyHours,
                    weeklyHours: studyHours,
                });
            }

            document.querySelector("#nameInput").value = "";
            document.querySelector("#studyHoursInput").value = "";
            updateLeaderboard();
        } else {
            alert("Please enter valid data.");
        }
    }
</script>

</body>
</html>
