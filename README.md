# Kubernetes

# Wakatime
- https://wakatime.com/@spcn05/projects/ezgjtswfdh

# Ref
- https://github.com/iamapinan/kubeplay-traefik

# ขั้นตอนการติดตั้ง kubectl

1. ใช้คำสั่ง
    
  ```
    curl.exe -LO "https://dl.k8s.io/release/v1.26.0/bin/windows/amd64/kubectl.exe"
  ```
  
2. ตรวจสอบเวอร์ชั่น 
    
  ```
    kubectl version --client
  ```

# ขั้นตอนการติดตั้ง Traefik

1. ใช้คำสั่งติดตั้ง Traefik Resource Definitions

  ```
    kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml
  ```

2. ใช้คำสั่งติดตั้ง RBAC for Traefik

  ```
    kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml
  ```

3. ทำการสร้าง namespace

  ```
    kubectl create namespace <namespace>
  ```

4. ใช้คำสั่งติดตั้ง Traefik Helmchart

  ```
    helm repo add traefik https://traefik.github.io/charts
    helm repo update
    helm install traefik traefik/traefik
  ```

5. ตรวจสอบ Service Traefik

  ```
    kubectl get svc -l app.kubernetes.io/name=traefik
    kubectl get po -l app.kubernetes.io/name=traefik
  ```

6. ใช้คำสั่งเปิด LoadBalance

  ```
    minikube tunnel
  ```

6. ทำการสร้างรหัส Secret โดยทำการรันบน git bash โดย <user> คือ User ที่ใช้ล็อกอินใน Traefik

  ```
    htpasswd -nB <user> | tee auth-secret

    kubectl create secret generic -n default dashboard-auth-secret --from-file=users=auth-secret -o yaml --dry-run=client | tee dashboard-secret.yaml
  ```
    จะได้ไฟล์ที่ชื่อว่า dashboard-secret.yaml ขึ้นมา

7. นำรหัสคีย์จากไฟล์ dashboard-secret.yaml มาใส่ใน traefik-dashboard.yaml

8. ทำการ Deploy โดยใช้คำสั่ง

  ```
    kubectl apply -f traefik-dashboard.yaml
  ```

9. ทดสอบโดยการเข้าไปยังลิงค์ https://traefik.spcn05.local/dashboard/#/

    ![](image/traefik.png)

    ![](image/traefik-route.png)





