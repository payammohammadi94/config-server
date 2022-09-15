# config-server
1) install nginx
2) sudo ufw allow port for project
3) sudo ufw allow port 22 and 22/tcp
4) sudo ufw allow "Nginx Full"
5) systemctl enable ufw
6)خرید دامنه
7) استفاده از سایت کلودفلر به عنوان دی ان اس
8) اضافه کردن دی ان اس های کلودفلر به دامنه
9) بعد فعال شدن دی ان اس باید تنظیمات وبسرور را برای پورت خاص انجام داد

10) cd /etc/nginx/sites-available/
11) vim tanakora-sanandaj

(*
server {
    listen 80;
    server_name tanakora-sanandaj.ir www.tanakora-sanandaj.ir;

    # Serve any static assets with NGINX
    location /_next/static {
        alias /var/www/demoSite/.next/static;
        expires 30d;
	access_log off;
    }




    location / {
        # reverse proxy for next server
        proxy_pass http://localhost:3000; #Don't forget to update your port number
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

}
*)

12) sudo ln -s /etc/nginx/sites-available/tanakora-sanandaj /etc/nginx/sites-enabled/tanakora-sanandaj
13)systemctl restart nginx

14)finish
