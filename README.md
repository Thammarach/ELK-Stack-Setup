# ELK-Stack-Setup
This install ELK Stack (Elasticsearch, Logstash, Kibana) on Ubuntu 22.04

Topic
[การติดตั้ง Java บน Ubuntu 20.04 LTS](https://github.com/Thammarach/ELK-Stack-Setup/edit/main/README.md#-การติดตั้ง-java-บน-ubuntu-2004-lts)
[การเปิดและปิดใช้งาน firewall ports บน Ubuntu 20.04 LTS](https://github.com/Thammarach/ELK-Stack-Setup/edit/main/README.md#-การติดตั้ง-java-บน-ubuntu-2004-lts)
[การติดตั้งซอฟแวร์ Elasticsearch บน Ubuntu 20.04 LTS](https://github.com/Thammarach/ELK-Stack-Setup/edit/main/README.md#-การติดตั้ง-java-บน-ubuntu-2004-lts)
[การติดตั้งซอฟแวร์ Logstash บน Ubuntu 20.04 LTS](https://github.com/Thammarach/ELK-Stack-Setup/edit/main/README.md#-การติดตั้ง-java-บน-ubuntu-2004-lts)
[การติดตั้งซอฟแวร์ Kibana บน Ubuntu 20.04 LTS](https://github.com/Thammarach/ELK-Stack-Setup/edit/main/README.md#-การติดตั้ง-java-บน-ubuntu-2004-lts)

## 👨‍💻 **การติดตั้ง Java บน Ubuntu 20.04 LTS**

- การเข้าใช้งานในฐานะสิทธิ์ระดับ Superuser
```
sudo -i
```

- เริ่มต้นด้วยการอัพเดทแพ็คเกจระบบ
```
sudo apt update
```

- ติดตั้งแพ็คเกจ apt-transport-https เพื่อให้สามารถเข้าถึง HTTPS
```
sudo apt install apt-transport-https
```

- ติดตั้ง OpenJDK 11 บน Ubuntu 22.04
```
java –version
```
Output:
<img width="277" alt="image" src="https://user-images.githubusercontent.com/88868657/225249069-385d0b0d-7195-4d68-8be2-e2b52a66931d.png">

- การเข้าไปกำหนดค่าใน environment หลังจากการติดตั้ง Java เสร็จสิ้น
```
sudo nano /etc/environment
```

- เมื่อเข้ามาแล้วให้นำตัวแปรด้านล่างนี้ไปวางในไฟล์ของ environment
```
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```

- โหลดไฟล์ environment โดยใช้คำสั่งต่อไปนี้
```
source /etc/environment
```

- ตรวจสอบตัวแปรหลังจากที่ได้เพิ่มลงไป
```
echo $JAVA_HOME
```
Output:
<img width="277" alt="image" src="https://user-images.githubusercontent.com/88868657/225249810-64c4c63d-5310-463d-a265-3552f168bba8.png">

## 👨‍💻 **การเปิดและปิดใช้งาน firewall ports บน Ubuntu 20.04 LTS**

- การเริ่มและหยุดใช้งาน UFW
```
sudo ufw enable
```
```
sudo ufw disable
```

- การตรวจสอบสถานะของ port ที่ใช้งานอยู่ในตอนนี้
```
sudo ufw status
```
```
sudo ufw status verbose
```
Output:
<a></a>
<img width="185" alt="image" src="https://user-images.githubusercontent.com/88868657/225250320-100bf732-d158-405e-bd1b-72abd0103c6a.png">

- การเปิดใช้งาน port ทั้งแบบ UDP และ TCP
```
sudo ufw allow {PORT_NUMBER}
```
```
sudo ufw allow {PORT_NUMBER}/tcp
```

- การแสดงรายการตามที่ผู้ใช้งานได้เพิ่มคำสั่งข้างต้นเข้าไป
```
sudo ufw show added
```
Output:
<img width="220" alt="image" src="https://user-images.githubusercontent.com/88868657/225250727-91acc363-b280-4fce-8db0-bafcf8056580.png">

## 👨‍💻 **การติดตั้งซอฟแวร์ Elasticsearch บน Ubuntu 20.04 LTS**

- ดาวน์โหลดและติดตั้งคีย์ public key
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```

- บันทึกคำจำกัดความของ directory ไปที่ /etc/apt/sources.list.d/elastic-8.x.list
```
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
```

- สามารถติดตั้ง Elasticsearch โดยใช้คำสั่งด้านล่าง ดังต่อไปนี้
```
sudo apt-get install elasticsearch
```

- คำสั่งให้ Elacticsearch เริ่มต้นทำงาน
```
sudo systemctl start elasticsearch
```

- เปิดใช้งาน Elasticsearch เมื่อระบบทำงานแล้ว
```
sudo systemctl enable elasticsearch
```

- ตรวจสอบสถานะของ Elasticsearch
```
sudo systemctl status elasticsearch
```
Output:
<img width="360" alt="image" src="https://user-images.githubusercontent.com/88868657/225253460-e34291b1-9b13-43f2-ab89-bbe01b54d319.png">

หลังจากกำหนดค่าไฟล์คอนฟิกกูเรชัน (elasticsearch.yml) แล้วจะต้องรีสตาร์ทการทำงานโดยใช้คำสั่ง ดังต่อไปนี้
```
sudo systemctl restart elasticsearch
```

- ทดสอบ Elasticsearch ด้วยการใช้คำสั่ง curl โดยจะส่งคำขอไปทาง HTTP
```
curl -X GET "localhost:9200"
```
Output:
<img width="176" alt="image" src="https://user-images.githubusercontent.com/88868657/225253917-cafe00a5-8efc-408e-ac3e-3e62dac50f19.png">

## 👨‍💻 **การติดตั้งซอฟต์แวร์ Logstash บน Ubuntu 20.04 LTS**

- สามารถติดตั้ง Logstash โดยใช้คำสั่งด้านล่าง ดังต่อไปนี้
```
sudo apt-get install logstash
```

- คำสั่งให้ Logstash เริ่มต้นทำงาน
```
sudo systemctl start logstash
```

- เปิดใช้งาน Logstash เมื่อระบบทำงานแล้ว
```
sudo systemctl enable logstash
```

- ตรวจสอบสถานะของ Logstash
```
sudo systemctl status logstash
```
Output:
<img width="277" alt="image" src="https://user-images.githubusercontent.com/88868657/225254662-9ae5f86a-9c53-4455-95ba-8403c31cf118.png">

หลังจากกำหนดค่าไฟล์คอนฟิกกูเรชัน (conf.d) แล้วจะต้องรีสตาร์ทโดยใช้คำสั่ง ดังต่อไปนี้

```
sudo systemctl restart logstash
```

## 👨‍💻 **การติดตั้งซอฟต์แวร์ Kibana บน Ubuntu 20.04 LTS**

- สามารถติดตั้ง kibana โดยใช้คำสั่งด้านล่าง ดังต่อไปนี้
```
sudo apt-get install kibana
```

- คำสั่งให้ kibana เริ่มต้นทำงาน
```
sudo systemctl start kibana
```

- เปิดใช้งาน kibana เมื่อระบบทำงานแล้ว
```
sudo systemctl enable kibana
```

- ตรวจสอบสถานะของ kibana
```
sudo systemctl status kibana
```
Output:
<img width="277" alt="image" src="https://user-images.githubusercontent.com/88868657/225255532-f4aaffb5-d78a-42c5-811c-649e50f38362.png">

หลังจากกำหนดค่าไฟล์คอนฟิกกูเรชัน (kibana.yml) แล้วต้องรีสตาร์ทโดยใช้คำสั่ง ดังต่อไปนี้

```
sudo systemctl restart kibana
```

















