# operations
 The main entrypoint into the project

Unfortunately we were unable to build the docker compose file in time due to issues with GitHub tokens. The individual modules can be inspected and work as intended so the application can still be run through each individual module. 

To check on our progress we refer to the `Docker` branch where we have started on the dokcer compose file. 
 
## Vagrant Setup (Windows)

### Prerequisites
- **Windows Subsystem for Linux (WSL)**
- **Vagrant**
- **VirtualBox**

### Step-by-Step Setup

1. **Open WSL:**
   ```sh
   wsl
   ```

2. **Enable Windows Access for Vagrant (only needed once):**
   ```sh
   export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
   ```

3. **Start Vagrant:**
   ```sh
   vagrant up
   ```

4. **SSH into Vagrant Nodes:**
   - For Node 1:
     ```sh
     vagrant ssh node1
     ```
     - If prompted for a password, use:
       ```
       vagrant
       ```
     - Exit Node 1:
       ```sh
       exit
       ```
   - For Node 2:
     ```sh
     vagrant ssh node2
     ```
     - If prompted for a password, use:
       ```
       vagrant
       ```
     - Exit Node 2:
       ```sh
       exit
       ```

5. **Shutdown Vagrant VMs:**
   ```sh
   vagrant halt
   ```

6. **Destroy Vagrant VMs:**
   ```sh
   vagrant destroy -f
   ```

7. **Shutdown WSL (optional):**
   ```sh
   wsl --shutdown
   ```
