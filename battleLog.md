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
myHeaders.append("Authorization", "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiIsImtpZCI6IjI4YTMxOGY3LTAwMDAtYTFlYi03ZmExLTJjNzQzM2M2Y2NhNSJ9.eyJpc3MiOiJzdXBlcmNlbGwiLCJhdWQiOiJzdXBlcmNlbGw6Z2FtZWFwaSIsImp0aSI6ImEyYWJmMTg1LWYzM2MtNDA2OC05MWQzLWFiMDI0Y2YwOTQyNSIsImlhdCI6MTcxNjU3MzQyOCwic3ViIjoiZGV2ZWxvcGVyL2U4MzAxMjJjLTkzZTMtYjFmYi00NTQ4LTA1ZjI3ZDQ3YTZiMSIsInNjb3BlcyI6WyJicmF3bHN0YXJzIl0sImxpbWl0cyI6W3sidGllciI6ImRldmVsb3Blci9zaWx2ZXIiLCJ0eXBlIjoidGhyb3R0bGluZyJ9LHsiY2lkcnMiOlsiMTg1LjE3Ny4xMjQuMjI1Il0sInR5cGUiOiJjbGllbnQifV19.feZESUVfaDrpbkt7YUcfoJFovSViDAUqciDqAtmtZ9zzz6xqTdH8GkNvVipB8j6Uc-x-lpPcpmlkkWtBy7zQEA");

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
