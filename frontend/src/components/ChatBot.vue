<template>
  <div class="chatbot-container">
    <div class="chatbot-chat">
      <div class="chatbot-header">
        <h1>
          <span class="parent">Parent</span>-
          <span class="chat">Chat</span>
        </h1>
        <button v-if="isUserLoggedIn" @click="clearMessages">New-Chat</button>
      </div>
      <div class="chatbot-body" ref="chatBody">
        <div
          v-for="message in messages"
          :key="message.id"
          class="chat-message"
          :class="{
            'user-message': message.fromUser,
            'bot-message': !message.fromUser,
          }"
          ref="messageRef"
        >
          <span class="message-text">{{ message.text }}</span>
        </div>
      </div>
      <div class="chat-input">
        <input
          v-model="newMessage"
          type="text"
          placeholder="Type your message here..."
        />
        <button @click="sendMessage">Send</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChatBot",
  data() {
    return {
      messages: [
        { id: 1, text: "Hello! \n How can I help you?", fromUser: false },
      ],
      newMessage: "",
    };
  },
  computed: {
    isUserLoggedIn() {
      // Check if the user is present in the localStorage
      const user = localStorage.getItem("id");
      return !!user; // Convert the user value to a boolean (true if user is present, false otherwise)
    },
  },
  mounted() {
    // Fetch the data when the component is mounted
    this.fetchData();
  },
  methods: {
    clearMessages() {
      let token = localStorage.getItem("token");
      let id = localStorage.getItem("id");

      if (token) {
        fetch(`http://localhost:5000/clearchat/${id}`, {
          method: "DELETE",
          headers: {
            "Content-Type": "application/json",
            Authorization: `${token}`,
          },
        })
          .then((response) => response.json())
          .then((data) => {
            // Handle the response from the server
            console.log(data.response);

            // Clear the messages in the frontend
            this.messages = [];
            window.location.reload();
            // Reset the newMessage input field
            this.newMessage = "";
          })
          .catch((error) => {
            // Handle any errors that occur during the request
            console.error(error);
          });
      } else {
        alert("You have to login first");
        this.newMessage = "";
      }
    },
    fetchData() {
      let token = localStorage.getItem("token");
      let id = localStorage.getItem("id");
      fetch(`http://localhost:5000/parent/${id}`, {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Authorization: `${token}`,
        },
      })
        .then((response) => response.json())
        .then((data) => {
          // Handle the response from the server
          console.log(data.response);
          let res = data.response;
          for (let i = 0; i < res.length; i++) {
            this.messages.push({
              id: this.messages.length + 1,
              text: res[i].text,
              fromUser: res[i].fromuser,
            });
          }

          this.newMessage = "";
        })
        .catch((error) => {
          // Handle any errors that occur during the request
          console.error(error);
        });
      // Your logic for sending the message to the Chatbot and receiving the response can be added here
      // For simplicity, we're just adding the user's message to the chat here
      this.newMessage = "";
    },
    newChat() {
      // Start a new chat
      this.currentChat = { id: Date.now(), messages: [] };
    },
    selectChat(chatId) {
      // Load the selected chat
      // For simplicity, we're using a static chat here
      this.currentChat = {
        id: chatId,
        messages: [{ id: 1, text: "Hello!", fromUser: false }],
      };
    },
    sendMessage() {
      let token = localStorage.getItem("token");
      let id = localStorage.getItem("id");

      if (token) {
        if (this.newMessage.trim() !== "") {
          this.messages.push({
            id: this.messages.length + 1,
            text: this.newMessage,
            fromUser: true,
          });
          this.$nextTick(() => {
            const messages = this.$refs.messageRef;
            const lastMessage = messages[messages.length - 1];
            lastMessage.scrollIntoView();
          });

          fetch(`http://localhost:5000/parent/${id}`, {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
              Authorization: `${token}`,
            },
            body: JSON.stringify({
              keyword: this.newMessage,
            }),
          })
            .then((response) => response.json())
            .then((data) => {
              // Handle the response from the server
              console.log(data.response);
              let res = data.response;
              this.messages.push({
                id: this.messages.length + 1,
                text: res[res.length - 1].text,
                fromUser: res[res.length - 1].fromuser,
              });
              this.newMessage = "";
            })
            .catch((error) => {
              // Handle any errors that occur during the request
              console.error(error);
            });
          // Your logic for sending the message to the Chatbot and receiving the response can be added here
          // For simplicity, we're just adding the user's message to the chat here
          this.newMessage = "";
        }
      } else {
        alert("You have to login first");
        this.newMessage = "";
      }
    },
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
/* Apply background gradient to the chatbot container */
.chatbot-container {
  /* ... (existing styles) ... */
  /* Add gradient background */
  background: linear-gradient(135deg, #f0f2f5, #d1d8e3);
}

/* Apply background gradient to the chatbot chat area */
.chatbot-chat {
  /* ... (existing styles) ... */
  /* Add gradient background */
  background: linear-gradient(135deg, #f0f2f5, #d1d8e3);
}

/* Apply background gradient to the chat input area */
.chat-input {
  /* ... (existing styles) ... */
  /* Add gradient background */
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

h1 {
  font-size: 24px;
  font-weight: bold;
  text-align: center;
}

/* Style for the "Parent" word */
span.parent {
  color: white; /* Orange color for "Parent" */
}

/* Style for the "Chat" word */
span.chat {
  color: red; /* Dodger blue color for "Chat" */
}

.chatbot-container {
  /* Add styles to make it take up 50% of the body screen and center it */
  display: flex;
  justify-content: center; /* Center horizontally */
  align-items: center; /* Center vertically */
  height: 50%; /* 50% of the viewport height */
  width: 50%;
  margin: auto;
}

.chat-summary {
  padding: 10px;
  border-bottom: 1px solid #ccc;
  cursor: pointer;
  transition: background-color 0.3s ease; /* Add smooth background color transition */
}

.chat-summary:last-child {
  border-bottom: none;
}

.chat-summary p {
  margin: 0;
}

.chat-summary:hover {
  background-color: #dcdcdc; /* Light gray background on hover */
  border-radius: 4px; /* Add rounded corners on hover */
}

.chats-list button {
  margin-top: 10px;
  padding: 5px 10px;
  background-color: blue; /* Set button background color */
  color: #fff; /* Set button text color */
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: transform 0.3s ease; /* Add scale effect on hover */
}

.chats-list button:hover {
  transform: scale(1.05); /* Slightly scale the button on hover */
}

.chatbot-chat {
  flex: 3;
  display: flex;
  flex-direction: column;
  border: 1px solid #cccccc;
  border-radius: 5px;
  margin: 10px;
  height: 78vh;
  overflow-y: scroll;
  margin-bottom: 45px;
  animation: fadeInRight 0.5s ease;
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.chatbot-header {
  box-shadow: rgba(0, 0, 0, 0.17) 0px -23px 25px 0px inset,
    rgba(0, 0, 0, 0.15) 0px -36px 30px 0px inset,
    rgba(0, 0, 0, 0.1) 0px -79px 40px 0px inset, rgba(0, 0, 0, 0.06) 0px 2px 1px,
    rgba(0, 0, 0, 0.09) 0px 4px 2px, rgba(0, 0, 0, 0.09) 0px 8px 4px,
    rgba(0, 0, 0, 0.09) 0px 16px 8px, rgba(0, 0, 0, 0.09) 0px 32px 16px;
  background-color: rgba(0, 0, 0, 0.491);
  color: #fff;
  padding: 10px;
  display: flex;
  justify-content: center;
}

.chatbot-body {
  flex: 1;
  overflow-y: scroll;
  background-image: url("https://cdn.dribbble.com/users/2058540/screenshots/8225138/media/af6d6d059328c6f2f9f6e7878c094c7e.gif");
  background-repeat: no-repeat;
  background-position: center;
  padding: 10px;
  display: flex;
  flex-direction: column;
}

.chat-message {
  margin-bottom: 5px;
  padding: 5px 10px;
  border-radius: 10px;
  max-width: 76%;
}

.user-message {
  background-color: #a92828;
  align-self: flex-end; /* Align user messages to the right side */
  color: #fffbfb; /* Set text color for user messages */

  /* New styles */
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  padding: 8px 12px;
}

.chat-input {
  /* Existing styles */
  display: flex;
  margin: auto;

  align-items: center;
  border-top: 1px solid #ccc;
  padding: 10px;
  position: fixed;
  bottom: 0;
  width: 49%;
  background-color: #f1f1f1;
  z-index: 1;

  /* New styles */
  border-radius: 20px;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}

/* Button hover effect */
.chat-input button {
  /* Existing styles */
  padding: 10px 15px;
  border: none;
  border-radius: 20px;
  background-color: blue;
  color: #fff;
  cursor: pointer;
  transition: transform 0.3s ease; /* Add scale effect on hover */

  /* New styles */
  box-shadow: rgba(0, 0, 0, 0.25) 0px 2px 4px;
}

/* Animation for container background fading */
@keyframes fadeInBackground {
  from {
    opacity: 0.5;
  }
  to {
    opacity: 1;
  }
}

/* Hover effect for chat summary */
.chat-summary:hover {
  background-color: #dcdcdc;
  border-radius: 10px;
  transform: scale(1.02); /* Slightly scale the chat summary on hover */
  box-shadow: rgba(0, 0, 0, 0.1) 0px 2px 4px; /* Add a subtle shadow on hover */
}

/* Bot message style with corner cut */
.bot-message {
  /* Existing styles */
  background-color: rgb(4, 4, 241);
  align-self: flex-start;
  color: rgb(255, 255, 255);

  /* New styles */
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  padding: 8px 12px;
}

/* Bot message text style */
.message-text {
  /* Existing styles */
  word-break: break-word;

  /* New styles */
  margin: 0;
}

/* Hover effect for bot messages */
.bot-message:hover {
  background-color: green; /* Slightly darken the background on hover */
  box-shadow: rgba(0, 0, 0, 0.25) 0px 2px 4px; /* Add a subtle shadow on hover */
  transform: scale(1.02); /* Slightly scale the bot message on hover */
}

.user-message:hover {
  background-color: rgba(
    0,
    0,
    0,
    0.854
  ); /* Slightly darken the background on hover */
  box-shadow: rgba(0, 0, 0, 0.158) 0px 2px 4px; /* Add a subtle shadow on hover */
  transform: scale(1.02); /* Slightly scale the bot message on hover */
}

/* Hover effect for chat message */
.chat-message:hover {
  transform: translateY(-2px); /* Move the message slightly up on hover */
  box-shadow: rgba(0, 0, 0, 0.25) 0px 2px 4px; /* Add a subtle shadow on hover */
}

/* Hover effect for chat input button */
.chat-input button:hover {
  transform: scale(1.1); /* Slightly scale the button on hover */
  background-color: #444; /* Slightly darken the background on hover */
}

/* Hover effect for chat summaries */
.chat-summary:hover {
  background-color: #dcdcdc;
  border-radius: 10px;
  transform: scale(1.02); /* Slightly scale the chat summary on hover */
  box-shadow: rgba(0, 0, 0, 0.1) 0px 2px 4px; /* Add a subtle shadow on hover */
}

/* Hover effect for chatbot-chat */
.chatbot-chat:hover {
  box-shadow: rgba(0, 0, 0, 0.35) 0px 10px 20px; /* Add a stronger shadow on hover */
}

/* Hover effect for input field */
.chat-input input:hover {
  box-shadow: rgba(0, 0, 0, 0.1) 0px 2px 4px; /* Add a subtle shadow on hover */
}

.chatbot-header button {
  padding: 8px 15px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-left: 39px;
  transition: transform 0.3s ease;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 2px 4px;
}

/* Existing CSS code */

/* Media query for screens with a maximum width of 600px */
@media screen and (max-width: 1000px) {
  .chatbot-container {
    width: 90%; /* Reduce the width to take up 90% of the viewport */
    height: auto; /* Reduce the height to take up 70% of the viewport */
  }

  .chatbot-chat {
    height: 90vh; /* Reduce the chat container height */
  }

  .chat-input {
    width: 85%; /* Reduce the width of the input container */
  }

  .chat-input input {
    width: 90%; /* Reduce the width of the input field */
  }

  .chatbot-header button {
    margin-left: 10; /* Reset the left margin for the button */
    margin-top: 10px; /* Add some top margin to the button */
  }
}
</style>
