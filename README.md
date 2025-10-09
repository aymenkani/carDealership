# 🚀 Full-Stack Microservices Application

This project is a **full-stack microservices web application** built with a **ReactJS frontend** and **Django** and **Node.js** backend services.  
It includes an integrated **AI-powered Sentiment Analysis service** deployed on **IBM Code Engine**, enabling real-time sentiment evaluation of customer reviews.  
All components are **containerized with Docker**, **orchestrated using Kubernetes**, and continuously delivered through an automated **CI/CD pipeline**.

---

## 🧩 Solution Architecture

The system follows a **cloud-native microservices architecture** designed for scalability, modularity, and maintainability.  
Each component is independently deployable and communicates through well-defined APIs.

---

### 🖥️ Frontend

- Developed with **ReactJS** to provide an interactive and responsive web interface.  
- Enables users to browse dealerships, view car details, and submit reviews.  
- Communicates with backend APIs for data retrieval and submission in real time.

---

### ⚙️ Backend Services

#### **1. Django Service**
- Acts as the primary gateway and central logic layer.  
- Handles user authentication and session management.  
- Exposes RESTful APIs that connect the frontend to backend microservices.  
- Core endpoints include:
  - `get_cars/` — Retrieves available car models and manufacturers.  
  - `get_dealers/` — Returns a list of registered dealers.  
  - `get_reviews/` — Displays customer reviews for a selected dealer.  
  - `add_review/` — Allows authenticated users to post a new review.  
- Integrates seamlessly with the Node.js microservice and AI sentiment analyzer.

#### **2. Node.js Service**
- Dedicated to managing dealer and review data.  
- Uses **MongoDB** as its data store for flexible and scalable data management.  
- Provides APIs consumed by the Django service.  
- Fully **containerized with Docker** for isolated deployment.

---

### 🧠 AI Sentiment Analysis Service

- Implements an **AI-based text analysis model** to classify review sentiment as **positive**, **negative**, or **neutral**.  
- Deployed as a **serverless microservice on IBM Code Engine** for high scalability and efficiency.  
- Sentiment results are displayed in real time within the Django frontend.

---

### ☁️ Infrastructure and Deployment

- **Docker** is used to containerize all microservices for consistent and portable environments.  
- **Kubernetes** orchestrates the containers, ensuring scalability, load balancing, and fault tolerance.  
- **CI/CD pipelines** automate building, testing, and deployment processes.  
- The entire application is deployed on **IBM Code Engine**, enabling seamless integration and cloud-native performance.

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-------------|
| Frontend | ReactJS |
| Backend | Django, Node.js |
| Database | MongoDB |
| AI Service | Python NLP Model (Sentiment Analysis) |
| Containerization | Docker |
| Orchestration | Kubernetes |
| Deployment | IBM Code Engine |
| CI/CD | GitHub Actions |

---

## 📈 Key Highlights

- Modular architecture with independently deployable microservices.  
- AI-driven sentiment analysis integrated into the user experience.  
- Automated CI/CD pipeline ensuring continuous integration and deployment.  
- Scalable and fault-tolerant deployment on Kubernetes and IBM Code Engine.

---

## 📦 Repository Overview
- /frontend → ReactJS application
- /django-service → Django microservice (core gateway)
- /node-service → Node.js microservice (dealers and reviews)
- /sentiment-service → AI sentiment analyzer microservice

---

## 🐳 Run the Application in a Container
You can run the Car Dealership application inside a Docker container or deploy it to Kubernetes for a production-like environment.

### 1. Build the Docker Image
   
   Make sure you’re in the project’s **server** directory where the `Dockerfile` is located.
   ```
      docker build -t dealership-app .
   ```
   
   If you’re using a container registry (for example, IBM Cloud Container Registry):
   ```
   export MY_NAMESPACE=<your-namespace>
   docker tag dealership-app us.icr.io/$MY_NAMESPACE/dealership
   docker push us.icr.io/$MY_NAMESPACE/dealership
   ```

### 2. Run the Container Locally
   To test the app locally using Docker:
   ```
   docker run -p 8000:8000 dealership-app
   ```
   This exposes the Django application on http://localhost:8000

### 3. Deploy to Kubernetes
   
   If you have Kubernetes configured (for example, with IBM Cloud Code Engine or Minikube):<br/>
        
   1. Update the image name in deployment.yaml (inside the server directory) to match your image path.<br/>
   
   ```yaml
   image: us.icr.io/<your-namespace>/dealership:latest
   ```
   2. Apply the deployment file:<br/>
   ```
   kubectl apply -f deployment.yaml
   ```
   3. Forward the container port to access the app:<br/>
   ```
   kubectl port-forward deployment.apps/dealership 8000:8000
   ```
   You can now open http://localhost:8000 to view the application.<br/>

### 5. Notes
   * The container automatically runs database migrations and collects static files on startup (as defined in `entrypoint.sh`)

   * If you have the frontend and microservices separated, make sure their URLs are correctly configured in the environment variables

   * To rebuild or update the container, simply re-run the docker build and kubectl apply commands
