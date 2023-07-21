<!-- <template>
    <div>
        <h1>Home page</h1>
    </div>
</template>
<script>
export default {
    name:'HomePage'
}
</script> -->

<template>
    <div class="home-page">
      <!-- Header Section -->
      
  
      <!-- Hero Section -->
      <section class="hero">
        <!-- Image and text here -->
        <div class="hero-content">
          <h1>Welcome to FunChat</h1>
          <p>Connect and chat with friends in a fun way!</p>
          <button class="btn">Get Started</button>
        </div>
        <!-- <img src="@/assets/hero-image.png" alt="Hero Image" class="hero-image" /> -->
      </section>
  
      <!-- Features Section -->
      <section class="features">
        <!-- Features content here -->
        <div class="feature">
          <!-- <img src="@/assets/feature-icon-1.png" alt="Feature 1" /> -->
          <h3>Real-time Chat</h3>
          <p>Chat with friends in real-time and never miss a message.</p>
        </div>
        <div class="feature">
          <!-- <img src="@/assets/feature-icon-2.png" alt="Feature 2" /> -->
          <h3>Emoji Support</h3>
          <p>Express yourself with a wide range of emojis.</p>
        </div>
        <!-- Add more feature items as needed -->
      </section>
  
      <!-- Testimonials Section -->
      <section class="testimonials">
        <!-- Testimonials content here -->
        <div class="testimonial">
          <!-- <img src="@/assets/user-avatar-1.png" alt="User Avatar" /> -->
          <p>
            "FunChat is amazing! I love how easy it is to connect with my friends
            and have fun conversations."
          </p>
          <cite> - John Doe</cite>
        </div>
        <div class="testimonial">
          <!-- <img src="@/assets/user-avatar-2.png" alt="User Avatar" /> -->
          <p>
            "I've tried many chat apps, but FunChat is the best. The user
            experience is fantastic!"
          </p>
          <cite> - Jane Smith</cite>
        </div>
        <!-- Add more testimonial items as needed -->
      </section>
  
      <!-- Call-to-action Section -->
      <section class="cta">
        <!-- CTA content here -->
        <h2>Join FunChat Today!</h2>
        <p>Sign up now to start connecting with friends and have a blast!</p>
        <button class="btn">Sign Up</button>
      </section>
  
      <!-- Footer Section -->
      <footer class="footer">
        <!-- Footer content here -->
        <div class="footer-content">
          <!-- <img src="@/assets/logo.png" alt="Your Logo" class="footer-logo" /> -->
          <nav class="footer-navigation">
            <ul>
              <li><a href="#">Home</a></li>
              <li><a href="#">Features</a></li>
              <li><a href="#">Testimonials</a></li>
              <li><a href="#">Privacy Policy</a></li>
              <!-- Add more footer links as needed -->
            </ul>
          </nav>
        </div>
        <p class="footer-copyright">
          &copy; 2023 FunChat. All rights reserved.
        </p>
      </footer>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HomePage',
  };
  </script>
  
  <style>
  /* Add your CSS styles here to make it look attractive based on the design */
  /* Use CSS animations to add some beautiful animations */
  /* Ensure responsiveness for different screen sizes */
  
  /* Example CSS styles for the given code */
  .home-page {
    font-family: Arial, sans-serif;
  }
  
  /* Header Styles */
  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px;
  }
  
  .logo {
    width: 100px; /* Adjust the width as needed */
  }
  
  .navigation ul {
    list-style: none;
    display: flex;
  }
  
  .navigation li {
    margin-right: 20px;
  }
  
  .navigation a {
    text-decoration: none;
    color: #333;
  }
  
  /* Hero Styles */
  .hero {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 80px 40px;
    background-color: #f9f9f9;
  }
  
  .hero-content {
    max-width: 500px;
  }
  
  .hero h1 {
    font-size: 36px;
    margin-bottom: 20px;
  }
  
  .hero p {
    font-size: 18px;
    color: #666;
    margin-bottom: 30px;
  }
  
  .hero-image {
    max-width: 600px;
  }
  
  /* Features Styles */
  .features {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 80px 40px;
    background-color: #fff;
  }
  
  .feature {
    text-align: center;
    max-width: 250px;
  }
  
  .feature img {
    width: 60px;
    margin-bottom: 20px;
  }
  
  .feature h3 {
    font-size: 24px;
    margin-bottom: 10px;
  }
  
  .feature p {
    color: #666;
  }
  
  /* Testimonials Styles */
  .testimonials {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 80px 40px;
    background-color: #f9f9f9;
  }
  
  .testimonial {
    text-align: center;
    max-width: 250px;
  }
  
  .testimonial img {
    width: 80px;
    border-radius: 50%;
    margin-bottom: 20px;
  }
  
  .testimonial p {
    color: #666;
  }
  
  .testimonial cite {
    font-weight: bold;
  }
  
  /* CTA Styles */
  .cta {
    text-align: center;
    padding: 80px 40px;
    background-color: #fff;
  }
  
  .cta h2 {
    font-size: 32px;
    margin-bottom: 20px;
  }
  
  .cta p {
    color: #666;
    margin-bottom: 30px;
  }
  
  /* Footer Styles */
  .footer {
    background-color: #333;
    color: #fff;
    padding: 40px;
  }
  
  .footer-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  
  .footer-logo {
    width: 80px; /* Adjust the width as needed */
  }
  
  .footer-navigation ul {
    list-style: none;
    display: flex;
  }
  
  .footer-navigation li {
    margin-right: 20px;
  }
  
  .footer-navigation a {
    text-decoration: none;
    color: #fff;
  }
  
  .footer-copyright {
    text-align: center;
    margin-top: 20px;
  }
  </style>
  