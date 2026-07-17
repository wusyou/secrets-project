# Secrets Project

![Node.js](https://img.shields.io/badge/Node.js-Backend-339933?logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express.js-Framework-000000?logo=express&logoColor=white)
![EJS](https://img.shields.io/badge/EJS-Templating-B4CA65?logo=ejs&logoColor=black)
![Axios](https://img.shields.io/badge/Axios-HTTP%20Client-5A29E4?logo=axios&logoColor=white)
![Vercel](https://img.shields.io/badge/Deployed%20on-Vercel-000000?logo=vercel&logoColor=white)

A server-side rendered web app that fetches a random anonymous secret from an external REST API and displays it dynamically. Built as part of Angela Yu's Web Development Bootcamp (Udemy).

---

## Table of Contents

- [About the Project](#about-the-project)
- [Tech Stack](#tech-stack)
- [API Architecture and Workflow](#api-architecture-and-workflow)
- [Project Structure](#project-structure)
- [Setup and Running Locally](#setup-and-running-locally)
- [Deployment](#deployment)
- [Repository](#repository)

---

## About the Project

**Project Name:** Secrets Project

**Source:** Angela Yu's Web Development Bootcamp (Udemy)

**What It Is:** A Node.js and Express application that acts as a server-side client to an external public REST API. When the user visits the home page, the server requests a random secret from the API and renders it into an EJS template, so the browser only ever receives fully rendered HTML.

---

## Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Backend Framework** | Node.js with Express.js |
| **Frontend Templating** | EJS (Embedded JavaScript) for dynamic rendering |
| **HTTP Client** | Axios for server-to-server requests |
| **Styling** | Custom CSS (`public/styles/main.css`) |
| **Deployment Platform** | Vercel (configured as a serverless Node.js app via `vercel.json`) |

---

## API Architecture and Workflow

The app connects to an external public REST API with the base URL `https://secrets-api.appbrewery.com`.

The request flow works like this:

1. The user visits the root path (`/`).
2. The Express server uses Axios to send a `GET` request to the `/random` endpoint of the API.
3. The API returns JSON data containing a `secret` and a `username`.
4. That data is passed into `index.ejs` and rendered dynamically before the page is sent to the browser.

```
Browser  ->  GET /  ->  Express Server
                            |
                            |  Axios GET /random
                            v
              https://secrets-api.appbrewery.com
                            |
                            |  JSON { secret, username }
                            v
              Express renders index.ejs  ->  HTML  ->  Browser
```

Because the API call happens on the server, the API base URL and response handling stay on the backend, and the client only receives the final rendered page.

---

## Project Structure

```
5.6 Secrets Project/
├── public/
│   └── styles/
│       └── main.css        # Custom styling
├── views/
│   └── index.ejs           # Dynamic template for the secret and username
├── index.js                # Express server and Axios API logic
├── vercel.json             # Serverless deployment config
└── package.json            # Dependencies and scripts
```

---

## Setup and Running Locally

### Prerequisites
Make sure the following are installed:
- Node.js (LTS version recommended)
- npm (comes bundled with Node.js)
- Git

### Steps

1. Clone the repository:
```bash
   git clone https://github.com/wusyou/secrets-project.git
```

2. Move into the project folder:
```bash
   cd secrets-project
```

3. Install the dependencies:
```bash
   npm install
```

4. Start the server:
```bash
   node index.js
```

5. Open your browser and visit:
```
   http://localhost:3000
```

### Port Configuration
The app uses a dynamic port through `process.env.PORT`, with a fallback to port `3000` when run locally. This lets the same code run both on a hosting platform and on your machine without changes.

---

## Deployment

This project is configured for deployment on **Vercel** as a serverless Node.js application. The `vercel.json` file tells Vercel how to build and route requests to the Express app, so no separate always-on server is required.

---

## Repository

GitHub: `https://github.com/wusyou/secrets-project.git`
