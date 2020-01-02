---
layout: post
author: Jitendra
categories: [projects]
comments: false
---
This is a concept project. The idea is to build a chat bot that will retrieve nutrition facts of a food when it is asked for using
Google DialogFlow (once called API AI). To know more about what DiaglogFlow is about [visit DialogFlow](https://dialogflow.com/){:target="_blank"}

The application uses [edamam api](https://developer.edamam.com/){:target="_blank"} to fetch the nutrition facts. Intents and action are built using DialogFlow
where as the backend to fetch nutrition facts information is built using Express Js which is a web application framework for Node.js

<!--more-->

Code for the server is available at [github](https://github.com/jitendra8911/nutritionFactsChatBotServer){:target="_blank"}

Even though the DiaglogFlow application is integrated with ExpressJs server using webhooks, the server is not deployed to cloud due to
time and money constraints. The project may be enhanced in future to deploy the server in cloud and integrate the chat bot with any of the 
platforms such google assistant, slack, facebook messenger, twitter, viber, twilio, skype etc.
   