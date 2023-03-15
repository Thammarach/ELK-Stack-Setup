# ELK-Stack-Setup
This install ELK Stack (Elasticsearch, Logstash, Kibana) on Ubuntu 22.04

👨‍💻 **การติดตั้ง Java บน Ubuntu 20.04 LTS**

- การเข้าใช้งานในฐานะสิทธิ์ระดับ Superuser
```
sudo -i
```

- เริ่มต้นด้วยการอัพเดทแพ็คเกจระบบ
```
o	sudo apt update
```

- ติดตั้งแพ็คเกจ apt-transport-https เพื่อให้สามารถเข้าถึง HTTPS
```
o	sudo apt install apt-transport-https
```

- ติดตั้ง OpenJDK 11 บน Ubuntu 22.04
```
o	java –version
```
Output:
<img width="277" alt="image" src="https://user-images.githubusercontent.com/88868657/225249069-385d0b0d-7195-4d68-8be2-e2b52a66931d.png">

- การเข้าไปกำหนดค่าใน environment หลังจากการติดตั้ง Java เสร็จสิ้น
```
o	sudo nano /etc/environment
```

- เมื่อเข้ามาแล้วให้นำตัวแปรด้านล่างนี้ไปวางในไฟล์ของ environment
```
o	JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```

- โหลดไฟล์ environment โดยใช้คำสั่งต่อไปนี้
```
o	source /etc/environment
```

- ตรวจสอบตัวแปรหลังจากที่ได้เพิ่มลงไป
```
o	echo $JAVA_HOME
```
Output:
<img width="277" alt="image" src="https://user-images.githubusercontent.com/88868657/225249810-64c4c63d-5310-463d-a265-3552f168bba8.png">

👨‍💻 **การเปิดและปิดใช้งาน firewall ports บน Ubuntu 20.04 LTS**

- การเริ่มและหยุดใช้งาน UFW
```
o	sudo ufw enable
```
```
o	sudo ufw disable
```

- การตรวจสอบสถานะของ port ที่ใช้งานอยู่ในตอนนี้
```
o	sudo ufw status
```
```
o	sudo ufw status verbose
```
Output:
<img width="185" alt="image" src="https://user-images.githubusercontent.com/88868657/225250320-100bf732-d158-405e-bd1b-72abd0103c6a.png">

- การเปิดใช้งาน port ทั้งแบบ UDP และ TCP
```
o	sudo ufw allow {PORT_NUMBER}
```
```
o	sudo ufw allow {PORT_NUMBER}/tcp
```

- การแสดงรายการตามที่ผู้ใช้งานได้เพิ่มคำสั่งข้างต้นเข้าไป
```
o	sudo ufw show added
```
Output:
<img width="220" alt="image" src="https://user-images.githubusercontent.com/88868657/225250727-91acc363-b280-4fce-8db0-bafcf8056580.png">





























