# 🐳 Docker Cheat Sheet for DevOps (No Programming Required)

## 1️⃣ Identify the App Basics
- **Entry point**: command to start the app (`npm start`, `python app.py`, `java -jar app.jar`)
- **Dependencies**: list of required packages
  - Node → `package.json`
  - Python → `requirements.txt`
  - Java → `pom.xml` / `build.gradle`
- **Ports**: which port the app listens on
- **Data folders**: any directories that must persist

## 2️⃣ Create a Dockerfile
Minimal Dockerfile template:

```dockerfile
# Base image for the app type
FROM <official-image>   # e.g., node:20-alpine, python:3.12-slim, openjdk:20

# Set working directory inside container
WORKDIR /app

# Copy dependency files
COPY <dependency-files> ./

# Install dependencies
RUN <install-command>  # e.g., npm install, pip install -r requirements.txt, mvn install

# Copy app code
COPY . .

# Expose the port
EXPOSE <PORT>

# Command to start the app
CMD ["<start-command>"]
```

> Replace `<...>` with info you collected in step 1.

## 3️⃣ Build the Docker image
```bash
docker build -t <image-name>:<tag> .
```

- `.` → current folder where Dockerfile is located
- `<image-name>` → your custom name
- `<tag>` → version (like `1.0`)

## 4️⃣ Run the container
```bash
docker run -d \
  --name <container-name> \
  -p <host-port>:<container-port> \
  -v <host-volume>:<container-volume> \
  --env-file .env \
  <image-name>:<tag>
```

- `-d` → detached (run in background)  
- `-p` → map host port to container port  
- `-v` → mount volumes for persistent data  
- `.env` → environment variables  

## 5️⃣ Debugging
If the container exits immediately:
```bash
docker ps -a                  # see stopped containers
docker logs <container-name>  # view crash logs
```
Run interactively to test:
```bash
docker run -it --rm <image-name>:<tag> sh
# Then manually start the app to see errors
```

## 6️⃣ Common DevOps Notes
- **Don’t need to understand the code** — just know start command, ports, dependencies.  
- Use **named volumes** for folders the app writes to (logs, node_modules, temp).  
- Always separate **read-only code** vs **writable data**.  
- `.env` files are mounted at runtime — never copy secrets into images.  
- Test locally before deploying to production or Kubernetes.  

## 7️⃣ Optional: Use Docker Compose
- If app needs multiple services (DB, cache, API), create `docker-compose.yml`:
```yaml
version: "3.9"
services:
  app:
    build: .
    ports:
      - "3000:8000"
    env_file:
      - .env
    volumes:
      - feedback:/app/feedback
      - /app/node_modules
      - /app/temp
volumes:
  feedback:
```
- Run everything with:
```bash
docker-compose up -d
```

💡 **TL;DR:**
With this cheat sheet, as a DevOps engineer you **can containerize any app** without knowing the programming language — just follow the app’s entry point, dependencies, ports, and volume requirements.

