# redirToParentFolder
Redirect traffic from physical but empty Folder to parent folder, providing parameters using htaccess

Imagine a scenario where you are moving a online shop or a huge site from one folder to another one. This may occur when migrating to another shop software oder cms. 

In this case this htacces snippet will help you. It will redirect traffic from a subfolder to a parent folder. The subfolders name and other ressource names will be used as http-parameters that can be used for a onsite search, for example. 

This solution uses one physical folder. I assuem that your prio website used this folder as an entry point for incoming traffic. This folder contains an .htaccess-file. The advantage is: Instead of an .htaccess-file inside the root-folder, filtering entire website traffic, only traffic to this folder will be processed. This keeps overhead to a minimum. 

# folder structure

/index.php - this is the starting point of your new softare in the root folder of your hosted website

/foobar - this is a physical folder inside your webspace, represanting the starting point of your old folder structure. 

/foobar/.htaccess - this is the .htaccess-file we are using to redirect the traffic

# htacess content
There are two rules, the first one redirects traffic from /foobar to the root, the second one from every direct subfolder of /foobar to the root, like /foobar/world, /foobar/fling and so on. This ruleset will not redirect traffic pointing to a 3rd level, like /foobar/hello/world/

 RewriteEngine On

 RewriteRule ^(/?)([a-zA-Z0-9]+)?([\.html]+)?/?$ /index.php?search=$2 [R=301,NC]

 RewriteRule ^(/?)([a-zA-Z0-9]+)?/([a-zA-Z0-9]+)?([\.html]+)?/?$ /index.php?search=$2\ $3 [L,R=301,NC]
 
 # example
 
  www.shop.com/de1/foobar -> www.shop.com/index.php?search=foobar
  
  www.shop.com/de1/foobar.html -> www.shop.com/index.php?search=foobar
