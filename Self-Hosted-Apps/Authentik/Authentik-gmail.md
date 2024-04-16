### **Step 1: Install Docker and Docker Compose**

1. Update your system's package index:

```
sudo apt-get update
```

1. Install Docker:

```
sudo apt-get install -y docker.io
```

1. Enable Docker to start on boot:

```
sudo systemctl enable --now docker
```

1. Install Docker Compose:

```
sudo apt-get install -y docker-compose
```

### **Step 2: Prepare for authentik Installation**

1. Navigate to the directory where you want to keep your **`docker-compose.yml`**:

```
cd /path/to/your/directory
```

1. Download the latest **`docker-compose.yml`** for authentik:

```
wget https://goauthentik.io/docker-compose.ym
```

### **Step 3: Generate Environment Variables**

1. Install **`pwgen`** for password generation:

```
sudo apt-get install -y pwgen
```

1. Generate and append the environment variables to the **`.env`** file:

```
echo "PG_PASS=$(pwgen -s 40 1)" >> .env
echo "AUTHENTIK_SECRET_KEY=$(pwgen -s 50 1)" >> .env
echo "AUTHENTIK_ERROR_REPORTING__ENABLED=true" >> .env
```

### **Step 4: Configure Gmail SMTP Settings**

1. Create an App Password for your Gmail account if 2-Step Verification is enabled:
    - Visit your Google Account settings.
    - Go to the Security section.
    - Look for "App passwords" and create a new one.
    - Note down the generated password.
2. Open your **`.env`** file with a text editor:

```
nano .env
```

1. Add the following Gmail SMTP settings to the **`.env`** file:

```
AUTHENTIK_EMAIL__HOST=smtp.gmail.com
AUTHENTIK_EMAIL__PORT=587
AUTHENTIK_EMAIL__USERNAME=seanjosephriley@gmail.com
AUTHENTIK_EMAIL__PASSWORD=your_app_password
AUTHENTIK_EMAIL__USE_TLS=true
AUTHENTIK_EMAIL__USE_SSL=false
AUTHENTIK_EMAIL__TIMEOUT=10
AUTHENTIK_EMAIL__FROM=seanjosephriley@gmail.com
```

Make sure to replace **`your_app_password`** with the app password you generated for Gmail.

1. Save and close the file (in nano, press **`CTRL + X`**, then **`Y`**, and **`Enter`** to save).

### **Step 5: Configure Ports**

To configure authentik to use standard web ports, add these lines to your **`.env`** file:

```
COMPOSE_PORT_HTTP=80
COMPOSE_PORT_HTTPS=443
```

### **Step 6: Start authentik**

1. Pull the Docker images:

```
docker-compose pull
```

1. Start the authentik services:

```
docker-compose up -d
```

### **Step 7: Complete Initial Setup**

1. Open your web browser and navigate to **`http://<your server's IP or hostname>:9000/if/flow/initial-setup/`**.
2. Complete the initial setup by setting a password for the **`akadmin`** user.

Your authentik installation should now be up and running with Gmail as the email service. If you have issues sending emails, please ensure that "Less secure app access" is enabled if you're not using 2-Step Verification or check the app password and settings if you are.