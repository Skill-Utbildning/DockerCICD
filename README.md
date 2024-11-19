# DOCKER CI CD

## Prerequisites

- Docker installed on your machine
- Docker Compose installed on your machine

## Setup Instructions

1. **Clone the repository**:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. **Build and start the Jenkins services**:
    ```sh
    docker-compose up -d
    ```

3. **Access Jenkins Web UI**:
    - Open your browser and go to `http://localhost:8080`
    - Log in with the credentials:
      - Username: `admin`
      - Password: `admin`

4. **Fetch the Jenkins Agent Secret**:
    - Go to `Manage Jenkins` > `Manage Nodes and Clouds`
    - Click on the agent node (e.g., `agent-1`)
    - Click on `Log` to see the secret or go to `Configure` to find the secret under `Agent secret`

5. **Update the `docker-compose.yml` with the fetched secret**:
    - Edit the `docker-compose.yml` file and replace `your-agent-secret` with the actual secret:
      ```yml
      services:
        jenkins-agent:
          environment:
            - JENKINS_AGENT_SECRET=<fetched-secret>
      ```

6. **Restart the Jenkins services**:
    ```sh
    docker-compose down
    docker-compose up -d
    ```

7. **Verify the Jenkins Agent Connection**:
    - Go to `Manage Jenkins` > `Manage Nodes and Clouds`
    - Ensure that the agent node is connected and online

## Additional Information

- Jenkins home directory is persisted in a Docker volume named `jenkins_home`
- Docker socket is mounted to allow Jenkins to run Docker commands