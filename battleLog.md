---
comments: False
layout: default
title: battlelog
permalink: /battleLog
---

<script>
    var API_KEY = "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiIsImtpZCI6IjI4YTMxOGY3LTAwMDAtYTFlYi03ZmExLTJjNzQzM2M2Y2NhNSJ9.eyJpc3MiOiJzdXBlcmNlbGwiLCJhdWQiOiJzdXBlcmNlbGw6Z2FtZWFwaSIsImp0aSI6ImM3ZDBhOTkwLTBkZjgtNGExYi1iYzVjLTNhZjc1MzhiZmYxNyIsImlhdCI6MTcxNjQ5NDY4OCwic3ViIjoiZGV2ZWxvcGVyL2U4MzAxMjJjLTkzZTMtYjFmYi00NTQ4LTA1ZjI3ZDQ3YTZiMSIsInNjb3BlcyI6WyJicmF3bHN0YXJzIl0sImxpbWl0cyI6W3sidGllciI6ImRldmVsb3Blci9zaWx2ZXIiLCJ0eXBlIjoidGhyb3R0bGluZyJ9LHsiY2lkcnMiOlsiMTQzLjI0NC40NC4xNzUiXSwidHlwZSI6ImNsaWVudCJ9XX0.sUOHy8Nj33_NVE2MCZia9VofXMC8uGOHP2o1gIn1AX4UM3ZTaNMJp8hhWwM8wzVcpg4CdTA4t8RGDfkpK_M93g"
        try {
            fetch('https://api.brawlstars.com/v1/players/%238Q29VUJJP/battlelog', {
                method: 'GET', 
                headers: {
                    'Content-Type': 'application/json; charset=utf-8',
                    'Authorization':'Bearer ' + API_KEY,
                    'cache-control': 'max-age=120'
                }
            });
            response.json().then(data => {
                let x = false;
                for (const row of data) {
                    console.log(data)
                    }
                })
            const result = response.json();
            console.log(response)
            console.log("Result:", result); // Debugging log
            alert(`Prediction: Water is ${result.prediction}`); // Show an alert
        } catch (error) {
            console.error('Error:', error);
            alert('An error occurred. Please try again.'); // Show an alert in case of error
        }
</script>

</body>
</html>
