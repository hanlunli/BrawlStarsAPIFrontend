<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Brawl Stars Player Log</title>
</head>
<body>
    <h1>Brawl Stars Player Log</h1>
    <!-- Button to trigger GET request -->
    <button onclick="sendGetRequest()">Get Battle Log</button>
    <!-- Display response -->
    <pre id="response-output"></pre>
    <script>
        function sendGetRequest() {
            var myHeaders = new Headers();
            myHeaders.append("Authorization", "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiIsImtpZCI6IjI4YTMxOGY3LTAwMDAtYTFlYi03ZmExLTJjNzQzM2M2Y2NhNSJ9.eyJpc3MiOiJzdXBlcmNlbGwiLCJhdWQiOiJzdXBlcmNlbGw6Z2FtZWFwaSIsImp0aSI6IjcxZGZhZjZmLTRkZWQtNDdiZi1iNWM4LTNlYTQyNGFkOWRlMSIsImlhdCI6MTcxNjU4MjAyOSwic3ViIjoiZGV2ZWxvcGVyLzY1MjJjZGQ2LThhYzktMzRhOS1kMjhlLWNiZmIwM2JkMTExNyIsInNjb3BlcyI6WyJicmF3bHN0YXJzIl0sImxpbWl0cyI6W3sidGllciI6ImRldmVsb3Blci9zaWx2ZXIiLCJ0eXBlIjoidGhyb3R0bGluZyJ9LHsiY2lkcnMiOlsiMTA0LjIzMi4zNy4xNjciXSwidHlwZSI6ImNsaWVudCJ9XX0.IlFf34rH0NPan-n8Txsveavm-7pSepP-CzmvFKde0kXAHRkE7YJ5FoqVAXYIBugVXfzFFGP_RbjsYmIE3LHrVw");
            var requestOptions = {
                method: 'GET',
                headers: myHeaders,
                redirect: 'follow'
            };
            fetch("https://api.brawlstars.com/v1/players/%23JG2QC2R/battlelog", requestOptions)
                .then(response => response.json())
                .then(result => {
                    // Display the response
                    document.getElementById('response-output').innerText = JSON.stringify(result, null, 2);
                })
                .catch(error => {
                    document.getElementById('response-output').innerText = `Error: ${error}`;
                });
        }
    </script>
</body>
</html>
