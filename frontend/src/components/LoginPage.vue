<template>
  <div>
    <div id="main">
      <div>
        <h2 class="title">Welcome to Parent-Influencer Podcasts</h2>
        <div class="buttons">
          <button @click="registerbtn" class="btn">Register</button>
          <button @click="loginbtn" class="btn">Login</button>
        </div>
        <div id="registerdiv" v-if="showRegister">
          <form @submit.prevent="register" class="form">
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
                type="password"
                id="password"
                placeholder="Enter Your Password"
                v-model="password"
                required
              /><br />
            </div>
            <button type="submit" class="submit-button">Register</button>
          </form>
        </div>
        <div id="logindiv" v-if="showLogin">
          <form @submit.prevent="login" class="form">
            <div class="form-group">
              <label for="loginEmail">Email:</label><br />
              <input
                type="email"
                id="loginEmail"
                placeholder="Enter Your Email"
                v-model="email"
                required
              /><br />
            </div>
            <div class="form-group">
              <label for="loginPassword">Password:</label><br />
              <input
                type="password"
                id="loginPassword"
                placeholder="Enter Your Password"
                v-model="password"
                required
              /><br />
            </div>
            <button type="submit" class="submit-button">Login</button>
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
      showRegister: true,
      showLogin: false,
    };
  },
  methods: {
    registerbtn() {
      this.showRegister = true;
      this.showLogin = false;
    },
    loginbtn() {
      this.showRegister = false;
      this.showLogin = true;
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

          alert("Registered Sucessfully");

          console.log(data);
        })
        .catch((error) => {
          // Handle any errors that occur during the request
          console.error(error);
        });
    },
    login() {
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
            localStorage.setItem("token", data.token);
            window.location.reload();
            alert("Login successfully");

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
/* body {
  background-image: url(@/assets/k.jpg);
} */
#main {
  /* ... (existing styles) ... */
  /* Add gradient background to the main container */
  background: linear-gradient(135deg, #f0f2f5, #d1d8e3);
}

/* Apply gradient background to the buttons */
.btn {
  /* ... (existing styles) ... */
  background: linear-gradient(45deg, #1877f2, #3b5998);
}

/* Apply gradient background to the submit button */
.submit-button {
  /* ... (existing styles) ... */
  background: linear-gradient(45deg, #1877f2, #3b5998);
}
#main {
  width: 30%;
  color: #333;
  background-color: #f0f2f5;
  margin: auto;
  height: auto;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.16);
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

.title {
  font-size: 28px;
  margin-bottom: 20px;
}

.buttons {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.btn {
  background-color: #1877f2;
  color: white;
  transition: transform 0.3s ease-in-out;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  margin: 0 5px;
}

.btn:hover {
  transform: scale(1.05);
}

.form {
  width: 100%;
  margin: auto;
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
  border-radius: 8px;
  background-color: white;
}

.submit-button {
  background-color: #1877f2;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 15px;
}

.submit-button:hover {
  background-color: #1566c9;
}

input {
  margin-top: 10px;
  margin-bottom: 10px;
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
