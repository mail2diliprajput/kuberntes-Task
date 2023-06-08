# kuberntes-Task

1)_Connect two pods to the same external access point
-------------------------------------------------
Step -1 First Pod
-------------------------------------------------
#pod1.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dep1
  labels:
    apps: dep1
    tier: cloud
spec:
  template:
    metadata:
      name: dep1-pod
      labels:
        app: deployment1
    spec:
        containers:
        - name: cont1
          image: cont1
          ports:
            - containerPort: 8081
  selector:
    matchLabels:
      app:deployment1
      
      
-------------------------------------------------
Step -2 Secound Pod
-------------------------------------------------
#pod2.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dep2
  labels:
    apps: dep2
    tier: cloud
spec:
  template:
    metadata:
      name: dep2-pod
      labels:
        app: deployment1
    spec:
        containers:
        - name: cont2
          image: cont2
          ports:
            - containerPort: 8081
  selector:
    matchLabels:
      app:deployment1
      
-------------------------------------------------
Step -3 Service Create 
-------------------------------------------------
#service.yaml
apiVersion: v1
kind: Service
metadata:
  name: service1
spec:
  type: NodePort
  ports:
    - port: 8081
      targetPort: 8081
      nodePort: 30169
  selector:
    app: deployment1
