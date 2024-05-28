---
layout: base
title: Leaderboard for game of life
permalink: /leaderboard
---

<!-- HTML table layout for page.  The table is filled by JavaScript below. 
-->

<html lang="en">
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Leaderboard</title>

<body>

<h1>Leaderboard for times played</h1>

<table>
  <thead>
  <tr>
    <th>ID</th>
    <th>Times Played</th>
  </tr>
  </thead>
  <tbody id="result">
    <!-- javascript generated data -->
  </tbody>
</table>


<script type="module">
  // uri variable and options object are obtained from config.js
  import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';

  // Set Users endpoint (list of users)
  const url = uri + '/api/users/';

  // prepare HTML result container for new output
  const resultContainer = document.getElementById("result");

  // fetch the API
  fetch(url, options)
    // response is a RESTful "promise" on any successful fetch
.then(response => {
    // check for response errors and display
    if (response.status !== 200) {
        if (response.status === 401) {
            // Unauthorized - Redirect to 401 error page
            window.location.href = "{{site.baseurl}}/login";

        } else if (response.status === 403) {
            // Forbidden - Redirect to 403 error page
            alert(response.status + " error. Redirecting you to the login")
            const errorMsg = 'Database response error: ' + response.status;
            console.log(errorMsg);
            const tr = document.createElement("tr");
            const td = document.createElement("td");
            td.innerHTML = errorMsg;
            tr.appendChild(td);
            resultContainer.appendChild(tr);
            window.location.href = "{{site.baseurl}}/login";
            return;
        }
    }
    // valid response will contain JSON data
    response.json().then(data => {
        console.log(data);

        // Sort data by timesplayed (highest to lowest)
        data.sort((a, b) => b.timesplayed - a.timesplayed);

        for (const row of data) {
            // tr and td build out for each row
            const tr = document.createElement("tr");
            const id = document.createElement("td");
            const timesplayed = document.createElement("td");
            // data is specific to the API
            id.innerHTML = row.uid; 
            timesplayed.innerHTML = row.timesplayed;
            // this builds td's into tr
            tr.appendChild(id);
            tr.appendChild(timesplayed);

            // append the row to table
            resultContainer.appendChild(tr);
        }
    });
})

  // catch fetch errors (ie ACCESS to server blocked)
  .catch(err => {
    console.error(err);
    const tr = document.createElement("tr");
    const td = document.createElement("td");
    td.innerHTML = err + ": " + url;
    tr.appendChild(td);
    resultContainer.appendChild(tr);
  });
</script>

