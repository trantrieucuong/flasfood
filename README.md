Helo thầy và các bạn lớp agile và các bạn nhóm 6
Em tên là Trần Triều Cường


Em sẽ giới thiệu sơ qua 1 chút công nghê em đang sử dụ
em đang áp dụng vào dự án là mô hình phát triển bằng agile (Em bám theo các takl t5rong trello để code các chức năng.(Và lần lượt tiền hành ghép vào fe (template sẵn)))

Công nghệ em sử dụng là java spring boot hibernate and thymeleaf (cơ bản) 
Cần chuẩn bị jdk 11, docker, mysql 

Cách Chạy dự án: 
Bước 1 clone dự án về
Bước 2: Chuẩn bị ket như bên dưới
Bước 3: ./mvnw spring-boot:run


Cách tải kit 
jdk 11: https://www.oracle.com/vn/java/technologies/javase/jdk11-archive-downloads.html

Cài đặt Portainer (optional - công cụ quản lý container trên giao diện)

docker run -d -p 8000:8000 -p 9443:9443 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.9.3
Cài đặt MySQL

// 1. Tạo volume
docker volume create mysql-volume

// 2. Tạo container
docker run -d --name mysql-container -p 3306:3306 -v mysql-volume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123 mysql:latest
Account truy cập

username : root
password : 123
Cài đặt phpAdmin

// 1. Tạo volume
docker volume create phpmyadmin-volume

// 2. Tạo container
docker run -d --name phpmyadmin-container -v phpmyadmin-volume:/etc/phpmyadmin/config.usr.inc.php --link mysql-container:db -p 82:80 phpmyadmin/phpmyadmin:latest
Chú ý khi khởi tạo container phpMyAdmin cần link đến container MySQL đang chạy thông qua tên của container

Docker image tham khảo

MySQL : https://hub.docker.com/_/mysql
phpMyAdmin : https://hub.docker.com/r/phpmyadmin/phpmyadmin/
Cài đặt MySQL và phpMyAdmin sử dụng docker compose
Tạo network

docker network create mysql
File docker-compose.yml

version: "3.8"

services:
    # MySQL
    db:
        image: mysql:latest
        volumes:
            - db_data:/var/lib/mysql
        restart: always
        ports:
            - "3306:3306"
        environment:
            MYSQL_ROOT_PASSWORD: 123
        networks:
            - mysql
    # phpmyadmin
    phpmyadmin:
        depends_on:
            - db
        image: phpmyadmin/phpmyadmin:latest
        restart: always
        ports:
            - "82:80"
        environment:
            PMA_HOST: db
            MYSQL_ROOT_PASSWORD: 123
        networks:
            - mysql
networks:
    mysql:
volumes:
    db_data:




 Lời sau cuối xin cảm ơn thầy cô và các bạn ! Chúc các bạn thành công

  


Cuongdji : http://cuongvovanhoa.com/ 
