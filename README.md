# Simple Face Recognition

## Introduction

I am experimenting with the face recognition task of computer vision. I would like to build a simple website that allows for a picture-based login. 

## Requirements

Here are the requirements from the website.
1. There should be a login page where users can register or login into their accounts.
2. At the time of registration, users will have to provide a unique username and click a photograph from their webcam.
3. At the time of login, they will have to provide their username and access to the webcam. 
4. The website should save the user's photograph along with the username at the time of registration. And match the photograph with the webcam live feed at the time of login.
5. If the user in the photograph is present in the live feed, the website should allow access else it should deny access.

## Tech stack

I am going to use the following tech stack for this project.
1. Frontend:
   1. VueJS
   2. Socket.io
2. Backend:
   1. Node.js
   2. Express.js
   3. Face-API.js

## Sub-problems to solve

1. Create the front end of the login page using Vue.JS. The login page should do two jobs, sign-in and sign-up.
   1. For sign-in, you should have a textbox for username and the website should send your 
2. Create the backend using Express.js