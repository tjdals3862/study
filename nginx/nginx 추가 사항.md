



##### reverse proxy

```
일반적으로 DMZ에 배치되어 인터넷 사용자에 의한 공격으로부터 내부 서버를 보호하는 보안 기능을 수행함으로써 회사 인트라넷 등의 http 서버를 보호하는 보안 장치
```



reverse proxy의 장점

1. 서버의 부하를 덜어줄수 있는 로드 밸런싱 처리
2.  각 서버의 부하를 덜어준 만큼 웹서버 속도 증대
3. 보안과 익명성
4. 중앙 집중식 log 작성과 감시
5. 캐쉬 사용

[![diagram002](http://akal.co.kr/wordpress/wp-content/uploads/2016/05/diagram002.png)](http://akal.co.kr/wordpress/wp-content/uploads/2016/05/diagram002.png)

```
하위 웹서버에 apache와 tomcat을 이용하여 예제 진행
```

[![diagram003](http://akal.co.kr/wordpress/wp-content/uploads/2016/05/diagram003.png)](http://akal.co.kr/wordpress/wp-content/uploads/2016/05/diagram003.png)

reverse proxy 예시

```
목적 : 하나의 IP로 각각 다른 도메인을 이용하여 여러개의 페이지사용

환경 구성
nginx : 80 apache : 8080 tomcat : 8888 
앞단에 nginx 뒷단에 apache, tomcat(tomcat은 vhost를 이용하여 2가지 도메인 사용)

test 진행을 위해
localhost에 172.16.120.20 nginx.com, apachetest.com, tomcat1.com tomcat2.com 등록

각 도메인 별 document Root와 index page 생성
mkdir /var/www/nginx
mkdir /var/www/apache
mkdir /var/www/tomcat1
mkdir /var/www/tomcat2

```



apache reverse proxy

```nginx
vi /etc/nginx/sites-available/apache.conf
server {
        listen 80;
      
        index index.php index.html index.htm index.nginx-debian.html; 
      
      server_name apachetest.com; // apache로 접근할 도메인
      
        location / {
                proxy_pass http://172.16.120.60:8080;  //apache port
            	proxy_set_header X-Real-IP $remote_addr;
        		 #실제 접속자의 IP를 X-Real-IP 헤더에 입혀서 전송
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $http_host;
            	set_real_ip_from 172.16.120.60;
        		# nginx server IP
            	real_ip_header	X-Forwarded-For;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        }      
}

ln -s /etc/nginx/sites-available/apache.conf /etc/nginx/site-enabled/apache.conf
systemctl restart nginx //서비스 재시작

apachetest.com으로 주소를 요청하게 되면 http://172.16.120.20:8080로 클라이언트의 요청을 보낸다.

```



tomcat reverse proxy

```nginx
vi /etc/nginx/sites-available/tomcat1.conf and tomcat2.conf

server {
        listen 80;
       
        index index.php index.html index.htm index.nginx-debian.html index.jsp;

        server_name tomcat1.com; //tomcat으로 접근할 도메인 

        location / {
                proxy_pass http://172.16.120.60:8888; #tomcat port 지정
                proxy_set_header X-Real-IP $remote_addr;
        		 #실제 접속자의 IP를 X-Real-IP 헤더에 입혀서 전송
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $http_host;
        }
}

ln -s /etc/nginx/sites-available/tomcat1.conf /etc/nginx/site-enabled/tomcat1.conf
ln -s /etc/nginx/sites-available/tomcat2.conf /etc/nginx/site-enabled/tomcat2.conf
systemctl restart nginx //서비스 재시작
```

![1590386002702](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1590386002702.png)



![1590386043512](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1590386043512.png)





![1590386076666](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1590386076666.png)

![1590386095039](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1590386095039.png)





IP 접근 제어

```
server {
	listen 80;
	server_name nginx.com;
	
	location / {
		deny 172.16.100.0/24;
		allow 172.16.0.0/16;
		deny all;
	}
}

172.16.100.0 의 회사 사내 ip에 대해 차단 후
172.16.100.0/24의 대역을 제외한 172.16.0.0의 모든 대역 허용 후 그 외 모든 ip 차단

```



접근 거부 IP로 서버에 접근할 경우

![1590386669909](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1590386669909.png)



```nginx
vi /etc/nginx/site-available/nginx.conf
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        
   		index index.php index.html index.htm index.nginx-debian.html;
        root /var/www/nginx;
        
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
                }
       }
```



```nginx
vi /etc/nginx/site-available/nginx2.conf
server {
        listen 80;

        index index.php index.html index.htm index.nginx-debian.html;

        root /var/www/nginx2;
        server_name nginx2.com;
        location / {
        
        set_real_ip_from 172.16.120.50;
        real_ip_header  X-Forwarded-For;
        access_log /var/log/nginx/nginx2.com.log;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.1-fpm.sock;
        }
}
```

















![1592442882664](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592442882664.png)







![1592442884492](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592442884492.png)







```nginx
vi /etc/nginx/nginx.conf
		gzip on;
        gzip_disable "msie6";    
        gzip_static on;
        gzip_vary on; #vary 헤더
        gzip_min_length 0; #파일 용량에 상관 없이 모두  압축
        gzip_proxied any;
        gzip_comp_level 6; # 텍스트 압축 레벨 1-9
        gzip_buffers 16 8k;
        gzip_types   text/plain text/css text/javascript text/xml
             application/javascript application/json application/x-javascript
             application/xml application/xml+rss
             image/svg+xml image/svg;
```



```nginx
http {
  server {
    location / {
      root /path/to/html ;
    }
    location /images/ {
      root /path/to/image ;
    }
  }
}
```



```http
bizspring@ubuntu:/var/log/apache2$ tail -100f other_vhosts_access.log
172.16.208.1  172.16.120.50 - - [18/Jun/2020:10:22:40 +0900] "GET / HTTP/1.0" 200 496 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.97 Safari/537.36"
172.16.208.1  172.16.120.50 - - [18/Jun/2020:11:44:50 +0900] "GET / HTTP/1.0" 200 496 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.97 Safari/537.36"
172.16.208.1  172.16.120.50 - - [18/Jun/2020:11:44:51 +0900] "GET /favicon.ico HTTP/1.0" 404 456 "http://apachetest.com/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.97 Safari/537.36"
```







```nginx
nginx
location / {
                proxy_pass http://172.16.120.60:8080;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        set_real_ip_from 172.16.120.50;
        real_ip_header  X-Forwarded-For;
        access_log /var/log/nginx/apachetest.com.log;
        }

apache
LogFormat "%{X-Forwarded-For}i  %h %l %u %t \"%r\" %>s %O \"%{Referer}i\" \"%{User-Agent}i\"" vhost_combined

tomcat
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log." suffix=".txt"
               pattern="%{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b %{User-Agent}i" />
```

