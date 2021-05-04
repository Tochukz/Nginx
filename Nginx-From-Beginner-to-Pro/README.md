# Nginx From Beginner to Pro (2016)  
__By Rahul Soni__  

## Chapter 1: Introduction to Nginx Web Server  
Nginx is a HTTP server and reverse proxy, as well as an IMAP/POP3 proxy server.

#### Main Feature of Nginx
__It Has a Straightforward Load Balancer__  
With Nginx you can set up a pretty straightforward and fast software load balancer. It can immediately help you out by sharing load across your front-end web servers.  

__It Scales Well__  
Nginx is one of the very few servers (along with Node.js) that is capable of addressing this issue, which is often referred to as _C10K_ problem (a term coined in 1999 by Dan Kegel for 10,000 concurrent connections).

__More Than Just a Web Server__  
At its core you can consider Nginx to be an event-bases _reverse proxy server_. A _reverse proxy_ is a type of proxy server that retrieves resources from the servers on behalf of a client.

__Modular Design__  
You can rebuild Nginx from source and include or exclude the modules that you don't need.  This gives you a very focused executable that does precisely what you need. This approach has a downside too., though. If you decide to incorporate another module at a later point, you will need to recompile with appropriate switches.  

__Asynchronous Web Server__  
Nginx gains much of its performance due to its asynchronous and event-based architecture whereas Apache and IIS like to spin new threads per connection, which are blocking in nature.

__SSL Termination__  
The idea of an SSL termination is that the request will come to the load balance on a secure channel but will be sent to the other web servers without SSL. This way, your web server acts faster and eventually your requests go to the clients in a secure manner as well.  

__Enterprise Features of Nginx Plus__  
Nginx Plus has features like load balancing, session persistence, cache control, and even health checks out of the box.  

#### Advantages of Nginx Plus  
__Advanced HTTP and TCP Load Balancing__  
There are four methods of load balancing in Nginx that are common to both versions:  
* Round Robin
* Least connections
* Generic Hash  
* IP Hash

Nginx Plus adds the least time method in tis stack. The load balancing methods in Nginx plus are extended to support multicore servers in an optimized way.

__Session Persistence__  
Nginx Plus load balancer identifies and pins all requests in a session to the same upstream server. It also provides a feature called _session draining_, which allows you to take a server down without interrupting established sessions.  

__Application Health Checks__  
Health checks continually test the upstream servers an d instruct Nginx Plus to avoid servers that have failed. If yours is a very busy site. this feature can be considered as one of the biggest reason why you should go with Nginx Plus!

__Live Active Monitoring__  
Nginx Plus comes with a real-time activity monitoring interface.  

#### Difference between Apache and Nginx  
__Static vs. Dynamic Content__  
Nginx has a clear advantage when serving static content. Apache has a clear, early mover advantage for dynamic content. It has built-in support for PHP, Python, Perl and many other languages. Nginx almost always requires extra effort to make it work with these languages. If you are a Python or Ruby developer, Apache might be a better choice since it will not need CGI to execute it. PHP has good support on Nginx.

__Configuration__  
You can have `.htaccess` file in every directory (if you like) using which you can provide additional directions to Apache about how to response to the requests of that specific directory. Nginx on the other hand interprets the requests based on the URL, instead of a directory structure.

__Modules (or Plug-Ins)__  
In Apache, you can dynamically load/unload the modules using configurations, but in Nginx you are supposed to build the binaries using different switches.

## Chapter 2: Installing Nginx  
__Preparing Your Environment__  
* Update the packages on your server  
```
$ sudo apt-get update
$ sudo apt-get upgrade
```
* Install some basic utilities: `lynx`, a text bases browser
```
$ sudo apt-get install lynx
$ sudo apt-get install ssh
```
`nano` (a text editor) and `wget` (a text based downloader) are installed by default on Ubuntu.  

