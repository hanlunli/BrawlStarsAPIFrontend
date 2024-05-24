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
            myHeaders.append("Authorization", "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiIsImtpZCI6IjI4YTMxOGY3LTAwMDAtYTFlYi03ZmExLTJjNzQzM2M2Y2NhNSJ9.eyJpc3MiOiJzdXBlcmNlbGwiLCJhdWQiOiJzdXBlcmNlbGw6Z2FtZWFwaSIsImp0aSI6IjVhYjRjODQyLTNjZjQtNDRjNy05NjAzLTQ4Njk2MWJmYjkzNCIsImlhdCI6MTcxNjU3NDAxMSwic3ViIjoiZGV2ZWxvcGVyLzY1MjJjZGQ2LThhYzktMzRhOS1kMjhlLWNiZmIwM2JkMTExNyIsInNjb3BlcyI6WyJicmF3bHN0YXJzIl0sImxpbWl0cyI6W3sidGllciI6ImRldmVsb3Blci9zaWx2ZXIiLCJ0eXBlIjoidGhyb3R0bGluZyJ9LHsiY2lkcnMiOlsiMTA0LjIzMi4zNy4yMTMiXSwidHlwZSI6ImNsaWVudCJ9XX0.sgIo-pA--PIHC6VkCvTdLwGgBt3vEz3Y7htoUOLwqDKj6_zgI5Dt3tdkql0_32iV3zgX27skU4fVkihbTYgRAg");

            var requestOptions = {
                method: 'GET',
                headers: myHeaders,
                redirect: 'follow'
            };

            // Use a CORS proxy
            var corsProxy = 'https://cors-anywhere.herokuapp.com/';
            var apiUrl = "https://api.brawlstars.com/v1/players/%23JG2QC2R/battlelog";
            var url = corsProxy + apiUrl;

            fetch(url, requestOptions)
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Network response was not ok ' + response.statusText);
                    }
                    return response.json();
                })
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
