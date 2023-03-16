# **บันทึกขั้นตอนการติดตั้ง การใช้งานคลัสเตอร์ที่สร้าง**

Ref.
- https://minikube.sigs.k8s.io/docs/start/

**สร้างคลัสเตอร์ Kubernetes**

เตรียมเครื่องมือ
- kubectl : เครื่องมือที่ติดต่อเพื่อเข้าไปควบคุมKubernetes
- minikube : ใช้จัดการคลัสเตอร์บน Window
- docker engine 

# 1.ติดตั้ง kubectl
**1.1 Install kubectl**
- ค้นหา Install kubectl 
หรือกดที่ Link : https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
<center><img src="images/install Kubectl.png" alt="center"></center>

**1.2 Copy คำสั่งต่างๆตามขั้นตอน**
* 1.2.1ดาวโหลดรุ่นล่าสุด version1.26.0**
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

ยังไม่เสร็จค่ะ