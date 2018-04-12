- nginx配置
```
server {
    listen 80;
    server_name vipop.cc;
    root "/vagrant/www/vip-operate";
    index index.html index.php;

    location / {
        #try_files $uri $uri/ /index.php?$query_string;
        try_files $uri $uri/ /index.php?s=$uri&$args;		## 注意这里
    }

    location ~ \.php$ {
        root "/vagrant/www/vip-operate";					## 这个也添加上去吧，默认是不用添加的
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
        #try_files $uri /index.php =404;
        #fastcgi_split_path_info ^(.+\.php)(/.+)$;
    }
}


```
