# My_Company_Tasks

#___________________________________________Task1 :Deploy a PHP Application using Azure Virtual Machine on Apache Server______________________________________________

sudo apt-get update
sudo apt-get install apache2 -y
sudo apt-get install php libapache2-mod-php -y
sudo apt install php-dev libmcrypt-dev php-pear -y
sudo pecl channel-update pecl.php.net

->> yha pe latest dalna hei otw error 1.0.1 xxx
sudo pecl install mcrypt-1.0.5

sudo service apache2 restart
cd /var/www/html
sudo rm index.html
xx sudo nano test.php

xx <?php
xx echo “Hello World!”;
xx ?>

sudo git clone https://github.com/Shilpajoshi7/PHPTrialApplication.git

https://medium.com/analytics-vidhya/learn-to-deploy-a-php-application-using-amazon-ec2-instance-cb0c212e6362



#_________________________________________Task2 Deploy django application on Azure Virtual Machine in apache and nginx server__________________________________________

->> Link simply apache se kiya django ka rocket aara (Koi hello wrold application nhi banaye)

https://www.digitalocean.com/community/tutorials/how-to-serve-django-applications-with-apache-and-mod_wsgi-on-ubuntu-14-04


sudo apt-get update
sudo apt-get install python3-pip apache2 libapache2-mod-wsgi-py3
sudo pip install virtualenv
mkdir ~/myproject
cd ~/myproject
virtualenv myprojectenv
source myprojectenv/bin/activate
pip install django
django-admin startproject myproject .
nano myproject/settings.py

import os 
ALLOWED_HOSTS = [' ']      ----> VM IP Address 
STATIC_ROOT = os.path.join(BASE_DIR, "static/")


cd ~/myproject
./manage.py makemigrations
./manage.py migrate
python3 ./manage.py createsuperuser
./manage.py collectstatic
./manage.py runserver 0.0.0.0:8000

sudo nano /etc/apache2/sites-available/000-default.conf

-------Indentation shi se lena copy karte time-----------
Alias /static /home/azureuser/myproject/static
    <Directory /home/azureuser/myproject/static>
        Require all granted
    </Directory>

    <Directory /home/azureuser/myproject/myproject>
        <Files wsgi.py>
            Require all granted
        </Files>
    </Directory>

    WSGIDaemonProcess myproject python-path=/home/azureuser/myproject python-home=/home/azureuser/myproject/myprojectenv
    WSGIProcessGroup myproject
    WSGIScriptAlias / /home/azureuser/myproject/myproject/wsgi.py
    
sudo service apache2 restart    







#___________________________________________________________Task3 Load Balancer_______________________________________________________________________________________
Load Balancing ke page refresh karke  This is VM1 refresh This is VM2 

1) VM1 mei ssh karke  VM2 mei bhi same karna hei  
cd downloads --->>key downloads mei save hoti hai
ssh ka link key daal ke ex ssh -i key1.pem azureuser@20.168.231.212

2) Apache daala aur page moify karna 
sudo apt update
sudo apt install apache2 -y
sudo service apache2 start
cd /var/www/html
sudo rm index.html
sudo vi index.html
<h1> This is VM1 </h1>       same in VM2

_________________________________________________________Task4  Autoscaling in LB  _____________________________________________________________________
Take help from 
https://www.youtube.com/watch?v=xD9MVGY216o

NOTE : 1 hei VM lena varna nhi hora ( I think 2 or more VM leke load un VMs mei manage hooo zara hei )

 Autoscaling mei CPU load increse karne ke liye
 top
 yes >/dev/null &
 top
kill -9 pid  ----> pid lena


#___________Task5  Deploy Reactjs Application on Azure App Service and distribute traffic through AZ Traffic manager  _______  ___

xxxxxxx https://websitebeaver.com/deploy-create-react-app-to-azure-app-services If u want ot try it using github pipeline xxxxxxx

correct way deploy reactjs application on azure app service from vs code   (VS codeko use karke)

https://medium.com/geekculture/easiest-way-to-host-your-react-app-azure-vs-code-8046f9f7fb0b
https://medium.com/ms-club-of-sliit/deploy-a-react-app-using-azure-app-service-from-vs-code-57643313f53c


create a folder open it on VS Code
Now go to vs code terminal 

node --version
npx --version
create-react-app mediumblog
cd mediumblog
npm start

web.config
<?xml version="1.0"?>    
<configuration>    
 <system.webServer>    
   <rewrite>    
     <rules>    
       <rule name="React Routes" stopProcessing="true">    
         <match url=".*" />    
         <conditions logicalGrouping="MatchAll">    
          <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />    
          <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />    
          <add input="{REQUEST_URI}" pattern="^/(api)" negate="true" />    
         </conditions>    
         <action type="Rewrite" url="/" />    
       </rule>    
     </rules>    
   </rewrite>    
 </system.webServer>    
</configuration>  

npm run build 

Install the “Azure App Service” VS code extension




->> agar aysa eroe ayega toh 
Error  npm ERR! code ERR_SOCKET_TIMEOUT    ( I Think yeh sirf network connectivity issue hei Internet problem )
Soln   npm cache clear --force

---XXXX Not Req Add Custom Domain to Traffic Manager
https://www.youtube.com/watch?v=1ggz9qZpVHo


______________________________________Task6  Deploy Nojejs application on azure virtual machine and add custom doamin _____________________________________
https://medium.com/tensult/configure-nginx-with-nodejs-application-on-aws-ubuntu-18-04-server-for-different-http-ports-a2f722902032


____________________________________Task7 Deploy python code using azure app function and 



