# Keywords

<h3>Table of Contents</h3>

[TOC]

# CS Dictionary

## General


#### i368
- genereally refers a 32bit processor
- Intel 80368: First 32bit CPU

#### amd64
- genereally refers a 64bit processor
- 64bit CPU architecture invented by amd

#### CRUD
* create, read, update, delete
* SQL: insert, select, update, delete
* HTTP: Used in RESTful API: PUT/POST, GET, PUT/POST/PATCH, DELETE
* DDS: Data Distribution Service: write, read/take, write, despose

#### module
* a file containing codes

#### package
* collection of modules

#### library
* A bunch of code which simplifies functions/methods for quick use.
* to help you do things more quickly/easily
* offer one area of functionality

#### api
* application programming interface
* the interface to the library
* that you can call to ask it to do things for you

#### framework
* is a big library or group of libraries that provides many services
* supplies a complete base on which you build your own code


#### sdk
* software development kit
* is a library or group of libraries 
* with extra tool applications, data files and sample code

#### ide
* integrated development environment
* text editor with additional support for developing,compiling and debugging applications. e.g Eclipse, Visual Studio.

#### toolkit
* is like an SDK
* with more focus on providing tools and applications than on just code libraries

#### markup lang
* Markup language is a paradigm/system to annotate a document in a way that is syntactically distinguishable from the text.
* e.g. (X)HTML: (Extensible)Hypertext ML, XML: Extensible ML, (La)TeX: (Lamport)TeX

#### JSON
* JavaScript object notation

#### YAML
* stands for "YAML Ain't Markup Language"
* YAML is to configuration what markdown is to markup
* YAML is a human-readable data serialization language
* commonly used for configuration files, 
* but could be used in many applications where 
    * data is being stored (e.g. debugging output)
    * data is being transmitted (e.g. document headers). 
* Uses python style indentation, [], {}
* Superset of JSON
* YAML is case sensitive.
* Can contain unix/linux commands 


## Web

#### SaaS
- Software as a service
- Gmail, Google apps, Cisco WebEx

#### PaaS
- Platform as a service
- heroku, Travis CI, Circle CI

#### IaaS
- Infrastructure as a service
- AWS, MS Azure, 

#### FaaS
Function as a service

#### BaaS
Backend as a service

#### CaaS
Container as a service

#### CSS
* cascading style sheet
* a style sheet language
* used for describing presentation of a document written in a markup language.

#### LESS
* CSS preprocessor: scripting language that extends CSS
* Leaner CSS
* CSS Dry
* Implemented in JavaScript
* Extension: .less

#### Sass
* CSS preprocessor: scripting language that extends CSS
* Syntactically Awesome style sheet
* CSS Dry
* implemented in Ruby
* Extension: .scss

#### CDN
* Content Delivery Network
* a system of distributed servers/network that deliver pages and other web content to a user 
* based on geographical locations of the user to provide highspeed delivery
* Working:
    * When a user request a page that is a part of CDN, then request goes to the central server and redirects the request to nearby server

#### RWD (Responsive Web Design)
* A web designing approach
* crafting site to provide an optimal viewing experience
* easy reading and navigation with a minimum of resizing, panning, and scrolling
* across a wide range  of device (from mobile phones, tablets to desktop screens)

#### Mobile First
* A paradigm for creating UX
* design UX for mobile devices first than other
* because users prefer mobiles nowadays


#### UI Design/Front-end Framework
* eg. Bootstrap, Foundation, Pure
* includes CSS, HTML for typography, icons, forms, buttons, tables, layout grids, navigation.
* includes JS also
* support for responsive

#### JS Framework
* e.g. AngularJS, ReactJS,
* JavaScript framework for building CRUD centric AJAX style web applications
* features 2-way data binding, deep linking, routing, transition animations and a lot lot more

#### HTTP
* Hyper text transfer protocol
* base protocol the internet is built on
* a request and response system
* client sends a request to endpoint and endpoint responds
* e.g. a browser accessing a web server, an app accessing an API

#### HTTP Request Methods
Used for sending and retrieving HTML form data.

* **GET**
    * Default
    * sends request by enclosing all the data into url string
    * The request/response have HTTP header only
    * Parameters are visible
    * Parameters remains in history
    * Hackable
    * Not Secure
    * Restriction in data length, 2048 chars, depends on browser
    * can be cached
    * Should be used for case when state of system/data is not going to be changed
    * unsuitable for sending password 
* **POST**
    * sends request by enclosing all the data into 
    * The request/response have HTTP header & HTTP body
    * HTTP body contains message in URLEncoded format
* **PUT**
* **DELETE**

#### CSRF : Cross Site Request Forgery
* A Cross-site request forgery hole is when a malicious site can cause a visitor's browser to make a request to your server that causes a change on the server. The server thinks that because the request comes with the user's cookies, the user wanted to submit that form.

#### Web Server
* a software, not a machine which stores code
* recieves requests from client/browser
* returns response, but doesn't create response
* so, it talks to **web application**

#### Web Apllication
* creates response based on urls
* passes response to web server

#### WSGI: Web Server Gateway Interface
* an interface between web server & application
* contains some statements, set of rules
* its not a software/library/framework
* WSGI compliant server will able to communicate with a WSGI compliant web app
* in WSGI, WSGI application has to be callable & it needs o be given to web server, so web server can call web application whenever it receives a request

#### Web Service
* a piece of software available over internet
* and can be ustilized by some other softwares
* using standard messaging system XML.

#### Web API
* Application Programming Interface
* In web world its synonym to 'web services'
* used by client apps to retrieve and update data 

##### Appication Without web API
<img src="https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/56/73/3225.NoAPIArchitecture.PNG"  /img>

##### Appication Without web API
<img src="https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/56/73/2318.WithAPIArchitecture.PNG" /img>


-
Source: https://knpuniversity.com/screencast/rest/rest
https://blogs.msdn.microsoft.com/martinkearn/2015/01/05/introduction-to-rest-and-net-web-api/
http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm


## Infrastructure

(Nginx, Gunicorn, RabbitMQ, Celery, Redis, memcached, apache, WSGI)
(load balancer, web accelerator, cache, database, task queue, etc.) 

#### Nginx: 
* An HTTP and Reverse Proxy Server

#### Gunicorn: 
* A WSGI HTTP server

#### Celery:
* A tool for asynchronous processing with Python

#### Redis: 
* A message broker

#### Supervisor: 
* A process control system for unix

