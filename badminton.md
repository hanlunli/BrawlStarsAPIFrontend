---
comments: False
layout: default
title: Badminton Predictor
permalink: /badminton
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Badminton</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px; /* Added padding */
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh; /* Changed height to min-height */
      background-image: url('cherryblossom.gif'); /* Replace 'cherryblossom.gif' with the path to your GIF file */
      background-repeat: no-repeat;
      background-attachment: fixed; /* This ensures that the background image doesn't scroll with the content */
      background-size: cover; 
    }
    .container {
      max-width: 600px;
      width: 100%;
      text-align: center;
      background-color: rgba(255, 255, 255, 0.8);
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    .form-group {
      margin-bottom: 20px;
      text-align: left;
    }
    label {
      display: block;
      margin-bottom: 5px;
    }
    input[type="number"],
    input[type="text"] {
      padding: 8px;
      border-radius: 5px;
      border: 1px solid #ccc;
      width: calc(100% - 18px);
    }
    button {
      padding: 8px;
      border-radius: 5px;
      border: 1px solid #ccc;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    button.selected {
      background-color: #007bff;
      color: #fff;
    }
    button:hover {
      background-color: #0056b3;
    }
  /* Modal styles */
/* Updated modal styles */
/* Updated modal styles with flexbox */
.modal {
    display: none; 
    position: fixed; 
    z-index: 1; 
    width: 45%; 
    height: 45%; 
    border-radius: 30px;
    overflow: auto; 
    background-color: rgba(0,0,0,0.9); /* Updated background color */
    color: white; /* Text color */
    justify-content: center; /* Center horizontally */
    align-items: center;
    font-size: 50px;
    top: 53%;
    left: 50%;
    transform: translate(-50%, -50%);
}
.modal-content {
    background-color: black; /* Updated modal background color */
    margin: 0; /* No margin */
    padding: 20px;
    border: 3px; /* No border */
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    text-align: center;
    display: flex;
    justify-content: center; /* Center horizontally */
    align-items: center;
}
/* Close button */
.close {
  color: white;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 20px; /* Adjust this value as needed */
}
.close:hover,
.close:focus {
    color: white; /* Close button hover/focus color */
    text-decoration: none;
    cursor: pointer;
}




</style>
</head>
<body>
    <div class="outlook">
      <label>Outlook:</label>
      <button id="outlook-yes" class="toggle-button" onclick="togglebutton('outlook')">unfavorable</button>
    </div>
    <div class="temperature">
      <label>Temperature:</label>
      <div id="temperature-buttons" class="button-group">
        <button id="temperature-yes" class="toggle-button" onclick="togglebutton('temperature')">unfavorable</button>
      </div>
    </div>
    <div class="humidity">
      <label>Humidity:</label>
      <div id="humidity-buttons" class="button-group">
        <button id="humidity-yes" class="toggle-button" onclick="togglebutton('humidity')">unfavorable</button>
      </div>
    </div>
    <div class="wind">
      <label>Wind:</label>
      <div id="wind-buttons" class="button-group">
        <button id="wind-yes" class="toggle-button" onclick="togglebutton('wind')">unfavorable</button>
      </div>
    </div>
    <button type="button" class = "search" onclick="submitForm()">Search</button>
  <div id="myModal" class="modal">
  <!-- Modal content -->
    <div class="modal-content">
      <span class="close" onclick="closeModal()">&times;</span>
      <p id="modalData">Variable Data Goes Here</p>
    </div>
  </div>
  <script>
    var outlook = false;temperature = false;humidity = false;wind = false;
    const toggleButtons = document.querySelectorAll('.toggle-button');
    toggleButtons.forEach(button => {
      button.addEventListener('click', function() {
        const siblingButton = this.id.includes('yes') ? this.nextElementSibling : this.previousElementSibling;
        this.classList.add('selected');
        siblingButton.classList.remove('selected');
      });
    });
    function togglebutton(buttonname) {
        if (buttonname === 'outlook') {
            outlook = !outlook;
            console.log(outlook)
            if (outlook == false) {
                document.getElementById("outlook-yes").innerText = "unfavorable"}
            else if (outlook == true) {
                document.getElementById("outlook-yes").innerText = "favorable"
            }
        } else if (buttonname === 'temperature') {
            temperature = !temperature;
            console.log(temperature)
            if (temperature == false) {
                document.getElementById("temperature-yes").innerText = "unfavorable"}
            else if (temperature == true) {
                document.getElementById("temperature-yes").innerText = "favorable"
            }
        } else if (buttonname === 'humidity') {
            humidity = !humidity;
            console.log(humidity)
            if (humidity == false) {
                document.getElementById("humidity-yes").innerText = "unfavorable"}
            else if (humidity == true) {
                document.getElementById("humidity-yes").innerText = "favorable"
            }
        } else if (buttonname === 'wind') {
            wind = !wind;
            console.log(wind)
            if (wind == false) {
                document.getElementById("wind-yes").innerText = "unfavorable"}
            else if (wind == true) {
                document.getElementById("wind-yes").innerText = "favorable"
            }
        }
    }
    function openModal(data) {
  var modal = document.getElementById("myModal");
  modal.style.display = "block";
    // Here you can set the variable data to be displayed in the modal
    if (data == 'yes') {
      var variableData = "good day to play badminton"
    }
    else {
      var variableData = "bad day to play badminton"
    }
    document.getElementById("modalData").innerText = variableData;
  }
  // Function to close the modal
  function closeModal() {
    var modal = document.getElementById("myModal");
    modal.style.display = "none";
  }
  // Close the modal when clicking outside of it
  window.onclick = function(event) {
    var modal = document.getElementById("myModal");
    if (event.target == modal) {
      modal.style.display = "none";
    }
  }
  closeModal()
    function submitForm() {
      const formData = {
        outlook: outlook === true ? 'yes' : 'no',
        temperature: temperature === true ? 'yes' : 'no',
        humidity: humidity === true ? 'yes' : 'no',
        wind: wind === true ? 'yes' : 'no'
      };
      const jsonOutput = JSON.stringify(formData);
      console.log(jsonOutput);
      fetch("http://127.0.0.1:8086/badminton/", {
      method: "POST",
      body: jsonOutput,
      headers: {
        "Content-type": "application/json; charset=UTF-8"
      }
      })
      .then(response => response.json())
      .then(data => {
            // Handle successful response here
            openModal(data);
            })
  console.log('OUR FRONTEND ACTUALLY WORKS????????????/')
      // You can do whatever you want with the JSON data here, for example, send it to a server.
    }
    
  </script>
</body>
</html>
