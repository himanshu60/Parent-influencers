<template>
    <div class="chatbot-container">
      <div class="chats-list">
        <button @click="newChat">New Conversation</button>
        <h2>Recent Conversations</h2>
        <div
          class="chat-summary"
          v-for="chat in lastChats"
          :key="chat.id"
          @click="selectChat(chat.id)"
        >
          <p>{{ chat.summary }}</p>
        </div>
      </div>
      <div class="chatbot-chat">
        <div class="chatbot-header">
          <h1>Parent-Influencers-ChatBot</h1>
        </div>
        <div class="chatbot-body">
          <div
            v-for="message in messages"
            :key="message.id"
            class="chat-message"
            :class="{
              'user-message': message.fromUser,
              'bot-message': !message.fromUser,
            }"
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
        lastChats: [
          { id: 1, summary: "mera chota beta bhut presan krta hai?..." },
          { id: 2, summary: "meri beti 4 saal ki hai bhut jldi gussa ho jati?.." },
          { id: 3, summary: "JS Learning through ex.." },
          { id: 4, summary: "React Learning through ex.." },
          { id: 5, summary: "TS Learning through ex.." },
        ],
        messages: [
          { id: 1, text: "Hello! \n How can I help you?", fromUser: false },
        ],
        newMessage: "",
      };
    },
    methods: {
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
        let token = localStorage.getItem("token")
  
        if (token) {
          if (this.newMessage.trim() !== "") {
            this.messages.push({
              id: this.messages.length + 1,
              text: this.newMessage,
              fromUser: true,
            });
  
            fetch("http://localhost:5000/parent", {
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
                this.messages.push({
                  id: this.messages.length + 1,
                  text: data.response,
                  fromUser: false,
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
        }else{
          alert("You have to login first")
          this.newMessage = "";
        }
      },
    },
  };
  </script>
  
  <style>
  .chatbot-container {
    display: flex;
    height: 100%;
    /* background-image: url('@/assets/inf-background'); */
    background-size: cover;
    background-position: center;
  }

  .chats-list {
    flex: 1;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    color: #333; /* Text color */
    padding: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    animation: fadeInLeft 0.5s ease; /* Add fade-in animation */
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
    animation: fadeInRight 0.5s ease; /* Add fade-in animation */
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
    background-color: teal;
    color: #fff;
    padding: 10px;
    display: flex;
    justify-content: center;
  }
  
  .chatbot-body {
    flex: 1;
    overflow-y: scroll;
    background-image: url(@/assets/chatinput.jpeg);
    padding: 10px;
    display: flex;
    flex-direction: column;
  }
  
  .chat-message {
    
    margin-bottom: 5px;
    padding: 5px 10px;
    border-radius: 10px;
    max-width: 70%;
  }
  
  .user-message {
    background-color: #5096e5;
    align-self: flex-end; /* Align user messages to the right side */
    color: #fffbfb; /* Set text color for user messages */
  }
  
  .bot-message {
    background-color: #8b7070; /* Set background color for bot messages */
    align-self: flex-start; /* Align bot messages to the left side */
    color: rgb(255, 255, 255); /* Set text color for bot messages */
  }
  
  .message-text {
    
    word-break: break-word;
  }
  
  .chat-input {
    display: flex;
    align-items: center;
    border-top: 1px solid #ccc;
    
    padding: 10px;
    position: fixed;
    bottom: 0;
    width: 72%;
    background-color: #f1f1f1;
    z-index: 1; /* Set a higher z-index to make it appear above other elements */
    animation: slideInUp 0.5s ease; /* Add animation */
  }
  
  .chat-input input {
    flex: 1;
    padding: 5px;
    border: none;
    border-radius: 20px;
    margin-right: 5px;
  }
  
  .chat-input button {
    padding: 5px 15px;
    border: none;
    border-radius: 20px;
    background-color: black;
    color: #fff;
    cursor: pointer;
  }
  
  /* Media query for smaller screens */
  @media (max-width: 768px) {
    .chatbot-container {
      flex-direction: column;
    }
  
    .chats-list {
      flex: 1;
      border-bottom: 1px solid #ccc;
      margin-bottom: 10px;
    }
  
    .chatbot-chat {
      flex: 1;
      margin: 0;
    }
  
    .chat-input {
      width: 100%; /* Set full width on smaller screens */
    }
  }
  </style>
  