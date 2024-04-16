# Mailcow Install
1. **Update and upgrade Ubuntu:**
    
    ```bash
    sudo apt update
    sudo apt upgrade
    ```
    
2. **Install prerequisites:**
    
    ```bash
    sudo apt install apt-transport-https ca-certificates curl software-properties-common
    ```
    
3. **Add the Docker repository:**
    
    ```csharp
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```
    
4. **Install Docker:**
    
    ```sql
    sudo apt update
    sudo apt install docker-ce
    ```
    
5. **Add your user to the Docker group:**
    
    ```bash
    sudo usermod -aG docker $USER
    ```
    
6. **Log out and log back in to apply the changes.**
7. **Download and run the MailCow installation script:**
    
    ```bash
    wget https://github.com/mailcow/mailcow-dockerized/archive/master.tar.gz
    tar xf master.tar.gz
    cd mailcow-dockerized-master
    ./generate_config.sh
    ```
    
8. **Configure MailCow:**
    
    ```
    Copy code
    nano mailcow.conf
    
    ```
    
    Configure the necessary settings such as domain name, email address, and password.
    
9. **Install MailCow:**
    
    ```
    Copy code
    docker-compose up -d
    
    ```
    
10. **Access MailCow:**
Visit your server's IP address or domain name in a web browser and log in using the credentials you specified in the configuration.

Regarding the specific file paths, the paths may vary depending on your setup and version of MailCow. However, the configuration file is typically located in the MailCow directory, and the installation script usually sets up the required directory structure for you.

Always refer to the official MailCow documentation or the GitHub repository for the most up-to-date information and any potential changes.

---

To ensure that your MailCow server functions correctly, you'll need to forward certain ports on your router to allow incoming traffic to reach the MailCow services. Here are the standard ports that you may need to forward:

1. **SMTP (Simple Mail Transfer Protocol):** Port 25 (or 587 if using submission port for email clients)
    - Used for sending email messages.
2. **IMAP (Internet Message Access Protocol):** Port 143 (or 993 for secure SSL/TLS connections)
    - Used for retrieving email messages from the server.
3. **POP3 (Post Office Protocol 3):** Port 110 (or 995 for secure SSL/TLS connections)
    - Used for downloading email messages from the server to the email client.

Ensure that these ports are properly forwarded on your router to allow external traffic to reach your MailCow server. Consult your router's user manual or documentation for instructions on how to set up port forwarding.

Additionally, if you plan to access the MailCow web interface remotely, you may need to forward port 80 for HTTP or port 443 for HTTPS, depending on your setup. Forwarding these ports will allow you to access the MailCow web interface securely over the internet.