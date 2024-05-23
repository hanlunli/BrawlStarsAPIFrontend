<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Brawl Stars Player Log</title>
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
</head>
<body>
    <h1>Brawl Stars Player Log</h1>
    <!-- Markdown input area -->
    <textarea id="markdown-input" rows="10" cols="30">
        Input your Player ID: `JG2QC2R`
    </textarea>
    <!-- Button to trigger POST request -->
    <button onclick="sendPostRequest()">Get Battle Log</button>
    <!-- Display response -->
    <pre id="response-output"></pre>
    <script>
        function sendPostRequest() {
            // Get the input value
            const markdownInput = document.getElementById('markdown-input').value;
            // Parse the player ID from the Markdown input
            const playerID = markdownInput.match(/`([^`]+)`/)[1];
            // Format the URL
            const url = `https://api.brawlstars.com/v1/players/%23${playerID}/battlelog`;
            // Set up the headers (replace 'YOUR_ACCESS_TOKEN' with your actual token)
            const headers = {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
            };
            // Send the POST request
            fetch(url, {
                method: 'POST',
                headers: headers
            })
            .then(response => response.json())
            .then(data => {
                // Display the response
                document.getElementById('response-output').innerText = JSON.stringify(data, null, 2);
            })
            .catch(error => {
                document.getElementById('response-output').innerText = `Error: ${error}`;
            });
        }
    </script>
</body>
</html>
