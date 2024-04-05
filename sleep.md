<!DOCTYPE html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Submit Sleep Data</title>
</head>
<body>
    <h2>Enter Sleep Data</h2>
    <form id="sleepForm">
        <label for="sleep_duration">Sleep Duration:</label>
        <input type="number" step="0.1" id="sleep_duration" name="sleep_duration" required><br>

        <label for="quality_of_sleep">Quality of Sleep:</label>
        <input type="number" id="quality_of_sleep" name="quality_of_sleep" required><br>

        <label for="physical_activity_level">Physical Activity Level:</label>
        <input type="number" id="physical_activity_level" name="physical_activity_level" required><br>

        <label for="stress_level">Stress Level:</label>
        <input type="number" id="stress_level" name="stress_level" required><br>

        <label for="bmi_category">BMI Category:</label>
        <input type="number" id="bmi_category" name="bmi_category" required><br>

        <label for="blood_pressure">Blood Pressure:</label>
        <input type="number" id="blood_pressure" name="blood_pressure" required><br>

        <label for="heart_rate">Heart Rate:</label>
        <input type="number" id="heart_rate" name="heart_rate" required><br>

        <label for="daily_steps">Daily Steps:</label>
        <input type="number" id="daily_steps" name="daily_steps" required><br>

        <button type="submit">Submit Data</button>
    </form>

    <script>
        document.getElementById('sleepForm').addEventListener('submit', function(event) {
            event.preventDefault();

            const formData = {
                sleep_duration: parseFloat(document.getElementById('sleep_duration').value),
                quality_of_sleep: parseInt(document.getElementById('quality_of_sleep').value),
                physical_activity_level: parseInt(document.getElementById('physical_activity_level').value),
                stress_level: parseInt(document.getElementById('stress_level').value),
                bmi_category: parseInt(document.getElementById('bmi_category').value),
                blood_pressure: parseInt(document.getElementById('blood_pressure').value),
                heart_rate: parseInt(document.getElementById('heart_rate').value),
                daily_steps: parseInt(document.getElementById('daily_steps').value)
            };

            fetch("http://127.0.0.1:8086/sleep/", {
                method: "POST",
                body: JSON.stringify(formData),
                headers: {
                    "Content-type": "application/json; charset=UTF-8"
                }
            })
            .then(response => {
                if (!response.ok) {
                    throw new Error('Failed to submit data');
                }
                return response.json();
            })
            .then(data => {
                // Handle successful response here
                console.log('Data submitted successfully:', data);
                // Display popup with data
                alert('Data received from backend:\n' + JSON.stringify(data));
                // You can perform further actions here, such as displaying a success message or redirecting the user.
            })
            .catch(error => {
                console.error('Error submitting data:', error.message);
                // You can handle errors here, such as displaying an error message to the user.
            });
        });
    </script>
</body>
</html>
