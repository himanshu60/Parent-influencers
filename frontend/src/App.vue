<template>
  <div>
    <nav>
      <img src="@/assets/parentchat.png" alt="Logo" class="logo" />
      <router-link to="/" class="nav-link">Home</router-link>
      <router-link v-if="!name" to="/login" class="nav-link" id="login"
          >Login || Signup</router-link
        >
        <router-link v-else to="/" class="nav-link">{{
          name
        }}</router-link>
      <router-link to="/chatbot" class="nav-link">chatbot</router-link>
      <button v-if="name" @click="logout">Logout</button>
    </nav>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      name: null, // Placeholder for the user name
    };
  },
  mounted() {
    // Check if the user name is available in the local storage
    const name = localStorage.getItem("name");
    if (name) {
      this.name = name;
    }
  },
  methods: {
    logout() {
      // Perform the logout action
      
      localStorage.clear();
      this.name = null;
    },
  },
};
</script>

<style>
/* body {
  background-image: url("@/assets/parentbackground.jpeg");
  
  background-size: cover;
  background-repeat: no-repeat;
 
} */
  nav {
    margin-top: -10px;
    width: 100%;
    height: 70px;
    display: flex;
    background-color: white; /* Light gray background color */
    justify-content: space-evenly;
    margin-bottom: 20px;
    align-items: center; /* Center the nav items vertically */
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px; /* Add a box-shadow effect */
  }

  .nav-link {
    text-decoration: none;
    color: black; /* Text color */
    text-align: center;
    font-size: 20px;
    font-weight: 600;
    padding: 10px; /* Add some padding around the nav items */
    transition: background-color 0.3s ease-in-out; /* Add a smooth background color transition */
  }

  .nav-link:hover {
    background-color: orangered; /* Light gray background on hover */
    border-radius: 4px; /* Add rounded corners on hover */
  }

  .nav-link.active {
    font-weight: bold; /* Make the active nav item bold */
  }

  nav button {
    background-color: #1877f2; /* Facebook blue color */
    color: white;
    border: none;
    border-radius: 4px;
    padding: 8px 16px; /* Add padding to the logout button */
    transition: transform 0.3s ease-in-out;
  }

  nav button:hover {
    transform: scale(1.05); /* Slightly scale the logout button on hover */
  }
</style>