#### Installing Nginx Using Pre-Built Packages  (Installation using the Package Manager)
__Install Nginx Pre-Built Package__  
Ubuntu PPA , has Nginx in their package repository list but it is not the latest version.  
To ensure that you have the latest version installed on your server, you will need to add the Nginx repository in the `sources.list` file.  
1. Open the `sources.list` file  
```
$ sudo nano /etc/apt/sources.list
```  
2. Append the Nginx repository to the button of the file and save
```
deb http://nginx.org/packages/ubuntu/ trusty nginx
deb-src http://nginx.org/packages/ubuntu/ trusty nginx
```  
3. Download and add the Nginx public key  
```
$ wget http://nginx.org/keys/nginx_signing.key
$ sudo apt-key add nginx_signing.key
```
4. Download and update the package lists from the repository  
```
$ sudo apt-get update
```
5. Install Nginx
```
$ sudo apt-get install nginx
```
6. Verify that Nginx was installed successfully  
```
$ nginx -v  
```

__Nginx Folder Structure__  
To get the complete list of Nginx configuration details  
```
$ nginx -V
```

* Nginx is installed at `/etc/nginx` and the its configuration details is found in `/etc/nginx/nginx.conf`.  
* The config file _include_ the `mime.types`. The `mime.types` and `fastcgi_params` file is found under `/etc/nginx`.  
* The Nginx executable is located in the system executable directory `/usr/sbin/nginx`  
* Nginx document root directory is located at `/usr/share/nginx/html` and contains `index.html` file
* The default error and access log files are located at `/var/log/nginx` as `access.log` and `error.log`

__Uninstall Nginx__  
```
$ sudo apt-get purge nginx nginx-common
```  
This will remove all the traces of Nginx installation. But it does not remove the Nginx entry from `sources.list`.  

#### Downloading Nginx from Source  (Installation from source)
If you want to make configurations changes, and pull in or pull out some modules from Nginx, you will need to rebuild Nginx from source. This is the same technique required to install a customized build of Nginx or to configure Nginx with third party modules.   

