nginx配置
```
server {
    listen 80;
    server_name vipoperate.test;
    location / {
        root "/code/vip-operate"; # 你的 TP 框架 index.php 所在目录, 记得用 / 分割路径
        index index.php index.html index.htm;
        try_files $uri $uri/ /index.php?s=$uri&$args; # 核心
    }
    # ...
    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    location ~ \.php$ {
        root "/code/vip-operate";   # 你的 TP 框架 index.php 所在目录, 记得用 / 分割路径
        fastcgi_pass unix:/var/run/php/php7.1-fpm.sock;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}

-------


server {
    listen 80;
    server_name vipop.cc;

    location / {
        root "/vagrant/www/vip-operate";
        index index.php index.html index.htm;
        try_files $uri $uri/ /index.php?s=$uri&$args; # 核心
    }

    location ~ \.php$ {
        root "/vagrant/www/vip-operate";
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
        #try_files $uri /index.php =404;
        #fastcgi_split_path_info ^(.+\.php)(/.+)$;
    }
}


```
