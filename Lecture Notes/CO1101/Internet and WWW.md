
Class: #CO1101
Date: 06-10-2025
Teacher: #GAT #DL
# Notes:

## The Internet

### What is the Internet?

- Global digital network that connects computers, people and devices together.


###   History of the Internet:

- ARPANET (Advanced Research Projects Agency Network) in 1969, which initially connected four universities' computers to each other

- Grew exponentially during the 1970s

- CSnet in 1979 to promote research

- CSnet and ARPAnet got connected in the 80s

- In 1983, the internet was born.


### Structure of the Internet:

![[How the internet works.png]]

In words:




### From the Internet to WWW:

- 1990 - ARPAnet really becomes the internet
- Before 1990, the Internet was largely academic only
- WWW is an application of the internet
- Web Standards: URL, HTML, HTTP


### Important Terminology

- *Client*: Any device on the network that requests services from another device on the network

- *Server*: Any computer that receives requests from client devices, processes them and sends the output

- *Web Page*: Any page that is hosted on the internet

- *Web Dev*: The process o creating and modifying web pages

![[Client-Server.png]]


## World Wide Web (WWW)

- The WWW or web uses the HTTP/HTTPS protocols to transmit webpages.

- It was created in 1989-91 by Tim Berners-lee

- Uses client-server model


### How does it all work?

- Information is stored in web pages (in HTML format).

- These web pages are stored on computers called *web servers*

- The computer (or device) reading the web pages is called *web client*

- The web client uses browsers like Google Chrome, Internet Explorer, Firefox, Safari, etc.

- The user makes use of web browsers to send a request to *server*.


## The Internet vs Web

- The internet and web are two *SEPARATE* things

- Internet is a collection of computers or networking devices connected together.
	- These devices can communicate with each other

- Web is a collection of interconnected web pages.
	- These documents are provided by web servers and can be accessed using a web browser


### Protocols

- A protocol is a set of standards that has been defined for computers to communicate with each other

- It defines the format of messages and order of messages sent/received

- Protocols control sending and receiving messages
	- TCP
	- IP
	- HTTP


#### IP

- A simple protocol to send data between two computers

- Each device connected to internet is assigned a *unique* IP address.

- Data travelling via internet is divided into smaller pieces called *packets*

- IP address info is attached to each packet so it can be routed to the correct destination

- Find you IP Address: *whatismyip.com*

### Domain Name System (DNS)

- A DNS is a set of servers that maps domain names to IP addresses

- For example: le.ac.uk translates to - 

```python
https.//le.ac.uk/ --> 143.210.133.109
```

### Uniform Resource Locator (URL)

- Also called a *web address*

- A unique identifier for the location of each web page.

- URL has 3 component: *protocol used, server name, path of file on the server.*

```python
https://le.ac.uk/courses

https:    ->   protocol
le.ac.uk  ->   domain name
courses   ->   path
```

### Hypertext Transfer Protocol (HTTP)

- This protocol defines how a web browser and web server exchange information

- A browser sends a HTTP request to the web server which in turn sends an HTTP response back.

- Establish a connection with the server which sends HTML pages to user's browser.


### Who runs the internet?

- *Internet Engineering Task Force (IETF)*: responsible for IP standards

- *Internet Corporation for Assigned Names and Numbers (ICANN)*: decides top-level domain names

- *WWW Consortium (W3C)*: develops web standards

### Web cookies

- A cookie is a small file sent to a browser from a server when a user visits a website

- When user visits the same website again, the browser sends the cookie back to server


#### Why are cookies useful?

- Cookies allow websites to remember information like:
	- User Login info
	- Details user may have entered
	- Keep items in basket
	- Items user viewed on previous visit
	- Number of times a user visited a page
	- Time user spent on a web page


### Web Techs

- Hypertext Markup Language (HTML): write web pages

- Cascading Style Sheets (CSS): for stylistic info of web pages

- JavaScript: for interactive and programmable web pages