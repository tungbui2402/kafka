# Kafka
## I. Khái niệm
Kafka là một hệ thống phân tán và một nền tảng xử lý dòng thông tin (stream processing) mã nguồn mở được phát triển bởi Apache Software Foundation. Nó được thiết kế để xử lý dữ liệu dòng (stream data) trong thời gian thực và có khả năng xử lý lượng dữ liệu lớn và độ trễ thấp.
Kafka được thiết kế dựa trên mô hình publish-subscribe (xuất bản-đăng ký) và sử dụng kiến trúc phân tán. Nó cung cấp một hệ thống hàng đợi tin nhắn phân tán (distributed message queue) và lưu trữ thông điệp dưới dạng log có thứ tự (ordered log). Mô hình này cho phép các ứng dụng gửi thông điệp (producer) và nhận thông điệp (consumer) từ các chủ đề (topics) khác nhau.
## II. Một số đặc điểm quan trọng của Kafka
- Khả năng mở rộng: Kafka có thể mở rộng dễ dàng bằng cách thêm các máy chủ (broker) vào cụm Kafka để xử lý lượng dữ liệu lớn và đáp ứng yêu cầu cao.
- Bảo đảm tin cậy: Kafka giữ được sự tin cậy thông qua việc sao lưu dữ liệu và duy trì độ tin cậy và bất biến của thông điệp.
- Xử lý dòng thông tin (stream processing): Kafka hỗ trợ xử lý dòng thông tin và tích hợp dữ liệu từ nhiều nguồn, cho phép xử lý dữ liệu theo thời gian thực và ứng dụng các luồng xử lý phức tạp trên dòng thông tin.
- Hỗ trợ cho nhiều ngôn ngữ và các công cụ xử lý dữ liệu: Kafka cung cấp các API cho nhiều ngôn ngữ lập trình, cho phép phát triển ứng dụng sử dụng Kafka bằng các ngôn ngữ phổ biến như Java, Python, và C++. Ngoài ra, Kafka tích hợp tốt với các công cụ xử lý dữ liệu như Apache Spark, Apache Storm và Apache Flink.
## III. Mô hình kafka
- Broker: Kafka được triển khai dưới dạng một cụm (cluster) gồm nhiều broker. Mỗi broker là một máy chủ Kafka độc lập có khả năng xử lý và lưu trữ thông điệp. Cụm Kafka có thể có nhiều broker để tăng khả năng mở rộng và đảm bảo sự tin cậy.
- Topic: Topic là một loại chủ đề hoặc một danh mục trong Kafka. Mỗi thông điệp trong Kafka được gán vào một topic cụ thể. Các producer (nhà sản xuất) gửi thông điệp tới các topic và các consumer (người tiêu thụ) đọc thông điệp từ các topic này. Một topic có thể có nhiều partition.
- Partition: Mỗi topic trong Kafka có thể được chia thành nhiều partition. Partition là một đơn vị lưu trữ dữ liệu được phân tán trên các broker. Mỗi partition duy trì một log có thứ tự của các thông điệp. Partition cho phép tăng khả năng mở rộng và xử lý song song của Kafka.
- Producer: Producer là thành phần tạo và gửi thông điệp tới các topic trong Kafka. Producer quyết định vào topic nào thông điệp sẽ được gửi và chịu trách nhiệm đảm bảo thông điệp đến được Kafka và được lưu trữ trong partition tương ứng.
- Consumer: Consumer là thành phần đọc và xử lý các thông điệp từ các topic trong Kafka. Một consumer có thể đăng ký để đọc từ một hoặc nhiều topic. Các consumer có thể tiêu thụ thông điệp theo mô hình pull (khi họ tự yêu cầu thông điệp) hoặc mô hình push (khi Kafka đẩy thông điệp tới consumer).
- Consumer Group: Consumer group là một nhóm các consumer có cùng group ID được tổ chức lại trong Kafka. Khi một consumer group đăng ký vào một topic, các partition của topic đó sẽ được chia đều giữa các consumer trong group. Điều này cho phép mỗi consumer trong group xử lý một phần dữ liệu độc lập và tăng khả năng mở rộng.
- ZooKeeper: ZooKeeper là một hệ thống quản lý và cung cấp các dịch vụ phân tán cho Kafka. ZooKeeper giúp quản lý trạng thái của các broker, consumer group và topic. Nó cũng cung cấp các thông tin về metadata và giám sát hệ thống Kafka.
### Tổng quan, mô hình Kafka bao gồm các broker, topic, partition, producer, consumer, consumer group và ZooKeeper. Đây là các thành phần cốt lõi trong kiến trúc Kafka và cho phép xử lý và quản lý dòng thông tin (stream data) một cách phân tán, mở rộng và tin cậy.
## IV. Hoạt động của Kafka
Kafka hoạt động theo cơ chế publish-subscribe, trong đó producer gửi thông điệp tới các topic và consumer nhận và xử lý các thông điệp từ các topic đó.

