---
layout: base
title: Course Outlines
permalink: /login
---


<div class="container">
    <form id="username" action="javascript:login_user()">
        <p>
        </p>
        <!-- <p>
        <label>
            Name:
            <input class="userInput" type="text" name="name" id="name" required>
        </label>
        </p> -->
        <p><label>
            User ID:
            <input class="userInput" type="text" name="uid" id="uid" required>
        </label></p>
        <p ><label>
            Password:
            <input class="userInput" type="password" name="password" id="password" required>
        </label></p>
        <!-- <p><label>
            Date of Birth:
            <input class="userInput" type="text" id="dob" required>
        </label></p> -->
        <p>
            <button>Login</button>
        </p>
        <a href='{{site.baseurl}}/register'>Register</a>
    </form>
</div>

<script>

    // uri variable and options object are obtained from config.js
    const uri = "https://brawlstarsapibackend.stu.nighthawkcodingsociety.com";
    const options = {
        method: 'GET', // *GET, POST, PUT, DELETE, etc.
        mode: 'cors', // no-cors, *cors, same-origin
        cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
        credentials: 'include', // include, same-origin, omit
        headers: {
            'Content-Type': 'application/json',
        },
    };
    function login_user(){
        // Set Authenticate endpoint
        
        const url = uri + '/api/users/authenticate';

        // Set the body of the request to include login data from the DOM
        const body = {
            // name: document.getElementById("name").value,
            uid: document.getElementById("uid").value,
            password: document.getElementById("password").value,
            // dob: document.getElementById("dob").value
        };
        localStorage.setItem("uid",document.getElementById("uid").value);
        // Change options according to Authentication requirements
        const authOptions = {
            ...options, // This will copy all properties from options
            method: 'POST', // Override the method property
            cache: 'no-cache', // Set the cache property
            body: JSON.stringify(body),
            headers: {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': 'include'
    },
        };

        // Fetch JWT
        fetch(url, authOptions)
        .then(response => {
            // handle error response from Web API
            if (!response.ok) {
                if (response.status === 401) {
                    // Unauthorized - Redirect to 401 error page
                    window.location.href = "{{site.baseurl}}/401.html";
                } 
                else if (response.status === 400) {
                    // Forbidden - Redirect to 403 error page
                    window.location.href = "{{site.baseurl}}/400.html";
                } else if (response.status === 403) {
                    // Forbidden - Redirect to 403 error page
                    window.location.href = "{{site.baseurl}}/403.html";
                } else if (response.status === 400) {
                    // Forbidden - Redirect to 400 error page
                    window.location.href = "{{site.baseurl}}/400.html";
                } else if (response.status === 404) {
                    // Not Found - Redirect to 404 error page
                    window.location.href = "{{site.baseurl}}/404.html";
                } else {
                    // Handle other error responses
                    const errorMsg = 'Login error: ' + response.status;
                    console.log(errorMsg);
                }
                return;
            }
            // Success!!!
            // Redirect to the database page
            window.location.href = "{{site.baseurl}}/gameoflife";
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .catch(err => {
            console.error(err);
        });
    }
    // Attach login_user to the window object, allowing access to form action
    window.login_user = login_user;

