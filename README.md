# Parent-chat-influencers
A parent influencer is a parent who has a significant impact on other people, especially other parents, through social media and online platforms. They use their personal experiences, advice, and recommendations to influence and inspire others in various aspects of parenting,
such as sharing parenting tips, product recommendations, family activities, and more. So I am creating a web application using Generative AI for asking questions and answering.


<br>

## Deployed Link :

   - Frontend - https://parent-influencers-frontend.vercel.app/
  


<br>

 - Individual:- Himanshu Choudhary
 
# frontend

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


# Site Map for Parent-Chat-Influencers

![flow-chat-parent app](https://github.com/himanshu60/Parent-influencers/assets/65457075/dcca7e51-9ee6-4ebd-aeef-e7ed7d36b63a)




<br>

# What are the requirements?

- User can log in and sign up
- User can visit parent-chat 
- User can see previous Conversations using through login again with the same id
- Users can remove previous chat by clicking on the new-chat button
    - The user can get a response after asking the queries.
    - It will be a private Conversation
- Logout 

# Teach Stacks:-
Frontend: Vue.js | CSS | JavaScript |

Backend: Python | Flask | MongoDB |

Node Modules: bcrypt | cors | dotenv | jsonwebtoken 



# Schema : 

- user 
     - name
     - email
     - password

- prompt
     - id 
     - user-id 
     - prompt
         - question
         - answer

- chats 
    - id
    - user-id
    - chat
       - text(question/answer)
    



## 
<br>

# API Endpoints 
----
<br>

## `User Login/Signup`
<br>   

- Login
                
        GET    -   /login
        POST   -   /register
        DELETE -   /clearchat/<id>

## `Parent Chat`

        GET    -   /parent/<id>
        POST   -   /parent/<id>
        DELETE -   /clearchat/<id>


<br>

  


## Home Page

![home-parent](https://github.com/himanshu60/Parent-influencers/assets/65457075/95bc168a-dc43-4744-8694-786a31988016)



## SignUp Page

![login-signup-parent](https://github.com/himanshu60/Parent-influencers/assets/65457075/e53fb7b8-2389-4d5c-813b-d2493462835f)


## Login Page

![login-parent](https://github.com/himanshu60/Parent-influencers/assets/65457075/348255a1-9b18-486d-9ee6-534ad1df8fe8)


## View Parent-chat Page
![parent-chat-conversation-without-login](https://github.com/himanshu60/Parent-influencers/assets/65457075/58b95c7c-32e3-45bd-b682-08b57c86c385)
![parent-chat-with-conversation](https://github.com/himanshu60/Parent-influencers/assets/65457075/5ae03492-7f6f-446d-9ca7-6b6ff2d20d97)
![with-conversation](https://github.com/himanshu60/Parent-influencers/assets/65457075/b46294ce-607d-45b4-9f75-6b8e318d2d55)




