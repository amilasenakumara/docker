# 🐳 Docker Interview Q&A Sheet

A quick review guide for common Docker interview questions.

---

### 1️⃣ What are images?
Docker images are **templates used to create containers**. They contain everything needed to run an application — code, libraries, dependencies, and configuration — all packaged together.

---

### 2️⃣ Why do we have images and containers? Why not just containers?
We have **images** so we can create **containers quickly and consistently**.  
- **Images** are the **blueprints** that define what a container should look like.  
- **Containers** are the **running instances** of those blueprints.  
If we had only containers, we couldn’t easily **recreate**, **share**, or **version** applications — images make that possible.

---

### 3️⃣ What is a container?
A container is a **lightweight, isolated environment** that runs an application and its dependencies.  
It’s created from a Docker image and behaves like a small virtual machine — but much faster and more efficient.

---

### 4️⃣ What are layers in the context of images?
Layers are the **individual building blocks** of a Docker image.  
Each instruction in a Dockerfile (like `RUN`, `COPY`, `ADD`) creates a new layer, and all layers stack together to form the final image.  
They help **reuse cached parts**, making builds **faster and smaller**.

---

### 5️⃣ What does this command `docker build .` do?
`docker build .` tells Docker to **build an image** using the **Dockerfile in the current directory (`.`)**.  
It reads the Dockerfile, executes its instructions step by step, and creates a new image based on them.

---

### 6️⃣ What does isolation mean in the context of containers?
Isolation means each container runs in its **own separate environment**, with its own filesystem, processes, and network — independent from other containers and the host system.  
This ensures one container can’t affect or interfere with another.

---

### 7️⃣ What does this command do `docker run node`?
`docker run node` downloads (if needed) and **starts a new container** from the official **Node.js image**.  
It opens an interactive shell or runs the default command defined in that image (usually a Node.js REPL).

---

### 8️⃣ Why is the `EXPOSE 80` instruction used in a Dockerfile?
`EXPOSE 80` tells Docker that the application inside the container **listens on port 80**.  
It’s only a **declaration**, not a port mapping — you must use `-p` during `docker run` to make it accessible from outside.

---

### 9️⃣ What are artifacts in Docker builds?
Artifacts are the **output files** created after a build process — for example, compiled code or bundled assets.  
In Docker, you often **build artifacts** first and then copy only the final results into the final image to keep it small.

---

### 🔟 What are Docker layers?
Each layer is a **snapshot** of the filesystem after a Dockerfile instruction runs.  
Layers are **cached**, so Docker only rebuilds layers that change — making builds much faster and efficient.

---

### 🧠 Bonus Tip
> “Docker builds layer by layer — and only cooks the ones you’ve changed.”  

---

**Author:** Generated with ❤️ for quick interview prep.
