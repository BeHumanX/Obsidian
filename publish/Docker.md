## What is docker?

>Docker is a tool that helps you **package, distribute, and run applications** in a consistent and isolated environment. Think of it as a **shipping [[Container]] for software**, Just like shipping containers standardize the transportation of goods, Docker standardizes the way applications are built, shipped, and run.

### **How Docker Works**
1. **Build:**
    - You write a **Dockerfile** to define your application’s environment.
    - You use the `docker build` command to create an **[[Image]]** from the Dockerfile.
2. **Ship:**
    - You upload the image to a registry (e.g., Docker Hub) using `docker push`.
    - Others can download the image using `docker pull`.
3. **Run:**
    - You use the `docker run` command to start a **[[Container]]** from the image.
    - The [[Container]] runs your application in an isolated environment.