---
comments: False
layout: default
title: I am under the watha
---
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Water Potability Prediction</title>
<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: #f4f4f4;
    }
    .container {
        max-width: 500px;
        padding: 20px;
        background-color: #fff;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    h1 {
        text-align: center;
        margin-bottom: 20px;
    }
    label {
        display: block;
        margin-bottom: 5px;
        color: black;
    }
    input[type="number"] {
        width: 100%;
        padding: 8px;
        margin-bottom: 10px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
    }
    button {
        width: 100%;
        padding: 10px;
        background-color: #007bff;
        color: #fff;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }
</style>
</head>
<body>
<div class="container">
    <h1>Water Potability Prediction</h1>
    <form id="prediction-form">
        <label for="ph">pH:</label>
        <input type="number" id="ph" name="ph" step="0.01" required>
        <label for="Hardness">Hardness:</label>
        <input type="number" id="Hardness" name="Hardness" required>
        <label for="Solids">Solids:</label>
        <input type="number" id="Solids" name="Solids" required>
        <label for="Chloramines">Chloramines:</label>
        <input type="number" id="Chloramines" name="Chloramines" step="0.01" required>
        <label for="Sulfate">Sulfate:</label>
        <input type="number" id="Sulfate" name="Sulfate" step="0.01" required>
        <label for="Conductivity">Conductivity:</label>
        <input type="number" id="Conductivity" name="Conductivity" step="0.01" required>
        <label for="Organic_carbon">Organic Carbon:</label>
        <input type="number" id="Organic_carbon" name="Organic_carbon" step="0.01" required>
        <label for="Trihalomethanes">Trihalomethanes:</label>
        <input type="number" id="Trihalomethanes" name="Trihalomethanes" step="0.01" required>
        <label for="Turbidity">Turbidity:</label>
        <input type="number" id="Turbidity" name="Turbidity" step="0.01" required>
        <button type="submit">Predict</button>
    </form>
</div>

<script>
    document.getElementById("prediction-form").addEventListener("submit", async function(event) {
        event.preventDefault();
        console.log("Form submitted"); // Debugging log
        const formData = new FormData(event.target);
        const data = {};
        formData.forEach(function(value, key){
            console.log(data[key])
            data[key] = Number(value);
        });
        console.log("Data:", Number(data)); // Debugging log

        try {
            const response = await fetch('http://127.0.0.1:8086/water/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            });
            const result = await response.json();
            console.log("Result:", result); // Debugging log
            alert(`Prediction: Water is ${result.prediction}`); // Show an alert
        } catch (error) {
            console.error('Error:', error);
            alert('An error occurred. Please try again.'); // Show an alert in case of error
        }
    });
</script>

</body>
</html>
