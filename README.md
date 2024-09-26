<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Questionnaire</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(to right, #74ebd5, #9face6);
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #333;
        }
        .container {
            max-width: 600px;
            width: 100%;
            background-color: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        label {
            display: block;
            margin-top: 15px;
            margin-bottom: 5px;
            color: #555;
        }
        input[type="text"], input[type="password"], select {
            width: 100%;
            padding: 12px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
            transition: border-color 0.3s;
        }
        input[type="text"]:focus, input[type="password"]:focus {
            border-color: #28a745;
            outline: none;
        }
        button {
            padding: 12px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #218838;
        }
        #admin-section {
            margin-top: 20px;
            display: none; /* Hidden until answers are submitted */
        }
        #admin-results {
            display: none; /* Hidden until password is verified */
            margin-top: 20px;
        }
        .response {
            border: 1px solid #ddd;
            border-radius: 5px;
            padding: 15px;
            margin: 10px 0;
            background-color: #f9f9f9;
        }
        hr {
            border: 1px solid #eee;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Answer the Questions</h1>
    
    <label for="discordNickname">Enter your Discord nickname:</label>
    <input type="text" id="discordNickname" placeholder="Your Discord Nickname" required>

    <label for="question1">1. What do you think about Butters?</label>
    <input type="text" id="question1" placeholder="Your opinion about Butters" required>

    <label for="question2">2. If you see Butters in person, what would you do?</label>
    <input type="text" id="question2" placeholder="What would you do?" required>

    <label for="question3">3. Do you think Butters is a good man?</label>
    <select id="question3">
        <option value="yes">Yes</option>
        <option value="no">No</option>
    </select>

    <button onclick="submitAnswers()">Submit</button>

    <div id="results" style="display: none; margin-top: 20px;">
        <h2>Thank you for answering all the questions!</h2>
        <p><strong>Discord Nickname:</strong> <span id="resultDiscord"></span></p>
        <p><strong>Your opinion about Butters:</strong> <span id="resultQ1"></span></p>
        <p><strong>What you'd do if you saw Butters:</strong> <span id="resultQ2"></span></p>
        <p><strong>Is Butters a good man?</strong> <span id="resultQ3"></span></p>
    </div>

    <div id="admin-section">
        <h2>Admin Access</h2>
        <label for="adminPassword">Enter password:</label>
        <input type="password" id="adminPassword" placeholder="Enter admin password">
        <button onclick="viewResponses()">View Responses</button>
        <div id="admin-results"></div>
    </div>
</div>

<script>
    const responses = []; // Array to store responses

    function submitAnswers() {
        // Get input values
        const discordNickname = document.getElementById('discordNickname').value;
        const question1 = document.getElementById('question1').value;
        const question2 = document.getElementById('question2').value;
        const question3 = document.getElementById('question3').value;

        // Store responses
        responses.push({
            nickname: discordNickname,
            opinion: question1,
            action: question2,
            goodMan: question3
        });

        // Display results
        document.getElementById('resultDiscord').innerText = discordNickname;
        document.getElementById('resultQ1').innerText = question1;
        document.getElementById('resultQ2').innerText = question2;
        document.getElementById('resultQ3').innerText = question3;

        document.getElementById('results').style.display = 'block';
        document.getElementById('admin-section').style.display = 'block'; // Show admin section

        // Clear input fields
        document.getElementById('discordNickname').value = '';
        document.getElementById('question1').value = '';
        document.getElementById('question2').value = '';
        document.getElementById('question3').selectedIndex = 0;
    }

    function viewResponses() {
        const adminPassword = document.getElementById('adminPassword').value;
        if (adminPassword === '6969') {
            const adminResults = document.getElementById('admin-results');
            adminResults.innerHTML = ''; // Clear previous results

            // Display all responses
            responses.forEach((response, index) => {
                const responseDiv = document.createElement('div');
                responseDiv.className = 'response'; // Add class for styling
                responseDiv.innerHTML = `
                    <strong>Response ${index + 1}:</strong><br>
                    <strong>Discord Nickname:</strong> ${response.nickname}<br>
                    <strong>Your opinion about Butters:</strong> ${response.opinion}<br>
                    <strong>What they'd do if they saw Butters:</strong> ${response.action}<br>
                    <strong>Is Butters a good man?</strong> ${response.goodMan}<br>
                    <hr>
                `;
                adminResults.appendChild(responseDiv);
            });
            adminResults.style.display = 'block'; // Show the results
        } else {
            alert('Incorrect password!');
        }
    }
</script>

</body>
</html>
