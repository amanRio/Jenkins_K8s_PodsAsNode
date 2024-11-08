Jenkins on Kubernetes with Dynamic Node Configuration for Agents

This repository provides a complete setup to deploy Jenkins on Kubernetes with dynamically configured nodes (agents). This setup includes Persistent Volumes, Ingress, Services, and Role Bindings for managing Jenkins and its agents.
Project Overview
This project automates Jenkins deployment on Kubernetes using YAML configuration files. The setup enables Jenkins to use Kubernetes as an agent provider, dynamically provisioning nodes as agents on-demand, ideal for scalable CI/CD environments.
Files in the Repository
•	jenkins_deployment.yml: Defines the Jenkins deployment on Kubernetes, configuring the master instance, resources, environment variables, and dynamic agent provisioning.
•	jenkins_ingress.yml: Configures ingress for external access to Jenkins, including hostname routing and SSL/TLS settings if required.
•	jenkins_service.yml: Exposes Jenkins as a service within the cluster, allowing internal communication with other services and the Ingress controller.
•	jenkins_volume.yml: Defines PersistentVolumeClaim for Jenkins, ensuring that data persists across pod restarts.
•	role_bindings.yml: Sets up Role-Based Access Control (RBAC) for Jenkins to interact with Kubernetes resources, enabling Jenkins to provision and manage agent nodes dynamically.
Prerequisites
•	Kubernetes Cluster: A running Kubernetes cluster (local or cloud-based).
•	kubectl: Kubernetes command-line tool.
•	Helm (optional): To manage Jenkins plugins or configurations.
•	Ingress Controller: Ensure an ingress controller (such as NGINX or Traefik) is installed on the cluster if using Ingress.
Setup Guide
1. Configure Jenkins Persistent Storage
Apply the jenkins_volume.yml to create persistent storage for Jenkins.

kubectl apply -f jenkins_volume.yml

2. Deploy Jenkins
Apply the Jenkins deployment configuration to create the Jenkins master instance. This configuration includes settings for dynamic agent provisioning.

kubectl apply -f jenkins_deployment.yml

3. Expose Jenkins Service

Apply the jenkins_service.yml to create a service that exposes Jenkins within the cluster.

kubectl apply -f jenkins_service.yml

4. Set Up Ingress (Optional)
If you require external access to Jenkins, apply the jenkins_ingress.yml file to set up routing.

kubectl apply -f jenkins_ingress.yml

Ensure that the ingress controller is correctly configured and DNS is set up if using a custom domain.
5. Configure RBAC for Jenkins
Apply the role_bindings.yml file to grant Jenkins necessary permissions to create and manage agent nodes.

kubectl apply -f role_bindings.yml

This enables Jenkins to dynamically provision and manage agents within the Kubernetes cluster.
Accessing Jenkins
•	Internal Access: Use the jenkins_service within the cluster to access Jenkins from other pods.
•	External Access: If Ingress is configured, access Jenkins at http://<your-domain>/ or as specified in your ingress configuration.
Dynamic Agent Configuration
With this setup, Jenkins can dynamically provision Kubernetes pods as agents based on pipeline requirements. This enables scalable CI/CD by creating agent pods as needed and terminating them upon completion.
Useful Commands
•	Check Pods: Monitor the Jenkins master and agent pods.
kubectl get pods -n <namespace>
•	View Logs: View Jenkins master logs.
kubectl logs -f <jenkins-master-pod-name> -n <namespace>
•	Delete Deployment: Remove Jenkins and related resources.
kubectl delete -f jenkins_deployment.yml
kubectl delete -f jenkins_service.yml
kubectl delete -f jenkins_ingress.yml
kubectl delete -f jenkins_volume.yml
kubectl delete -f role_bindings.yml
Contributing
Feel free to open issues or submit pull requests if you’d like to contribute to this project. Contributions for optimizing configurations, adding Helm chart templates, or enhancing dynamic provisioning are welcome.
License
This project is licensed under the MIT License.

