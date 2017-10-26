# Kubernetes Ingress Controllers Explained

Kubernetes ingress controllers are an amazing service on K8s that allows you to route public requests to the proper internal K8s services you have running.

## Prerequisites
- Understanding of:
    - Services and Service Manifest File in K8s
    - Deployments and Deployment Manifest File in K8s

## Anatomy of an Ingress Controller

Essentailly you can think of an Ingress Controller/Service as needing 3 things:
1. A Service manifest defined that will point to the pods/deployment that handles the actual proxying of requests
    - This is nothing different that a service definition for any other app
    - The type will be ```loadBalancer``` and it will provision an IP address for you
2. A Deployment manifest that defines how to do standup and run the pods/containers that represent the Ingress Controller
    - 3 Popular choices are [GCE Ingress](https://github.com/kubernetes/ingress-gce), [Nginx](https://github.com/kubernetes/ingress-nginx) (both maintained by Kubernetes Team) and [Traefik](https://traefik.io/)
3. Rules that define how the controller should proxy/route requests to the actual underlying services you wish send payloads to
    - These are ingress rules/config maps that define:
        - On a certain Public IP/Hostname/Domain and/or Port combination, to which named k8s service should you route to e.g. [```My-App-1 Service```, ```My-App-2 Service```, ```My-App-3 Service```]

You can deploy with one large Manifest file or break down the deployment.

![Ingress Diagram](images/ingress_diagram.png)