# SPCN-011
ขั้นตอนการใช้งานของสร้าง vm and ct on Proxmox cluster

1) Create master vm [ ubuntu-22.04 ]
   - สร้าง master vm มา 1 ตัว แล้วทำการ set ค่าพื้นฐานต่างๆ
   - เช็คเวลาด้วย dateและset update time ด้วยคำสั่ง sudo timedatectl set-timezone Asia/Bangkok
   - ทำการเปิดใช้งาน ip qemu ด้วยคำสั่ง
       - sudo -i
       - apt update
       - apt install qemu-guest-agent
       - systemctl enable qemu-guest-agent
       - และทำการตั้งค่าที่ option ให้เปิดใช้งานตัว Qemu guest agent เป็น Enable 
       ![2](https://user-images.githubusercontent.com/98762543/208230564-e33c99a7-dabe-40c8-938b-bda6167a041e.PNG)
       - reboot เพื่อรีระบบ
   1.1) clone from template 2 vm
   - Click ที่ vm(master) > Convert to template
   -  หลังจาก vm(master) กลายเป็นtemplate ให้ Click vm แล้วเลือก Clone เป็นตัวvmใหม่2ตัว
   
      ![3](https://user-images.githubusercontent.com/98762543/208230565-6e502090-a56b-45cd-8f72-eeccd36f0897.PNG)
   - ทำการsetระบบโดย
        - date เพื่อเช็ค timezone
          ![4](https://user-images.githubusercontent.com/98762543/208230566-8f36023a-d774-4257-b0f1-f5089ddef9d6.PNG)
        - ทำการเปลี่ยนipของระบบเพื่อไม่ให้ipซ้ำกันโดย
            - sudo -i
            - rm /var/lib/dbus/machine-id
            - nano /etc/machine-id เพื่อลบ id เก่าออก
            - ln -s /etc/machine-id /var/lib/dbus/machine-id เพื่อ link เชื่อมต่อกับ machine-id
            - reboot เพื่อรี ip ใหม่
            - หลังเปลี่ยน ip clone1
              ![5](https://user-images.githubusercontent.com/98762543/208230567-3dbdc66d-a18d-4ce6-8b29-9ca426005766.PNG)
            - หลังเปลี่ยน ip clone2
              ![6](https://user-images.githubusercontent.com/98762543/208230568-c0012667-511e-48dc-ad40-2b89729e2bfe.PNG)
 
2) create vm from other os
   - Create VM จากนั้นทำการตั้งค่าที่กำหนดโดยระบบปฏิบัติการที่เลือกใช้คือ Linux Mint
      - Summary ของ Linux Mint
       ![7](https://user-images.githubusercontent.com/98762543/208230569-5d6f113e-d440-4c16-8d8e-cc60f2243d78.PNG)
      - หน้า console screen
       ![8](https://user-images.githubusercontent.com/98762543/208230570-a0e6545c-8805-4bde-ac61-20d5c0107594.PNG)

3) create container template 
   - Click create container template เพื่อสร้าง CT
      - Summary 
        ![9](https://user-images.githubusercontent.com/98762543/208230571-43c9de55-65ed-462f-a928-32199a68885d.PNG)
      - console screen 
        ![10](https://user-images.githubusercontent.com/98762543/208230572-eae4cc55-1824-45d3-8efd-ca68cd5c8484.PNG)
