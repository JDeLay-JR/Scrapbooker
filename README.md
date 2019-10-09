# Scrappr: A Collaborative, Real-Time, Event Driven Scrapbook

## Project Background

Scrappr is a collaborative, real-time, event driven scrapbooking application for events, happenings, and life. Scrappr was built during my time as a student at The Fullstack Academy of Code. I worked closely with two other software engineers, Tim LaTorre and Bryan Clark, to build this unique platform that enables event-goers to contribute content in real-time to create a virtual scrapbook.

## Technology Stack

The technology stack our team used to build Scrappr was based on Node.js. Our backend consisted of a PostgreSQL database in combination with an Express web server. We decided to leverage the Sequelize.js ORM to seamlessly manage data flow from our database to our frontend. We built our frontend using React & Redux which allowed us to create a highly responsive progressive web application that was able to respond immediately to real-time state changes in the Redux store.

## Dealing with Images

### Firebase and Socket.io

One of the biggest challenges that our group faced was finding a solution for image storage. We decided to leverage Google's Firebase Storage technology to handle image hosting. Our team decided against using a third-party database system because we wanted to have strict control over the flow of image and user data. Therefore we used Firebase as a micro-service solely to host images and generate reference URLs that are subsequently saved to our PostgreSQL database along with other relevant EXIF image metadata. Once we obtain the URL reference and metadata we package it into an image object. We then utilized Socket.io to emit this image object from the client's device, to our server, which then broadcasts it to all of the event's participants triggering a real-time re-rendering of their photo mosaic to include the newly uploaded image.


### Image Compression & Orientation

An interesting challenge our group had to overcome was how to send images from a client's phone to our Firebase Storage server in a timely and performant manner. To accomplish this task we used HTML5's canvas element to reorient and resize each and every photo. Reducing the size of each photo sped up the entire upload process and reorienting each image allowed React to render them properly in the grid on the Mosaic component.

## Other Interesting Technology Used

Our team utilized both the Twilio API and the Nodemailer email module to facilitate the invitation process for event organizers and participants alike. All an organizer has to do is add their invitees as contacts and a text message and/or email is automatically sent to each participant's phone. We give the event organizer the option to choose either one or both of these options by having two different API end points that handle either text messages or emails respectively. In each API endpoint a secure link is generated and subsequently minimized by Bitly before being sent to a participant with an event-specific message.

