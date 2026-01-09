apiVersion: apps/v1
kind: Deployment
metadata:
  name: python-webapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: python-webapp
  template:
    metadata:
      labels:
        app: python-webapp
    spec:
      containers:
      - name: python-app
        image: python:3.9-slim
        command: ["python", "-c", "from http.server import HTTPServer, SimpleHTTPRequestHandler; HTTPServer(('', 8000), SimpleHTTPRequestHandler).serve_forever()"]
        ports:
        - containerPort: 8000




apiVersion: v1
kind: Service
metadata:
  name: python-service
spec:
  selector:
    app: python-webapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8000
  type: LoadBalancer
