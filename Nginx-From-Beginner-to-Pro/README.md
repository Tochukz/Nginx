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