Producer:
- Producer tạo ra các thông điệp và gửi chúng tới Kafka.
- Producer quyết định thông điệp sẽ được gửi tới topic nào.
- Nếu có nhiều partition trong topic, producer có thể chọn gửi thông điệp tới một partition cụ thể hoặc để Kafka tự động chọn partition dựa trên một thuật toán xác định.

Topic và Partition:
- Mỗi topic trong Kafka được chia thành nhiều partition để xử lý và lưu trữ dữ liệu một cách phân tán.
- Mỗi partition là một log có thứ tự của các thông điệp. Mỗi thông điệp được gán một offset duy nhất trong partition.
- Partition cho phép Kafka mở rộng và xử lý dữ liệu song song, và các producer có thể gửi thông điệp đến các partition khác nhau một cách độc lập.

Consumer và Consumer Group:
- Consumer đăng ký để đọc các thông điệp từ các topic.
- Các consumer có thể đọc từ một hoặc nhiều topic và có thể thuộc vào một consumer group.
- Khi một consumer group đăng ký vào một topic, các partition của topic đó sẽ được chia đều giữa các consumer trong group.
- Mỗi consumer trong group đọc từ một subset của partition, đảm bảo xử lý dữ liệu song song và khả năng mở rộng.

ZooKeeper:
- ZooKeeper được sử dụng bởi Kafka để quản lý trạng thái của các broker, consumer group và topic.
- ZooKeeper giám sát và duy trì metadata của Kafka, bao gồm thông tin về các topic, partition, offset và consumer group.
- ZooKeeper đảm bảo tính nhất quán và tin cậy trong việc quản lý Kafka và giúp điều phối các hoạt động của producer và consumer.

Xử lý dòng thông tin (Stream Processing):
- Kafka cung cấp các công cụ và thư viện để xử lý dòng thông tin (stream processing).
- Các công cụ như Apache Spark, Apache Flink và Kafka Streams cho phép xử lý dữ liệu trong thời gian thực từ Kafka và thực hiện các phân tích, biến đổi và tính toán trên dữ liệu.

Kafka hoạt động bằng cách cho phép producer gửi thông điệp tới các topic và consumer nhận và xử lý thông điệp từ các topic đó. Với cơ chế publish-subscribe, Kafka cung cấp khả năng xử lý dòng thông tin, mở rộng và tin cậy trong các hệ thống xử lý dữ liệu phân tán và thời gian thực.

# Kafka cluster
## I. Khái niệm
Một Kafka cluster (cụm Kafka) là một nhóm các máy chủ Kafka được cấu hình và kết nối với nhau để tạo thành một hệ thống Kafka phân tán. Cluster Kafka cho phép mở rộng khả năng xử lý và lưu trữ của Kafka bằng cách chia sẻ công việc giữa nhiều broker.
## II. Các thành phần trong kafka cluster
- Broker: Mỗi broker là một máy chủ Kafka độc lập trong cụm. Mỗi broker chịu trách nhiệm lưu trữ và xử lý một phần dữ liệu của các topic trong Kafka. Cluster Kafka có thể có một hoặc nhiều broker, và các broker giao tiếp với nhau để đồng bộ dữ liệu và phân chia công việc.
- Controller: Trong một cụm Kafka, một broker được chọn làm Controller. Controller là trung tâm quản lý trong cụm và giữ trạng thái của các partition và replica. Nhiệm vụ của Controller bao gồm quản lý sự gán kết của partition cho các broker, điều phối việc sao lưu và nhân bản dữ liệu, và xử lý các sự kiện xảy ra trong cụm.
- ZooKeeper: Kafka sử dụng ZooKeeper để lưu trữ thông tin metadata và quản lý tình trạng của cụm. ZooKeeper giúp các broker và Controller trong cụm Kafka tương tác và đồng bộ hoạt động. Tuy nhiên, từ phiên bản Kafka 2.8.0 trở đi, ZooKeeper không còn là một yêu cầu bắt buộc, và Kafka có thể hoạt động với một quản lý metadata nội bộ (internal metadata management).
- Replication: Kafka sử dụng cơ chế nhân bản (replication) để đảm bảo tính nhất quán và tin cậy của dữ liệu. Mỗi partition trong Kafka có thể có nhiều replica, trong đó một replica chính (leader replica) xử lý yêu cầu ghi và đọc, trong khi các replica sao lưu (follower replicas) duy trì bản sao của dữ liệu. Cơ chế nhân bản giúp đảm bảo sự mất mát dữ liệu khi một broker hoặc replica gặp sự cố.

Khi một Kafka cluster được thiết lập và hoạt động, producer có thể gửi thông điệp tới các topic, các broker trong cụm Kafka nhận và lưu trữ thông điệp trong các partition tương ứng, và consumer có thể đọc và xử lý thông điệp từ các topic. Controller và ZooKeeper giữ vai trò quan trọng trong việc quản lý và đồng bộ hoạt động của cụm Kafka. Việc sử dụng Kafka cluster cho phép mở rộng khả năng xử lý và lưu trữ, đảm bảo tính sẵn sàng và tin cậy, và tăng cường khả năng mở rộng của hệ thống Kafka trong việc xử lý dữ liệu dòng thông tin.
## III. Các mô hình 
Có hai mô hình chính khi triển khai Kafka cluster là standalone (đơn lẻ) và distributed (phân tán).

