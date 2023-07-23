<template>
  <div class="home-container">
    <!-- Hero Section -->
    <header class="hero">
      <h1 class="hero-title">Welcome to Parent-Influencer Podcasts</h1>
      <p class="hero-subtitle">
        Discover Engaging Content for Parents and Influencers
      </p>
      <button class="hero-cta-button">Get Started</button>
    </header>

    <!-- Services Section -->
    <section class="services">
      <div class="service-card">
        <i class="fa fa-microphone"></i>
        <h2 class="service-title">Podcast Creation</h2>
        <p class="service-description">
          Turn your ideas into captivating podcast episodes with our expert
          guidance.
        </p>
      </div>
      <div class="service-card">
        <i class="fa fa-headphones"></i>
        <h2 class="service-title">Podcast Listening</h2>
        <p class="service-description">
          Tune in to our wide range of podcasts covering various parenting and
          influencer topics.
        </p>
      </div>
    </section>

    <!-- Contact Form -->
    <section class="contact">
      <h2 class="contact-title">Contact Us</h2>
      <form class="contact-form">
        <input type="text" placeholder="Your Name" class="contact-input" />
        <input type="email" placeholder="Your Email" class="contact-input" />
        <textarea
          placeholder="Your Message"
          class="contact-textarea"
        ></textarea>
        <button class="contact-submit">Send Message</button>
      </form>
    </section>
  </div>
</template>

<style>
/* Reset default margin and padding */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.home-container {
  font-family: Arial, sans-serif;
  color: #333;
}

/* Hero Section Styles */
.hero {
  background-image: linear-gradient(to bottom, #4caf50, #45a049);
  text-align: center;
  padding: 100px 0;
  margin-top: -19px;
  color: #fff;
}

.hero-title {
  font-size: 48px;
  margin-bottom: 20px;
}

.hero-subtitle {
  font-size: 24px;
  margin-bottom: 40px;
}

.hero-cta-button {
  padding: 10px 20px;
  background-color: #fff;
  color: #4caf50;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.hero-cta-button:hover {
  background-color: #eee;
}

/* Services Section Styles */
.services {
  display: flex;
  justify-content: space-around;
  padding: 50px 0;
}

.service-card {
  background-color: yellow;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  text-align: center;
  border-radius: 4%;
  max-width: 300px;
  margin: 10px;
  padding: 10px;
}

.fa {
  font-size: 48px;
  margin-bottom: 20px;
}

.service-title {
  font-size: 24px;
  color: blueviolet;
  margin-bottom: 10px;
}

.service-description {
  color: crimson;
  line-height: 1.6;
}

/* Contact Form Styles */
.contact {
  text-align: center;
  background-color: #f0f0f0;
  padding: 50px 0;
}

.contact-title {
  font-size: 36px;
  margin-bottom: 30px;
}

.contact-form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.contact-input,
.contact-textarea {
  width: 300px;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.contact-submit {
  padding: 10px 20px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.contact-submit:hover {
  background-color: #45a049;
}
</style>
