## **Overview**

This repo conisists of an end-to-end implementation of machine learning method for house price prediction.

The implementation was adapted from [this](https://youtube.com/playlist?list=PLeo1K3hjS3uu7clOTtwsp94PcHbzqpAdg) tutorial series on youtube.

### **1. Dataset**

The dataset consists of potential features house buyers consider when purchasing a new house (location, size, availability, etc.) in the city of Bengaluru, India. The dataset could be downloaded from [here](https://www.kaggle.com/datasets/amitabhajoy/bengaluru-house-price-data).

### 2. **Deployment**

1. Create an EC2 (Ubuntu) instance on AWS.
2. Connect with the instance using SSH.
3. Install and configure an nginx web server engine.

   i. Configuration setting (site.conf in /etc/nginx/sites-available directory)
   ```
	server {
    listen 80;
        server_name bhp;
        root /home/ubuntu/BangloreHomePrices/client;
        index app.html;
        location /api/ {
             rewrite ^/api(.*) $1 break;
             proxy_pass http://127.0.0.1:5000;
        }
	}
	```
	ii. Create sym link for this config file\
	`sudo ln -v -s /etc/nginx/sites-available/site.conf`

	iii. Unlink the default config\
	`sudo unlink default`

	iv. Restart nginx\
	`sudo service nginx restart`