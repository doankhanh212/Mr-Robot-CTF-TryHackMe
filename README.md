# Mr-Robot-CTF-TryHackMe

scan 

<img width="1244" height="682" alt="image" src="https://github.com/user-attachments/assets/0bce56da-7a36-4d30-a9f9-3a9597f92cbd" />

enumerating

└─$ gobuster dir -u http://10.201.126.52/ -w /usr/share/wordlists/dirb/common.txt

<img width="1085" height="785" alt="image" src="https://github.com/user-attachments/assets/474ac84e-f2f7-486f-b1ba-d65f953568c5" />

khi mà tôi truy cập thử các đường dẫn thì phát hiện file này chứa gợi ý tệp cờ 1 và 1 tệp gì đó

<img width="730" height="474" alt="image" src="https://github.com/user-attachments/assets/814d0229-4633-4909-99cb-57c84561b07e" />

<img width="697" height="414" alt="image" src="https://github.com/user-attachments/assets/cc044c02-dec1-43d3-92d6-144833223045" />

cờ 1 : 073403c8a58a1f80d943455fb30724b9

sau đó tôi lưu tất cả vào 1 file fsocity.dic

<img width="857" height="839" alt="image" src="https://github.com/user-attachments/assets/9f9d2c93-c3c6-473b-9186-0f146e48f8b7" />

sau đó tôi chuyển hướng đến trang /license phát hiện ra 1 mã base64 ở cuối trang web

ZWxsaW90OkVSMjgtMDY1Mgo=

<img width="1133" height="597" alt="image" src="https://github.com/user-attachments/assets/8f37c6cd-320c-499a-aa02-80c31a85da05" />

dường như nó rất giống username:password

<img width="1262" height="852" alt="image" src="https://github.com/user-attachments/assets/754c7692-fbaf-422d-90f7-6fd7e6f286b5" />

chính xác là vậy rồi 

chuyển hướng đến Appearance - Editor - 404 Template

xóa toàn bộ và thêm mã reverse shell vào và update file 

trên máy kali chạy trình lắng nghe netcat

sau đó mở đường dẫn http://10.201.126.52/wp-includes/themes/TwentyFifteen/404.php

vậy là chúng ta đã có được shell nhưng tôi chưa có quyền đọc cờ 2 

<img width="1076" height="530" alt="image" src="https://github.com/user-attachments/assets/b7b01439-21d6-4aba-b88f-009cbd84c238" />

nhưng chúng ta có 1 tệp thú vị tôi thử đọc nó 

robot:c3fcd3d76192e4007dfb496cca67e13b

<img width="539" height="89" alt="image" src="https://github.com/user-attachments/assets/d7612dc5-8fa3-4bf5-b04a-f0f29c56f05f" />

có vẻ như đây là người dùng có thể đọc được tệp cờ 2 

tôi lưu mật khẩu được mã hóa đó thành hash

sử dụng lệnh john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash 

<img width="909" height="235" alt="image" src="https://github.com/user-attachments/assets/88551864-3ba2-4b13-b3b2-0ae54fcda1cc" />

và tôi đã có được pass abcdefghijklmnopqrstuvwxyz

quay lại shell tôi nhập lệnh su robot và lấy cờ 2

<img width="539" height="228" alt="image" src="https://github.com/user-attachments/assets/69609003-5796-4578-b63a-93e4698e7fe3" />

sau đó tôi tìm cách leo lên quyền root 

find / -perm -4000 2>/dev/null

<img width="696" height="396" alt="image" src="https://github.com/user-attachments/assets/86358274-4d4f-4e1f-a73d-cf4b998b0d9b" />

tìm thấy đường dẫn file nmap 

sử dụng GTFOBins để tìm cách 

<img width="1216" height="664" alt="image" src="https://github.com/user-attachments/assets/ef902c50-8d9c-42e8-8a47-7b8da7b8214b" />

nmap --interactive

!sh

<img width="508" height="186" alt="image" src="https://github.com/user-attachments/assets/58382ec9-9546-415b-87bf-44ac1fe04456" />

vậy là đã có được quyền root 

<img width="487" height="173" alt="image" src="https://github.com/user-attachments/assets/47a6282b-3944-421c-add0-7c834c7bc9db" />

vậy là đã có được cờ 3 
