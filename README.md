# **บันทึกขั้นตอนการติดตั้ง การใช้งานคลัสเตอร์ที่สร้าง**

Ref.
- https://minikube.sigs.k8s.io/docs/start/

**สร้างคลัสเตอร์ Kubernetes**

เตรียมเครื่องมือ
- kubectl : เครื่องมือที่ติดต่อเพื่อเข้าไปควบคุมKubernetes
- minikube : ใช้จัดการคลัสเตอร์บน Window
- docker engine 

## หัวข้อที่ศึกษา
 - [1.kubectl](#1kubectl)
 - [2.minikube](#2minikube)
 - [3.docker engine ](#3-docker-engine)
 - [4.minikube Deploy-app](#4minikube-deploy-app)

# 1.kubectl
**1.1 Install kubectl**
- ค้นหา Install kubectl 
หรือกดที่ Link : https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
    <center><img src="images/install Kubectl.png" alt="center"></center>

**1.2 Copy คำสั่งต่างๆตามขั้นตอน**
* 1.2.1ดาวโหลดรุ่นล่าสุด version1.26.0 
โดยใช้คำสั่ง :
    <details>
    <summary>Show code</summary>

    ```ruby
    curl.exe -LO        "https://dl.k8s.io/release/v1.26.0/bin/windows/amd64/kubectl.exe"
    ```
    </details>

- ตรวจสอบ binary
    * ทำการดาวโหลด kubectl checksum file โดยใช้คำสั่ง :
    <details>
    <summary>Show code</summary>

    ```ruby
    curl.exe -LO "https://dl.k8s.io/v1.26.0/bin/windows/amd64/kubectl.exe.sha256"
    ```
    </details>

**1.3 การใช้ command promt**
- 1.3.1) สร้างโฟลเดอร์ชื่อ kubectl
    <center><img src="images/create-fol.png" alt="center"></center>

- 1.3.2) รันคำสั่งในข้อที่ 1.2.1
    <center><img src="images/run1.png" alt="center"></center>

- 1.3.3) ปรับ Environment 
    *  Search "Edit the system environment varibles"
    <center><img src="images/envi.png" alt="center"></center>

* กด Environment Variables
    <center><img src="images/envi2.png" alt="center"></center>
    
* เลือก Path
    <center><img src="images/envi3.png" alt="center"></center>
    
* กด New และเพิ่ม Path "C:\kubectl" เสร็จแล้วกด ok

    <center><img src="images/envi4.png" alt="center"></center>

- 1.3.4) ทดสอบเพื่อให้แน่ใจว่าเวอร์ชันของ kubectl เหมือนกับที่ดาวน์โหลดมา
โดยรันคำสั่ง
    <details>
    <summary>Show code</summary>

    ```ruby
    kubectl version --client
    ```
</details>

- 1.3.5) รันคำสั่งนี้ต่อ
    <details>
    <summary>Show code</summary>

    ```ruby
    kubectl version --client --output=yaml
    ```
    </details>
    ผลลัพธ์การรัน
    <center><img src="images/run.output.png" alt="center"></center>

# 2.minikube
**2.1 Install minikube**
- ค้นหา Install minikube หรือกดที่ Link : https://minikube.sigs.k8s.io/docs/start/
    <center><img src="images/install mini.png" alt="center"></center>

**2.2 ติดตั้งตามเว็บไซต์**
- 2.2.1) เลือก Spec ที่จะติดตั้ง
    <center><img src="images/spec mini.png" alt="center">   </center>

- 2.2.2) ดาวน์โหลดและเรียกใช้โปรแกรมติดตั้งสำหรับรุ่นล่าสุด หรือถ้าใช้ PowerShell 
ให้ใช้คำสั่งนี้:
    <details>
    <summary>Show code</summary>

    ```ruby
    New-Item -Path 'c:\' -Name 'minikube' -ItemType     Directory -Force
    Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri              'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-  amd64.exe' -UseBasicParsing
    ```

</details>

- 2.2.3) เพิ่มไบนารี minikube.exe ใน PATH ของคุณ ตรวจสอบให้แน่ใจว่าได้เรียกใช้ PowerShell ในฐานะ Administrator.
    <details>
    <summary>Show code</summary>

    ```ruby
    $oldPath = [Environment]::GetEnvironmentVariable('Path',    [EnvironmentVariableTarget]::Machine)
    if ($oldPath.Split(';') -inotcontains 'C:\minikube'){ `
  [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath),   [EnvironmentVariableTarget]::Machine) `
    }
    ```
    </details>


- 2.2.4) ทดสอบการเรียกใช้งาน minikube ใน command prompt : ถ้าสามารถเรียกใช้งานได้ถือว่าจบขั้นตอน
    * ผลลัพธ์ที่ได้
    <center><img src="images/test.png" alt="center"></center>

# 3. docker engine 
**3.1 Install  Docker Desktop**
- ค้นหา Install  Docker Desktop 
หรือกดที่ Link :https://docs.docker.com/desktop/install/windows-install/

