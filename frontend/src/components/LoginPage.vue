<template>
    <div>
      <div id="main">
        <div>
          <h2>Login Page</h2>
          <button id="registerbtn" v-on:click="registerbtn">Register</button>
          <button id="loginbtn" v-on:click="loginbtn">Login</button>
          <div id="registerdiv">
            <form @submit.prevent="register" class="register">
              <div class="form-group">
                <label for="name">Name:</label><br />
                <input
                  type="text"
                  id="name"
                  placeholder="Enter Your Name"
                  v-model="name"
                  required
                /><br />
              </div>
              <div class="form-group">
                <label for="email">Email:</label><br />
                <input
                  type="email"
                  id="email"
                  placeholder="Enter Your Email"
                  v-model="email"
                  required
                /><br />
              </div>
              <div class="form-group">
                <label for="password">Password:</label><br />
                <input
                  type="text"
                  id="password"
                  placeholder="Enter Your Password"
                  v-model="password"
                  required
                /><br />
              </div>
              <button type="submit" class="submit-button">Register</button>
            </form>
          </div>
          <div id="logindiv">
            <form @submit.prevent="login" class="login">
              <div class="form-group">
                <label for="email">Email:</label><br />
                <input
                  type="email"
                  id="email"
                  placeholder="Enter Your Email"
                  v-model="email"
                  required
                /><br />
              </div>
              <div class="form-group">
                <label for="password">Password:</label><br />
                <input
                  type="text"
                  id="password"
                  placeholder="Enter Your Password"
                  v-model="password"
                  required
                /><br />
              </div>
              <button type="submit" class="submit-button">login</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </template>
  <script>
  export default {
    name: "LoginPage",
    data() {
      return {
        name: "",
        email: "",
        password: "",
      };
    },
    methods: {
      registerbtn() {
        console.log("register");
        document.getElementById("registerdiv").style.display = "block";
        document.getElementById("logindiv").style.display = "none";
      },
      loginbtn() {
        console.log("login");
        document.getElementById("registerdiv").style.display = "none";
        document.getElementById("logindiv").style.display = "block";
      },
      register() {
        fetch("http://localhost:5000/register", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            name: this.name,
            email: this.email,
            password: this.password,
          }),
        })
          .then((response) => response.json())
          .then((data) => {
            // Handle the response from the server
            console.log(data);
          })
          .catch((error) => {
            // Handle any errors that occur during the request
            console.error(error);
          });
      },
      login() {
        console.log(this.email, this.password);
        fetch("http://localhost:5000/login", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            email: this.email,
            password: this.password,
          }),
        })
          .then((response) => response.json())
          .then((data) => {
            // Handle the response from the server
            console.log(data);
            if (data.message === "Login successful") {
              // Login successful, redirect to the home page
              localStorage.setItem("name", data.name);
              localStorage.setItem("id", data.id);
              localStorage.setItem("token",data.token)
              window.location.reload();
              alert("login successfully");
  
              this.$router.push("/dishes");
            } else {
              // Login failed, display the error message
              const errorMessage = document.getElementById("error-message");
              errorMessage.textContent = data.message;
              alert(data.message);
            }
          })
          .catch((error) => {
            console.error("Error:", error);
          });
      },
    },
  };
  </script>
  <style>
   #logindiv {
    display: none;
  }

  #main {
    width: 30%;
    color: #333; /* Text color */
    background-color: #f0f2f5; /* Light gray background */
    margin: auto;
    height: auto;
    border-radius: 8px; /* Rounded corners */
    padding: 20px; /* Add some padding */
    box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.16); /* Add a box-shadow effect */
    opacity: 0;
    animation: fade-in 1s ease-in-out forwards;
  }

  @keyframes fade-in {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  #main > div {
    width: 70%;
    margin: auto;
    text-align: center;
  }

  form {
    width: 80%;
    margin: auto;
    box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.1); /* Add box-shadow to the form */
    padding: 20px; /* Add some padding to the form */
    border-radius: 8px; /* Rounded corners for the form */
    background-color: white; /* White background for the form */
  }

  button {
    background-color: #1877f2; /* Facebook blue color */
    color: white;
    transition: transform 0.3s ease-in-out;
    padding: 10px 20px; /* Add padding to the buttons */
    border: none;
    border-radius: 4px; /* Rounded corners for buttons */
  }

  button:hover {
    transform: scale(1.05); /* Slightly scale the button on hover */
  }

  input {
    margin-top: 10px;
    margin-bottom: 10px;
    width: 100%; /* Make the input fields occupy the full width */
    padding: 8px; /* Add some padding to the input fields */
    border: 1px solid #ccc; /* Add a border to the input fields */
    border-radius: 4px; /* Rounded corners for input fields */
  }
  </style>