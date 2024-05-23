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
            const url = `https://api.brawlstars.com/v1/players/%23JG2QC2R/battlelog`;
            // Set up the headers (replace 'YOUR_ACCESS_TOKEN' with your actual token)
            const headers = {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiIsImtpZCI6IjI4YTMxOGY3LTAwMDAtYTFlYi03ZmExLTJjNzQzM2M2Y2NhNSJ9.eyJpc3MiOiJzdXBlcmNlbGwiLCJhdWQiOiJzdXBlcmNlbGw6Z2FtZWFwaSIsImp0aSI6IjRiNTEzMzlhLTM0NzQtNDYxOC05NzBiLWI5YTUyOThmOTJhOSIsImlhdCI6MTcxNjQ5NjgyOSwic3ViIjoiZGV2ZWxvcGVyLzY1MjJjZGQ2LThhYzktMzRhOS1kMjhlLWNiZmIwM2JkMTExNyIsInNjb3BlcyI6WyJicmF3bHN0YXJzIl0sImxpbWl0cyI6W3sidGllciI6ImRldmVsb3Blci9zaWx2ZXIiLCJ0eXBlIjoidGhyb3R0bGluZyJ9LHsiY2lkcnMiOlsiMTA0LjIzMi4zNy4yMTciXSwidHlwZSI6ImNsaWVudCJ9XX0.TrYhfmgQf7yPUQTBahM6xj3Q6y25gzBd14EYPI-Uoez8sT-qApJAAW6eMUF5DhVXZ36vTu8zXOBP6fiyCre0LA'
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