**3.2 เลือกตัวจำลองในการเอา minikube ไปรัน**

- 3.2.1) **Docker**

    Ref.  https://minikube.sigs.k8s.io/docs/drivers/docker/

- run คำสั่งใน command promt
    * เริ่ม cluster โดยการใช้ docker driver
    ใช้คำสั่ง:
        <details>
        <summary>Show code</summary>

        ```ruby
        minikube start --driver=docker
        ```
    </details>

    <center><img src="images/run Doc.png" alt="center"></center>

    * set ให้ Docker เป็นค่า Default
        <details>
        <summary>Show code</summary>

        ```ruby
        minikube config set driver docker
        ```
</details>

- หลังรันเสร็จเช็ค images และ Containers ที่ Docker Desktop
    * Images
    <center><img src="images/images After.png" alt="center"></center>
    
    * Containers
    <center><img src="images/Con-After.png" alt="center"></center>

    * ดู pod ที่ถูกสร้าง 
    ใช้คำสั่ง :
        <details>
        <summary>Show code</summary>

        ```ruby
        kubectl get pod -A
        ```
    </details>
    *ผลลัพธ์: จะเห็นได้ว่ามีหลาย nodes ที่ถูกสร้าง*
        <center><img src="images/pod.png" alt="center"></center>
    
    * จำลองในแลปที่เล็กที่สุดของ cluster ซึ่ง node ทั้งหมดที่สร้างจะถูกรวมไว้ใน minikube เหลือเพียง node เดียว
    
        ใช้คำสั่ง:
        <details>
            <summary>Show code</summary>

         ```ruby
            kubectl get nodes
        ```
        </details>
        ผลลัพธ์
         <center><img src="images/get nodes.png" alt="center"></center>

**3.3 ทดลองเปิด minikube dashboard**
* รันคำสั่งเพื่อ Dashboard minikube

    ใช้คำสั่ง :
    <details>
    <summary>Show code</summary>

     ```ruby
        minikube dashboard
    ```
    </details>
* ผลลัพธ์  
    <center><img src="images/minikube-dashboard.png" alt="center"></center>


# 4.minikube Deploy-app
       
       ทดลองตามอาจารย์-> สร้างโฟลเดอร์แยกทีหลัง
Ref.
- https://minikube.sigs.k8s.io/docs/start/

**4.1 Deploy applications service**
* ใช้คำสั่ง :
    <details>
    <summary>Show code</summary>
    
    ```ruby
    kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
    kubectl expose deployment hello-minikube --type=NodePort --port=8080
    ```
  </details>
     ผลลัพธ์ : 
     - ทำการสร้าง Containers ที่ชื่อว่า hello-minikube 
     - ทำการสร้าง service ที่เป็นชนิดของ NodePort
    <center><img src="images/deploy-create images.png" alt="center"></center>

* เช็ค minikube dashboard จะมีข้อมูลต่างๆขึ้น
    <center><img src="images/dashboard-After.png" alt="center"></center>

* ทดสอบการเชื่อมต่อ ว่ามี service ที่เราสร้าง run อยู่มั้ย
    * ใช้คำสั่ง :
        <details>
        <summary>Show code</summary>
    
        ```ruby
        kubectl get services hello- minikube

        ```
    </details>
    ผลลัพธ์
    <center><img src="images/test-connec.png" alt="center"></center>

* ทำการ Forward Port
    * ใช้คำสั่ง :
        <details>
        <summary>Show code</summary>
    
        ```ruby
       kubectl port-forward service/hello-  minikube 7080:8080


        ```
    </details>
        ผลลัพธ์
    <center><img src="images/forward port.png" alt="center"></center>

**4.1 Deploy applications LoadBalancer**
 - ทำเพิ่มเติม
 
    Ref.: https://minikube.sigs.k8s.io/docs/start/ 

 * Deploy application -> LoadBalancer 
    - ปรับใช้ LoadBalancer
    ใช้คำสั่ง :
        <details>
        <summary>Show code</summary>

        ```ruby
       kubectl create deployment balanced --image=kicbase/echo-server:1.0
        kubectl expose deployment balanced --type=LoadBalancer --port=8080
        ```
    </details>
            ผลลัพธ์
    
    <center><img src="images/LaLoadBalancer.png" alt="center">  </center>

* เช็ค minikube dashboard : 
     <center><img src="images/check-das.png" alt="center">  </center>

* ตรวจสอบ service 
  ใช้คำสั่ง :
  <details>
    <summary>Show code</summary>
    
    ```ruby
       kubectl get services balanced
    ```
    </details>
   
    -  ผลลัพธ์ : จะเห็นได้ว่า Services balanced มีสถานะ Pending อยู่
    <center><img src="images/Pending.png" alt="center">  </center>

    - แก้ไข :โดยการสร้าง tunnel
    ใช้คำสั่ง:
        <details>
        <summary>Show code</summary>
    
        ```ruby
        minikube tunnel
        ```
    </details>
    
     











ยังไม่เสร็จค่ะ 