# Blue-Green Deployment Project

  # Part 1 — Local Deployment
  
  
  # Project Setup
  
  # 1. Clone the Repository

  git clone <your-repository-url>
  cd blue-green-project
 
----

  # 2. Local Development
  
  # Backend Setup
    1. Navigate to backend directory
    2. Install dependencies
 
    cd backend
    npm install

    3. Create `.env` file with:
  
    PORT=5000
    MONGO_URI=mongodb+srv://alinahashmi2025_db_user:ebCvKe8e8ZxIUSbn@mycluster.2etxcjo.mongodb.net/bluegreen

    4. Start backend server

       npm start

<img width="633" height="298" alt="image" src="https://github.com/user-attachments/assets/2c0b36aa-80e3-4513-8399-5dac6f1c2318" />
       
----
  
  # Frontend Setup
  
    1. Setup Blue Frontend
 
       cd frontend-blue
       npm install

    2. Create `.env` file:

        PORT=3100
 
    3. Start blue frontend
   
        npm start

<img width="1523" height="948" alt="image" src="https://github.com/user-attachments/assets/009eca75-1e0c-4d49-801e-6327bde47649" />


<img width="1430" height="990" alt="image" src="https://github.com/user-attachments/assets/1191d32c-c264-4c2f-a1b0-6dc25a50745d" />


    4. Repeat similar steps for Green Frontend (with PORT=3200)


<img width="1411" height="962" alt="image" src="https://github.com/user-attachments/assets/90bb2c42-6a2d-4943-88d5-9aa3a0b20768" />



-----

# 3. Dockerization


### Build Backend Image

docker build -t imran7012/backend:latest .

### Build Blue Frontend Image

docker build -t your-username/frontend-blue:latest .

### Build Green Frontend Image

docker build -t your-username/frontend-green:latest .


<img width="1902" height="747" alt="image" src="https://github.com/user-attachments/assets/1f7de074-8028-4220-a67a-4fc2459058d1" />


### Run Containers
docker-compose up -d

<img width="1518" height="203" alt="image" src="https://github.com/user-attachments/assets/a3025abc-0d65-49f8-ab27-e98a06c5b09e" />

-----


# 4. Kubernetes Deployment


 # Create Kubernetes Manifest Files

### Required Manifest Files
Create following files in `k8s/` directory:
- `backend-deployment.yaml`
- `frontend-blue-deployment.yaml`
- `frontend-green-deployment.yaml`
- `frontend-service.yaml`

-----

# Deploy to Minikube

### Apply all manifests
kubectl apply -f k8s/

### Verify deployments
kubectl get deployments
kubectl get services
kubectl get pods
kubectl get svc

<img width="702" height="190" alt="image" src="https://github.com/user-attachments/assets/31d5280d-31b7-46d5-a752-ed84565a9fb6" />

-----

# Blue-Green Switching

## Switch Traffic Methods

## Create file patch.json

<img width="422" height="447" alt="image" src="https://github.com/user-attachments/assets/979683d7-baa1-4f4c-aef7-cafe47ac1771" />

-----


# Switch to Green

kubectl patch svc frontend --patch-file patch.json

kubectl get svc frontend -o yaml



<img width="531" height="368" alt="image" src="https://github.com/user-attachments/assets/7b149f63-c176-40db-a9fb-5694840d00f8" />



 kubectl port-forward svc/frontend 8080:80

<img width="1535" height="958" alt="image" src="https://github.com/user-attachments/assets/495a345a-d493-4f82-b8bd-05eea885ba79" />

-----

# Switch back to Blue

kubectl patch svc frontend --patch-file patch.json

kubectl get svc frontend -o yaml



<img width="631" height="960" alt="image" src="https://github.com/user-attachments/assets/1f616603-e872-463c-a997-988a2e4794a5" />



kubectl port-forward svc/frontend 8080:80

 
<img width="1448" height="973" alt="image" src="https://github.com/user-attachments/assets/4c624bfe-aaae-4ca5-977b-2d5c4ee7d6d2" />


-----


