<template>
  <div>
    <nav>
      <img src="@/assets/parentchat.png" alt="Logo" class="logo" />
      <router-link to="/" class="nav-link">Home</router-link>
      <router-link v-if="!name" to="/login" class="nav-link" id="login"
        >Login || Signup</router-link
      >
      <router-link v-else to="/" class="nav-link">{{ name }}</router-link>
      <router-link to="/chatbot" class="nav-link">Parent-chat</router-link>
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
      window.location.reload();
      
    },
  },
};
</script>

<style>
nav {
  margin-top: 4px;
  width: 100%;
  height: 70px;
  display: flex;

  background-color: #3b5998; /* Light gray background color */
  justify-content: space-evenly;
  margin-bottom: 20px;
  align-items: center; /* Center the nav items vertically */
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px; /* Add a box-shadow effect */
}

.nav-link {
  text-decoration: none;
  color: black; /* Text color */
  text-align: center;
  margin: 25px;
  padding: 30px;
  font-size: 20px;

  font-weight: 600;
  border-radius: 4%;
  background-color: #3b5998;
  padding: 10px; /* Add some padding around the nav items */
  transition: background-color 0.3s ease-in-out; /* Add a smooth background color transition */
}
.logo {
  height: 50px;
  width: 95px;
}

.nav-link:hover {
  background-color: #3b5998; /* Light gray background on hover */
  border-radius: 4px; /* Add rounded corners on hover */
  color: white;
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

nav {
  /* ... (existing styles) ... */
  background: linear-gradient(
    135deg,
    #3b5998,
    #28b485
  ); /* Apply the gradient background */
}

.nav-link {
  /* ... (existing styles) ... */
  background: linear-gradient(
    45deg,
    #7ed56f,
    #28b485
  ); /* Apply the gradient background to the nav items */
  /* ... (existing styles) ... */
  color: white;
}

.nav-link:hover {
  /* ... (existing styles) ... */
  background: linear-gradient(
    45deg,
    #1877f2,
    #7ed56f
  ); /* Apply the gradient background on hover */
  /* ... (existing styles) ... */
}

nav button {
  /* ... (existing styles) ... */
  background: linear-gradient(
    45deg,
    #1877f2,
    #3b5998
  ); /* Apply the gradient background to the logout button */
  /* ... (existing styles) ... */
}

nav button:hover {
  /* ... (existing styles) ... */
  background: linear-gradient(
    45deg,
    #3b5998,
    #1877f2
  ); /* Apply the gradient background on hover */
  /* ... (existing styles) ... */
}

/* Small screens (mobile phones) */
@media (max-width: 768px) {
  nav {
    flex-direction: column; /* Stack the nav items vertically */
    height: auto; /* Adjust the height to fit the content */
    box-shadow: none; /* Remove the box-shadow on small screens */
  }

  .nav-link {
    margin: 5px; /* Reduce the margin between nav items */
    padding: 5px; /* Reduce the padding around nav items */
    font-size: 16px; /* Decrease the font size for smaller screens */
  }
}

/* Medium screens (tablets and small laptops) */
@media (min-width: 769px) and (max-width: 1024px) {
  nav {
    justify-content: center; /* Center the nav items horizontally */
  }

  .nav-link {
    margin: 15px; /* Increase the margin between nav items */
    padding: 15px; /* Increase the padding around nav items */
    font-size: 18px; /* Increase the font size for medium screens */
  }
}

/* Large screens (desktops and larger laptops) */
@media (min-width: 1025px) {
  nav {
    justify-content: space-evenly; /* Revert to original justify-content */
    height: 70px; /* Revert to original height */
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px; /* Revert to original box-shadow */
  }

  .nav-link {
    font-size: 20px; /* Revert to original font size for large screens */
  }
}
</style>
