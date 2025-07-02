🚀 n8n Docker Local Setup
This guide walks you through setting up n8n locally using Docker.

📦 Prerequisites
Make sure you have the following installed on your machine:

Docker

Docker Compose (if using Docker Compose)

Optional: Node.js and npm for development

🛠️ Setup with Docker Compose
1. Clone the Repository
bash
Copy
Edit
git clone https://github.com/your-username/your-n8n-docker-repo.git
cd your-n8n-docker-repo
Replace with your actual repo or set this up in any directory.

2. Create Environment File
Create a .env file in the root directory with the following content:

env
Copy
Edit
# Basic Auth
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=securepassword

# n8n settings
N8N_HOST=localhost
N8N_PORT=5678
N8N_PROTOCOL=http

# Optional: To persist workflows
DB_TYPE=sqlite
3. Add docker-compose.yml
Create a docker-compose.yml file:

yaml
Copy
Edit
version: '3.1'

services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE
      - N8N_BASIC_AUTH_USER
      - N8N_BASIC_AUTH_PASSWORD
      - N8N_HOST
      - N8N_PORT
      - N8N_PROTOCOL
      - DB_TYPE
    volumes:
      - ./n8n-data:/home/node/.n8n
    env_file:
      - .env
4. Start n8n
bash
Copy
Edit
docker-compose up -d
n8n will be accessible at: http://localhost:5678

Login with the credentials from your .env file.

🧹 Stopping and Cleaning Up
To stop the container:

bash
Copy
Edit
docker-compose down
To remove all data (be careful):

bash
Copy
Edit
docker-compose down -v