Visit the Nginx download webpage at [nginx.org/en/download.html](http://nginx.org/en/download.html), and download the `nginx-1.18.0.tar.gz` (at the time of this writing the latest version was `1.18.0`).    
Alternately you can use the `wget` utility to download it.
```
$ wget http://nginx.org/download/nginx-1.18.0.tar.gz
```  

Extract the Nginx Archive
```
$ tar xzf nginx-1.18.0.tar.gz
```  
Checkout the content of the source directory  
```
$ ls -la nginx-1.18.0
```  

__Installing Nginx Binaries__   
Compiling the source code required a `GCC` compiler and the `Make` utility to build and install the build.  
Install the build tools:
* Check the list of packages available in your Uuntu OS.  
```
$ sudo apt-cache search all | more
```  
* Install the development tool
```
$ sudo apt-get install build-essential
```  
* Update the system  
```
$ sudo apt-get update
$ sudo apt-get upgrade
```
* Verify the `GCC` and `Make` version
```
$ gcc --version
$ make --version
```

__Install Dependent Packages__   
Install __PCRE Library__ (Perl Compatible Regular Expression).  
Ubuntu and CentOS already have PCRE-compiled version installed. But if not:
```
$ sudo apt-get install libprec3
```  
Install the development libraries for PCRE  
```
$ sudo apt-get install libpcre3-dev
```  
__OpenSSL__ is installed by default on most Linux distros:
```
$ openssl verson
```  
If it is missing, you can install it
```
$ sudo apt-get install openssl  
```   
To see the Open SSL details including it's directory :
```
$ openssl version -a
```
Install the development libraries:  
```
$ sudo apt-get install libssl-dev
```
__zlib Library__ is used by Nginx to gzip module for compression. _zlib_ is one of
the dependencies of OpenSSL-devel so you shpuld already have it installed, but if not  
```
$ sudo apt-get install zlib1g zlib1g-dev
```  
Checkout the different configuration parameters available by using `configure` script  
```
$ cd nginx-1.18.0
$  ./configure --help
```
This will show a list of all the --flags that can be used to configure Nginx.   

__Enabling Nginx Modules__  
If you need to enable a particular module after Nginx is configures the only option left is to recompile Nginx. Though Nginx update and upgrade has zero impact on your website, it is recommended to take extra precautions when recompiling from source.


__Third-Party Modules__  
* You can find a list of all the third-party module at https://www.nginx.com/resources/wiki/modules/  
* You will need to patch Nginx in case of some third-party modules
* YOu will need to configure Nginx using the `./configure` command with the `--add-module` command after downloading the module:  
```
$ ./configure --add-module=../ngx_http_healthcheck_module
$ make
$ make install
```  

#### Compiling and Installing Nginx
__Prerequisites__    
Create a group name nginx
```
$ groupadd -r nginx
```  
Create user name nginx
```
$ useradd -r nginx -g nginx
```

__Manual Configuration__   
```
$ cd nginx-1.18.0
$ ./configure --prefix=/etc/nginx \
--user=nginx \
--group=nginx \
--sbin-path=/usr/sbin/nginx \
--conf-path=/etc/nginx/nginx.conf \
--pid-path=/var/run/nginx.pid \
--lock-path=/var/run/nginx.lock \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log \
--with-http_gzip_static_module \
--with-http_stub_status_module \
--with-http_ssl_module \
--with-pcre \
--with-file-aio \
--with-http_realip_module \
--without-http_scgi_module \
--without-http_uwsgi_module \
--without-http_proxy_module \

```
This command will generate a `Makefile` in the `objs` directory in the source folder.
And the final output on the terminal should look similar to this
```
Configuration summary
  + using system PCRE library
  + using system OpenSSL library
  + using system zlib library

  nginx path prefix: "/etc/nginx"
  nginx binary file: "/usr/sbin/nginx"
  nginx modules path: "/etc/nginx/modules"
  nginx configuration prefix: "/etc/nginx"
  nginx configuration file: "/etc/nginx/nginx.conf"
  nginx pid file: "/var/run/nginx.pid"
  nginx error log file: "/var/log/nginx/error.log"
  nginx http access log file: "/var/log/nginx/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"

```
Now, you execute the `make` command, which will compile all the code of the libraries to create a binary executable.  
```
$ make
```
Once the make command is executed successfully, final output should like similar to this
```
...
-ldl -lpthread -lcrypt -lpcre -lssl -lcrypto -ldl -lpthread -lz \
-Wl,-E
sed -e "s|%%PREFIX%%|/etc/nginx|" \
	-e "s|%%PID_PATH%%|/var/run/nginx.pid|" \
	-e "s|%%CONF_PATH%%|/etc/nginx/nginx.conf|" \
	-e "s|%%ERROR_LOG_PATH%%|/var/log/nginx/error.log|" \
	< man/nginx.8 > objs/nginx.8
make[1]: Leaving directory '/home/chucks/nginx-1.18.0'
`
```  
Now, you can install Nginx using the command  
```
$ sudo make install
```  
The `make install` command execute the install part of the `Makefile`.  The command essentially makes directories that do not exits and copies the configuration files ad binaries to the specific folder. You can see this in the output stream on the terminal  

Next, Create the `nginx.service`
```
$ cd /lib/systemd/system
$ sudo nano nginx.service
```
Paste the following content into the `nano` editor
```
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=forking
PIDFile=/var/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/usr/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```  
Save and exit the editor  

Start Nginx
```
$ sudo service nginx start
```


__Scripted Configuration__   
The commands used to configure Nginx can be put together in a script. See `chp2/configure-nginx.sh`      
The script must be executable   
```
$ chmod u+x ./setup-nginx.sh
```  
After that you can use a single command for the configuration  and then run the `make` and `make install` commands  
```
$ ./configure-nginx.sh
$ make
$ make install
```  
