1pm made this <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Status Rotator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f4;
        }
        .container {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 400px;
            text-align: center;
        }
        h1 {
            margin-bottom: 20px;
        }
        button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #007bff;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #0056b3;
        }
        input {
            padding: 10px;
            width: 80%;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Discord Status Rotator</h1>
    <input type="text" id="tokenInput" placeholder="Enter your account token">
    <button onclick="startRotation()">Start Status Rotation</button>
    <button onclick="stopRotation()">Stop Status Rotation</button>
</div>

<script>
    let userToken = '';  // Token will be set from input
    const statuses = [
        "discord.gg/godsend",
        "YOU CANT STEP TOO ME LOLO🤡",
        "pussy dork🤡",
        "/mag",
        "when u die ima spit on your grave LMFAO🤡",
        "discord.gg/beefing",
      "i dont fw you pedo🤡",
      "child liker",
      "look at this cuck typing at 3.2wpm🤡",
      "we know your a unwanted slut",
      "come step dork🤡"
    ];
    let statusIndex = 0;
    let interval;

    function changeStatus(status) {
        const xhr = new XMLHttpRequest();
        xhr.open("PATCH", "https://discord.com/api/v9/users/@me/settings", true);
        xhr.setRequestHeader("Authorization", userToken);
        xhr.setRequestHeader("Content-Type", "application/json");

        xhr.onreadystatechange = function() {
            if (xhr.readyState === 4 && xhr.status === 200) {
                console.log(Status updated to: ${status});
            } else if (xhr.readyState === 4) {
                console.error("Failed to update status:", xhr.responseText);
            }
        };

        xhr.send(JSON.stringify({
            custom_status: {
                text: status
            }
        }));
    }

    function startRotation() {
        // Get the token from the input field
        userToken = document.getElementById("tokenInput").value;

        if (!userToken) {
            alert("add a token dumbass");
            return;
        }

        interval = setInterval(() => {
            changeStatus(statuses[statusIndex]);
            statusIndex = (statusIndex + 1) % statuses.length;  
        }, 6000);  // Change status every 6 seconds
    }

    function stopRotation() {
        clearInterval(interval);
        console.log("Status rotation stopped.");
    }
</script>

</body>
</html>
