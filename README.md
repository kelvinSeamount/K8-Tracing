                        K8s Distributed Tracing with Grafana Tempo & Alloy
                  

Problem Statement 

   So here's the thing when you are running microservices in Kubernetes, debugging issues can be very!! very!!! problematic.
   A request comes in, bounces through 5 different services, fails somewhere in the middle, and you are left staring at logs wondering "where did it all go wrong?" Traditional logging just doesn't cut it when you need to follow a request's journey across multiple services.

   That's where distributed tracing comes in. But before you can analyze traces, you need to generate them, collect them, and store them somewhere. And honestly? Setting all that up can feel like a project in itself.

Poject Aim

   This is a simple, working example of a distributed tracing stack in Kubernetes that you can actually learn from and build on. Nothing fluff, just the essentials:

# Generates traces using k6 (a load testing tool with tracing capabilities)
# Collects traces with Grafana Alloy (the telemetry data collector)
# Stores and queries traces in Grafana Tempo (the distributed tracing backend)


How It Works

   k6-trace-generator: This pod continuously generates synthetic traces using the xk6-client-tracing extension. It's basically simulating what a real application would send.

   Alloy: Acts as the middleman. It receives traces via OpenTelemetry Protocol (OTLP) on port 4317 and forwards them to Tempo. Why use Alloy? It handles batching, retry logic, and keeps your apps from needing to know where Tempo lives.

   Tempo: Stores all those traces efficiently and lets you query them later through Grafana.


Prerequisites

   A Kubernetes cluster (minikube, kind, Docker Desktop with Kubernetes enabled, or whatever you've got - I used Docker Desktop for this)

   kubectl configured and ready to go
   
   Helm 3 installed  

   Do not have Grafana Alloy and Tempo set up yet? No worries! Check out the command.md file for a step by step instructions on deploying the entire stack (Prometheus, Grafana, Tempo, and Alloy) using Helm.


![alt text](<Screenshot 2025-10-19 at 18.17.04.png>)

