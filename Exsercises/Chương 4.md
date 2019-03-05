Bài 1: Dùng một dòng lệnh chạy container centos version mới nhất đồng thời in ra màn hình các ổ đĩa và dung lượng nó đang sử dụng cũng như đang trống

+ Chạy centos 

  ```bash
  > docker run -ti --rm centos bash
  ```

+ Kiểm tra dung lượng ổ đĩa

  ```bash
  > df -h
  ```


Bài 2: Chạy một container centos ở version 6 dưới dạng detach ở terminal thứ nhất, và cho phép sử dụng 256mb bộ nhớ. Mở terminal thứ 2 và attach container. In ra danh sách các file và folder ở thư mục "/" vào file "/tmp/list.txt. Quay lại terminal thứ nhất để kiểm tra file vừa tạo có tồn tại không.

+ Chạy centos version 6 dưới dang detach và giới hạn bộ nhớ là 256mb
  ```bash
  > docker run -ti -d -m 256M centos:6 bash
  ```

+ Tạo terminal mới và chạy
  ```bash
  > docker attach [CONTAINER_ID]
  ```

+ In danh sách folder ra file /tmp/list.txt
  ```bash
  > echo $(ls) >/tmp/list.txt
  ```

+ Quay lại container lúc đầu và kiểm tra file vừa tạo tồn tại chưa


Bài 3: Tạo một mạng tên là comcast, chạy container ubuntu version 16.04 thuộc mạng comcast và cài đặt netcat cho container này. Tạo container thứ 2 và để container thứ 2 nằm cùng mạng với container thứ nhất. Truyền tin "Setup complete" từ container thứ 2 qua container thứ nhất sử dụng netcat

+ Tạo network comcast

  ```bash
  > docker network create comcast
  ```

+ Tạo container server và cài netcat
  ```bash
  > docker run -ti --rm --net=comcast --name server ubuntu:16.04 bash
  > apt-get update && apt-get install -y netcat
  > nc -lvkp 111
  ```

+ Tạo container client và cài netcat
  ```bash
  > docker run -ti --rm --net=comcast --link server --name client ubuntu:16.04 bash
  > apt-get update && apt-get install -y netcat
  > nc server 111
  ```
  