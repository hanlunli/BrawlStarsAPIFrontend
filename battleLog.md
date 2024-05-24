---
comments: False
layout: default
title: battlelog
permalink: /battleLog
---

<script>
 const myHeaders = new Headers();
myHeaders.append("cache-control", "max-age=120");
myHeaders.append("content-type", "application/json; charset=utf-8");
myHeaders.append("Authorization", "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiIsImtpZCI6IjI4YTMxOGY3LTAwMDAtYTFlYi03ZmExLTJjNzQzM2M2Y2NhNSJ9.eyJpc3MiOiJzdXBlcmNlbGwiLCJhdWQiOiJzdXBlcmNlbGw6Z2FtZWFwaSIsImp0aSI6ImZhNWNiNjk0LTQxNTUtNDljOS1iNWUxLTk3ZDFlNjc2ZDVjNSIsImlhdCI6MTcxNjU4MjM3Miwic3ViIjoiZGV2ZWxvcGVyL2U4MzAxMjJjLTkzZTMtYjFmYi00NTQ4LTA1ZjI3ZDQ3YTZiMSIsInNjb3BlcyI6WyJicmF3bHN0YXJzIl0sImxpbWl0cyI6W3sidGllciI6ImRldmVsb3Blci9zaWx2ZXIiLCJ0eXBlIjoidGhyb3R0bGluZyJ9LHsiY2lkcnMiOlsiMTQ2LjcwLjE3NC42NyJdLCJ0eXBlIjoiY2xpZW50In1dfQ.yZzeG-mra89lXH-jX2Mt7Hz6RXtwun5muc3ol3BsWRvLGUW2CuPfV0lQS992mxYeYMUEU38Dpe08c4YGdCae3A");
myHeaders.append("Access-Control-Allow-Origin", "*")

const requestOptions = {
  method: "GET",
  headers: myHeaders,
  redirect: "follow"


};

fetch("https://api.brawlstars.com/v1/players/%238Q29VUJJP/battlelog", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
</script>
