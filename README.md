 تحليل حركة مرور شبكة مشبوهة باستخدام Wireshark
🧪 نظرة عامة
يهدف هذا التقرير إلى تحليل ملف حركة مرور شبكة (PCAP) يحتوي على نشاط مشبوه، باستخدام أداة Wireshark. من خلال تطبيق فلاتر محددة وتحليل بروتوكولات DHCP وNBNS وHTTP، تم تحديد جهاز Windows مصاب بنشاط خبيث، بالإضافة إلى الاتصالات التي قام بها.

🔧 الأدوات المستخدمة
Wireshark

VirusTotal

🧵 خطوات التحليل
1. 🔎 تحديد عنوان IP وMAC واسم المضيف للجهاز المشبوه
من خلال تحليل الحزم باستخدام بروتوكولات NBNS وDHCP، تم التعرف على بيانات الجهاز المصاب:

عنوان IP: 192.168.137.83

عنوان MAC: 00:21:9b:5b:d1:7a

اسم الجهاز (Hostname): PYNDRINE-PC

تم الحصول على هذه المعلومات من الحزمة رقم 17 و33 باستخدام الفلاتر:




nbns
udp.port == 67
2. 📡 تحليل الطلبات الصادرة عبر HTTP
باستخدام الفلتر http.request، تم رصد نشاط HTTP غير معتاد صادر من الجهاز PYNDRINE-PC. وقد لوحظت عدة طلبات إلى خوادم قد تكون مشبوهة:


تم التعرف على هذه الطلبات من خلال الحزم التي تظهر في الصورة الخاصة بـ http.request

📌 النتائج
تم تحديد جهاز Windows مصاب عنوانه: 192.168.137.83 واسمه PYNDRINE-PC

الجهاز أجرى طلبات HTTP إلى عدة خوادم مشبوهة

أحد الطلبات كان لتحميل ملف ml1from2.tar من عنوان خارجي، مما يرجّح احتمال تحميل برمجية خبيثة

بعض الطلبات تضمنت عناوين فرعية تبدو مشابهة لخدمات Microsoft، مما قد يدل على محاولة تضليل






Suspicious Network Traffic Analysis using Wireshark
🧪 Overview
This report aims to analyze a PCAP file containing suspicious network activity using Wireshark. By applying specific filters and analyzing the DHCP, NBNS, and HTTP protocols, we were able to identify a compromised Windows machine and investigate the connections it made.

🔧 Tools Used
Wireshark

VirusTotal

🧵 Analysis Steps
1. 🔎 Identifying the IP, MAC Address, and Hostname of the Suspected Device
Through analysis of NBNS and DHCP packets, the following information about the suspected device was identified:

IP Address: 192.168.137.83

MAC Address: 00:21:9b:5b:d1:7a

Hostname: PYNDRINE-PC

This information was extracted from packets #17 and #33 using the following filters:

wireshark
نسخ
تحرير
nbns
udp.port == 67
2. 📡 Analyzing Outgoing HTTP Requests
Using the http.request filter, unusual HTTP traffic was observed originating from the device PYNDRINE-PC. Several requests were directed to potentially suspicious servers.

These requests were identified in the packets shown in the http.request filtered view.

📌 Key Findings
A compromised Windows machine was identified with IP address: 192.168.137.83 and hostname: PYNDRINE-PC.

The device made HTTP requests to multiple suspicious servers.

One request attempted to download a file named ml1from2.tar from an external IP address, which suggests a potential malware download.

Some requests were made to subdomains that mimic legitimate Microsoft services, likely as an evasion technique.
