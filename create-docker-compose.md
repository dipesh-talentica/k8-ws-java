# Docker Compose: NGINX Server in GitHub Codespaces

This guide walks you through creating and running an NGINX server using Docker Compose in GitHub Codespaces. The task will take approximately **10 minutes**.

---

## Prerequisites

1. A GitHub repository where you can create a Codespace.
2. Docker installed in your GitHub Codespace (pre-installed in most setups).

---

## Instructions

### **1. Open a GitHub Codespace**
1. Navigate to your GitHub repository.
2. Click on the `Code` button, then go to the `Codespaces` tab.
3. Click `Create codespace on main` to start a new Codespace.

---

### **2. Create Project Files**
1. Open the terminal in your Codespace.
2. Run the following commands to create a directory and files:
   ```bash
   mkdir nginx-docker-compose
   cd nginx-docker-compose
   touch docker-compose.yml

3. save the file
4. Run the following commands
    ```bash
    cd nginx-docker-compose
    docker-compose up
    
### Task Completed
Congratulations! You’ve successfully set up and run an NGINX server using Docker Compose in GitHub Codespaces.

### Cleanup (Optional)
If you want to stop the server and clean up resources:
1. Press Ctrl+C in the terminal to stop the server.
2. Remove the containers and network
    ```bash
    docker-compose down

### Key Takeways
1. Docker Compose simplifies multi-container setups.
2. It's easy to configure and run services with a single YAML file.
3. This task demonstrated how to use Compose for local development in GitHub Codespaces.    


### Reference you can visit
1. https://waytoeasylearn.com/learn/docker-compose-commands/
2. https://docs.docker.com/compose/

