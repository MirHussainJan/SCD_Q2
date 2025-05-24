# Deployment Instructions

This guide provides step-by-step instructions to deploy the application and its components.

## Prerequisites
- Kubernetes cluster set up and `kubectl` configured.
- Namespace `dataviz-ns` created.

## Steps to Deploy

### 1. Create Namespace
```bash
kubectl apply -f dataviz-namespace.yaml
```

### 2. Deploy MongoDB
1. Create the Persistent Volume Claim (PVC):
   ```bash
   kubectl apply -f mongodb-pvc.yaml
   ```
2. Deploy MongoDB:
   ```bash
   kubectl apply -f mongodb-deployment.yaml
   ```

### 3. Deploy Backend
1. Apply the ConfigMap and Secret:
   ```bash
   kubectl apply -f backend-config.yaml
   kubectl apply -f backend-secret.yaml
   ```
2. Deploy the Backend:
   ```bash
   kubectl apply -f backend-deployment.yaml
   ```
3. Expose the Backend Service:
   ```bash
   kubectl apply -f backend-service.yaml
   ```

### 4. Deploy Frontend
1. Deploy the Frontend:
   ```bash
   kubectl apply -f frontend-deployment.yaml
   ```
2. Expose the Frontend Service:
   ```bash
   kubectl apply -f frontend-service.yaml
   ```

### 5. Perform Rolling Update for Backend
1. Update the backend deployment to use a specific image version and rolling update strategy:
   ```bash
   kubectl apply -f backend-deployment.yaml
   ```

## Verify Deployment
1. Check all resources:
   ```bash
   kubectl get all -n dataviz-ns
   ```
2. Access the frontend using the NodePort exposed by the frontend service.

## Notes
- Ensure all YAML files are in the same directory as your terminal's working directory.
- Replace `dataviz-ns` with your namespace if different.

Enjoy your deployment!
