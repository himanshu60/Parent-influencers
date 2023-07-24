# Parent-chat-influencers
A parent influencer is a parent who has a significant impact on other people, especially other parents,
through social media and online platforms. They use their personal experiences, advice, and recommendations to influence and inspire others in various aspects of parenting,
such as sharing parenting tips, product recommendations, family activities, and more.

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

![flow-chat-parent app](https://github.com/himanshu60/Parent-influencers/assets/65457075/3af88e18-b200-4981-97ca-2081ce3f0675)



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

![home-parent](https://github.com/himanshu60/Parent-influencers/assets/65457075/109bc4ff-935b-4694-8eb2-398961c60075)


## SignUp Page

![login-signup-parent](https://github.com/himanshu60/Parent-influencers/assets/65457075/9440d6ce-7506-4f4e-81ff-bf6684ed16ab)

## Login Page
![login-parent](https://github.com/himanshu60/Parent-influencers/assets/65457075/498eb6e8-0551-42ed-a6e6-185888cf214a)


## View Parent-chat Page
![parent-chat-conversation-without-login](https://github.com/himanshu60/Parent-influencers/assets/65457075/e43a8dcc-83b1-47c9-897a-b87b62ece958)
![parent-chat-with-conversation](https://github.com/himanshu60/Parent-influencers/assets/65457075/5b8ab356-deb0-43d9-906f-7a5bb971fdcb)
![with-conversation](https://github.com/himanshu60/Parent-influencers/assets/65457075/03180e78-e226-49b2-8adf-2a0f41d68746)


