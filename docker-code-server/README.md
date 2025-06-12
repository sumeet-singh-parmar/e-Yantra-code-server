# e-Yantra Remote IDE

This repository contains the Docker setup for the **e-Yantra Remote IDE**, a web-based development environment powered by [code-server](https://github.com/coder/code-server). It provides a fully customizable IDE with pre-installed extensions and configurations tailored for development.

---

## **Features**
- Pre-installed **GitHub Dark Theme** and **Material Icon Theme**.
- Persistent workspace and user settings using Docker volumes.
- Customizable environment variables for user-specific configurations.
- Password-protected access for secure usage.

---

## **Pull the Docker Image**

To pull the pre-built Docker image from Docker Hub, run:

```bash
docker pull sumeetsinghparmar/eyantra-ide:latest
```

---

## **Build the Docker Image**

To build the Docker image locally, navigate to the root of this directory and run:

```bash
docker build -t eyantra-ide .
```

---

## **Run the Docker Container**

To run the container, use the following command:

```bash
docker run -it -p 8000:8443 \
  -e PASSWORD=123 \
  -e SUDO_PASSWORD=123 \
  -e PWA_APPNAME=eyantra \
  -e PUID=1000 \
  -e PGID=1000 \
  -v /home/sumeet/ros2ws/7/:/config/workspace \
  eyantra-ide
```

### **Explanation of Flags:**
- `-p 8000:8443`: Maps port `8443` in the container to port `8000` on the host.
- `-e PASSWORD=123`: Sets the password for accessing the IDE.
- `-e SUDO_PASSWORD=123`: Sets the sudo password for user inside the container.
- `-e PWA_APPNAME=eyantra`: Sets the Progressive Web App (PWA) name for the IDE.
- `-e PUID=1000` and `-e PGID=1000`: Sets the user and group IDs for file permissions.
- `-v /home/sumeet/ros2ws/7/:/config/workspace`: Mounts the host directory `/home/sumeet/ros2ws/7/` as the workspace inside the container.

---

## **Access the IDE**

Once the container is running, open your browser and navigate to:

```
http://localhost:8000
```

Enter the password (`123` in this example) to access the IDE.

---

## **Customizing the IDE**

### **Default Configuration**
The container includes default configurations for:
- `.bashrc`
- `data/User/settings.json` (VS Code settings)

These files are restored to `/config` on every container startup. You can modify them in the `/defaults` directory during the build process.

### **Extensions**
Pre-installed extensions include:
- **GitHub Dark Theme**
- **Material Icon Theme**

You can install additional extensions by modifying the Dockerfile or using the VS Code Extensions Marketplace inside the IDE.

---

## **Persistent Data**

The `/config` directory is mounted as a volume to ensure that your workspace, settings, and extensions persist across container restarts.

---

## **Contributing**

Feel free to open issues or submit pull requests to improve this setup. Contributions are always welcome!

---

## **License**

This project is licensed under the MIT License.