Kafka Cluster Standalone (Đơn lẻ):
- Mô hình standalone là một cấu hình đơn giản, trong đó chỉ có một broker Kafka hoạt động độc lập.
- Mô hình này thích hợp cho các ứng dụng nhỏ hoặc trong môi trường phát triển và thử nghiệm.
- Standalone Kafka cluster không sử dụng ZooKeeper để quản lý metadata và không có khả năng nhân bản hoặc phân chia công việc.

Kafka Cluster Distributed (Phân tán):
- Mô hình phân tán là một cấu hình mạnh mẽ hơn, bao gồm nhiều broker Kafka hoạt động cùng nhau trong một cụm.
- Mô hình này cho phép mở rộng khả năng xử lý, lưu trữ và đảm bảo tính sẵn sàng cao hơn.
- Kafka cluster phân tán sử dụng ZooKeeper để quản lý metadata, theo dõi trạng thái và điều phối các hoạt động giữa các broker.
- Các partition trong các topic được chia đều giữa các broker, và mỗi broker quản lý một hoặc nhiều partition.

Trong mô hình phân tán, Kafka cung cấp tính năng tự động nhân bản (replication) và điều phối (balancing) dữ liệu giữa các broker. Việc sử dụng Kafka cluster phân tán giúp tăng khả năng mở rộng, tính sẵn sàng cao và khả năng xử lý song song trong hệ thống xử lý dữ liệu dòng thông tin. Một Kafka cluster có thể có hàng chục hoặc hàng trăm broker, tùy thuộc vào quy mô và yêu cầu của ứng dụng. Sự lựa chọn giữa mô hình standalone và mô hình phân tán phụ thuộc vào quy mô, hiệu suất, tin cậy và yêu cầu của hệ thống.
## IV. Setup Kafka
Bước 1: Tạo 1 user là kafka:
```
sudo adduser kafka
sudo adduser kafka sudo
```
Sau đó đăng nhập vào tài khoản kafka: `su -l kafka`.
Bước 2: Tải và giải nén Kafka Binaries:
- Tạo 1 folder có tên là download: `mkdir ~/Downloads`.
- Tải kafka binaries về máy: `curl "https://downloads.apache.org/kafka/2.8.2/kafka_2.13-2.8.2.tgz" -o ~/Downloads/kafka.tgz`.
- Tạo thêm folder kafka: `mkdir ~/kafka && cd ~/kafka`.
- Giải nén file vừa tải về: `tar -xvzf ~/Downloads/kafka.tgz --strip 1`.

Bước 3: Cấu hình máy chủ kafka:
- Mở tệp server.properties: `nano ~/kafka/config/server.properties`.
- Thêm dòng sau vào cuối đoạn: `delete.topic.enable = true`.
- Tiếp đến tìm đến dòng `log.dirs` sau đó sửa từ dấu - về thành dấu / rồi lưu và thoát khỏi nano.

Bước 4: Cấu hình zookeeper và kafka.service:
- Tạo file zookeeper: `sudo nano /etc/systemd/system/zookeeper.service`
- Thêm vào file đoạn sau:
```
[Unit]
Requires=network.target remote-fs.target
After=network.target remote-fs.target

[Service]
Type=simple
User=kafka
ExecStart=/home/kafka/kafka/bin/zookeeper-server-start.sh /home/kafka/kafka/config/zookeeper.properties
ExecStop=/home/kafka/kafka/bin/zookeeper-server-stop.sh
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```
- Tạo file kafka.service: `sudo nano /etc/systemd/system/kafka.service`
- Thêm vào file đoạn sau:
```
[Unit]
Requires=zookeeper.service
After=zookeeper.service

[Service]
Type=simple
User=kafka
ExecStart=/bin/sh -c '/home/kafka/kafka/bin/kafka-server-start.sh /home/kafka/kafka/config/server.properties > /home/kafka/kafka/kafka.log 2>&1'
ExecStop=/home/kafka/kafka/bin/kafka-server-stop.sh
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```
- Sau khi thêm 2 dòng vào config thì chúng ta chạy kafka: `sudo systemctl start kafka`
- Kiểm tra tình trạng kafka: `sudo systemctl status kafka`
- Tiếp theo chạy zookeeper: `sudo systemctl enable zookeeper`
- Hiện thông báo `Created symlink /etc/systemd/system/multi-user.target.wants/zookeeper.service → /etc/systemd/system/zookeeper.service.` là thành công.
- Tiếp theo chạy lệnh: `sudo systemctl enable kafka`
- Hiện thông báo `Created symlink /etc/systemd/system/multi-user.target.wants/kafka.service → /etc/systemd/system/kafka.service.` là thành công.

Bước 5: Test:
Chạy thử theo link bên dưới:
```
https://www.digitalocean.com/community/tutorials/how-to-install-apache-kafka-on-ubuntu-20-04
```
