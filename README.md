# Frontend Developent
# 1.Create a Responsive Webpage:
# For this, we will use HTML, CSS (preferably with Flexbox or Grid), and JavaScript.

HTML Structure:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Responsive Webpage</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Navbar -->
    <nav class="navbar">
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">About</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>
    
    <!-- Main Content Layout -->
    <div class="container">
        <div class="left-menu">
            <button class="collapsible">Left Menu</button>
            <div class="menu-content">
                <p>Menu Item 1</p>
                <p>Menu Item 2</p>
                <p>Menu Item 3</p>
            </div>
        </div>
        <div class="main-content">
            <h1>Main Content Area</h1>
            <p>This is the main content.</p>
        </div>
        <div class="right-panel">
            <p>Right Side Panel</p>
        </div>
    </div>
    
    <!-- Footer -->
    <footer>
        <p>Footer Content</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>

CSS (styles.css):
/* Basic styling for layout */
body {
    margin: 0;
    font-family: Arial, sans-serif;
}

.navbar {
    position: fixed;
    top: 0;
    width: 100%;
    background-color: #333;
    padding: 10px;
    z-index: 1000;
}

.navbar ul {
    display: flex;
    list-style-type: none;
    padding: 0;
}

.navbar li {
    margin-right: 20px;
}

.navbar a {
    color: white;
    text-decoration: none;
}

.container {
    display: flex;
    margin-top: 50px;
}

.left-menu, .main-content, .right-panel {
    padding: 20px;
    border: 1px solid #ccc;
    flex: 1;
}

.left-menu {
    width: 200px;
    background-color: #f4f4f4;
}

.main-content {
    flex: 3;
}

.right-panel {
    width: 200px;
    background-color: #f4f4f4;
}

footer {
    text-align: center;
    padding: 10px;
    background-color: #333;
    color: white;
}

/* Collapsible menu */
.collapsible {
    background-color: #4CAF50;
    color: white;
    padding: 10px;
    width: 100%;
    text-align: left;
    border: none;
    cursor: pointer;
    font-size: 15px;
}

.menu-content {
    display: none;
    background-color: #f1f1f1;
    padding: 10px;
}

/* Media Queries */
@media (max-width: 992px) {
    .container {
        flex-direction: column;
    }
}

@media (max-width: 767px) {
    .container {
        flex-direction: column;
    }
}
JavaScript (script.js):
document.addEventListener('DOMContentLoaded', () => {
    // Collapsible Menu
    const collapsible = document.querySelector('.collapsible');
    const menuContent = document.querySelector('.menu-content');

    collapsible.addEventListener('click', () => {
        menuContent.style.display = menuContent.style.display === 'none' ? 'block' : 'none';
    });

    // Shrink Page on Screen Resize
    window.addEventListener('resize', () => {
        let width = window.innerWidth;
        let scale = 1;

        if (width >= 992 && width <= 1600) {
            scale = 0.9;
        } else if (width >= 700 && width <= 767) {
            scale = 0.8;
        } else if (width >= 600 && width <= 700) {
            scale = 0.75;
        } else if (width <= 600) {
            scale = 0.5;
        }

        document.body.style.transform = `scale(${scale})`;
    });
});


# Django: Chat Application
1.Set up Django Project:

Install Django via pip install django
Create a new Django project: django-admin startproject chatapp
Create an app for the chat feature: python manage.py startapp chat
2.Create Models for User and Messages:

In chat/models.py, create models for storing users and messages.
from django.db import models
from django.contrib.auth.models import User

class Message(models.Model):
    sender = models.ForeignKey(User, related_name='sent_messages', on_delete=models.CASCADE)
    recipient = models.ForeignKey(User, related_name='received_messages', on_delete=models.CASCADE)
    content = models.TextField()
    timestamp = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"{self.sender.username} to {self.recipient.username}: {self.content[:20]}"
3.WebSocket for Real-time Chat:

Use Django Channels for real-time communication.
Install Channels: pip install channels
Configure Channels in settings.py:
ASGI_APPLICATION = 'chatapp.asgi.application'
In chat/consumers.py, define the WebSocket consumer for handling chat messages.
4.Views and Templates:

Create a view to render the chat interface, showing a list of users, and handling message sending and receiving.
5.Chat Interface with WebSockets:

The JavaScript code will handle WebSocket communication, displaying new messages in real-time.
6.Authentication and User Management:

Use Django’s built-in authentication system to manage user login and sign-up.

# AWS Lambda Functions
1.Add Two Numbers: AWS Lambda function in Python (e.g., lambda_function.py):
def lambda_handler(event, context):
    num1 = event.get('num1', 0)
    num2 = event.get('num2', 0)
    result = num1 + num2
    return {'statusCode': 200, 'body': result}
2.Store Document in S3: AWS Lambda function for storing a document in an S3 bucket:
import boto3

s3 = boto3.client('s3')

def lambda_handler(event, context):
    bucket_name = 'your-bucket-name'
    file = event['file']
    s3.put_object(Bucket=bucket_name, Key=file['filename'], Body=file['content'])
    return {'statusCode': 200, 'body': 'File uploaded successfully'}



