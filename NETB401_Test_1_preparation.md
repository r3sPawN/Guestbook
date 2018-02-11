## 1. Describe HTTP requests. Which are idempotent. What does “idempotent” means in this context?

HTTP defines a set of request methods to indicate the desired action to be performed for a given resource. Although they can also be nouns, these request methods are sometimes referred to as HTTP verbs. Each of them implements a different semantic, but some common features are shared by a group of them: e.g. a request method can be safe, idempotent, or cacheable.

GET
The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.
HEAD
The HEAD method asks for a response identical to that of a GET request, but without the response body.
POST
The POST method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server
PUT
The PUT method replaces all current representations of the target resource with the request payload.

DELETE
The DELETE method deletes the specified resource.
CONNECT
The CONNECT method establishes a tunnel to the server identified by the target resource.

OPTIONS
The OPTIONS method is used to describe the communication options for the target resource.
TRACE
The TRACE method performs a message loop-back test along the path to the target resource.

PATCH
The PATCH method is used to apply partial modifications to a resource.

From a RESTful service standpoint, for an operation (or service call) to be idempotent, clients can make that same call repeatedly while producing the same result. In other words, making multiple identical requests has the same effect as making a single request. Note that while idempotent operations produce the same result on the server (no side effects), the response itself may not be the same (e.g. a resource's state may change between requests).

The PUT and DELETE methods are defined to be idempotent. However, there is a caveat on DELETE. The problem with DELETE, which if successful would normally return a 200 (OK) or 204 (No Content), will often return a 404 (Not Found) on subsequent calls, unless the service is configured to "mark" resources for deletion without actually deleting them. However, when the service actually deletes the resource, the next call will not find the resource to delete it and return a 404. However, the state on the server is the same after each DELETE call, but the response is different.

GET, HEAD, OPTIONS and TRACE methods are defined as safe, meaning they are only intended for retrieving data. This makes them idempotent as well since multiple, identical requests will behave the same.


## 2. What is the difference between static and dynamic website? Describe the advantages and disadvantages of both approaches?

Static websites are the websites, which do not practically have a backend to process the user interactions. A great modern example, would be a project stored in GitHub, displayed to the end user from GitHub pages. The project would partially hold some static data, but also could have JavaScript scripts, which run on the end user's machine, which request data from the other server and display the received data to the user.

The dynamic websites, on the other hand, can immediately process the user interactions. An example, could be a Guestbook, on which the user creates a new entry and immediately sees it in the list.

The static website approach has advantages in cost of hosting and cost of development. It is also easier and faster to develop. As for the disadvantages it is harder to maintain (requires web development expertise to update the website), might lack some crucial functionalities for the purpose.

Even though the dynamic websites are harder to develop, consume more time for development and are more expensive to host, provide infinite opportunities for functionality.


## 3. What does “Just-in-time” compilation means? What is the difference with interpretation?

JIT compiler: Reads your source code, or more typically some intermediate representation (bytecode) of it, compiles that on the fly and executes native code.

Interpreter: Reads your source code or some intermediate representation (bytecode) of it, and executes it directly.


## 4. Describe shortly ASP.NET page lifecycle

Stage
Description
Page request
The page request occurs before the page life cycle begins. When the page is requested by a user, ASP.NET determines whether the page needs to be parsed and compiled (therefore beginning the life of a page), or whether a cached version of the page can be sent in response without running the page.
Start
In the start stage, page properties such as Request and Response are set. At this stage, the page also determines whether the request is a postback or a new request and sets the IsPostBack property. The page also sets the UICulture property.
Initialization
During page initialization, controls on the page are available and each control's UniqueID property is set. A master page and themes are also applied to the page if applicable. If the current request is a postback, the postback data has not yet been loaded and control property values have not been restored to the values from view state.
Load
During load, if the current request is a postback, control properties are loaded with information recovered from view state and control state.
Postback event handling
If the request is a postback, control event handlers are called. After that, the Validate method of all validator controls is called, which sets the IsValid property of individual validator controls and of the page. (There is an exception to this sequence: the handler for the event that caused validation is called after validation.)
Rendering
Before rendering, view state is saved for the page and all controls. During the rendering stage, the page calls the Render method for each control, providing a text writer that writes its output to the OutputStream object of the page's Response property.
Unload
The Unload event is raised after the page has been fully rendered, sent to the client, and is ready to be discarded. At this point, page properties such as Response and Request are unloaded and cleanup is performed.


## 5. What are the differences between structures and classes in C#?

In .NET, there are two categories of types, reference types and value types.

Structs are value types and classes are reference types.

The general difference is that a reference type lives on the heap, and a value type lives inline, that is, wherever it is your variable or field is defined.

A variable containing a value type contains the entire value type value. For a struct, that means that the variable contains the entire struct, with all its fields.

A variable containing a reference type contains a pointer, or a reference to somewhere else in memory where the actual value resides.

This has one benefit, to begin with:

value types always contains a value
reference types can contain a null-reference, meaning that they don't refer to anything at all at the moment
Internally, reference types are implemented as pointers, and knowing that, and knowing how variable assignment works, there are other behavioral patterns:

copying the contents of a value type variable into another variable, copies the entire contents into the new variable, making the two distinct. In other words, after the copy, changes to one won't affect the other
copying the contents of a reference type variable into another variable, copies the reference, which means you now have two references to the same somewhere else storage of the actual data. In other words, after the copy, changing the data in one reference will appear to affect the other as well, but only because you're really just looking at the same data both places.


## 6. What is the function of the proxy server? What are the benefits from using it?

Depending on which side the proxy is used.

For the client side, it is:

A proxy server is a dedicated computer or a software system running on a computer that acts as an intermediary between an endpoint device, such as a computer, and another server from which a user or client is requesting a service. The proxy server may exist in the same machine as a firewall server or it may be on a separate server, which forwards requests through the firewall.


An advantage of a proxy server is that its cache can serve all users. If one or more Internet sites are frequently requested, these are likely to be in the proxy's cache, which will improve user response time. A proxy can also log its interactions, which can be helpful for troubleshooting.

For the server side, the reverse proxy exists. It is:

A reverse proxy accepts a request from a client, forwards it to a server that can fulfill it, and returns the server’s response to the client.

The advantages are:

Load Balancing

This is the reverse proxy function that people are most familiar with. Here the proxy routes incoming HTTP requests to a number of identical web servers. This can work on a simple round-robin basis, or if you have statefull web servers (it’s better not to) there are session-aware load balancers available. It’s such a common function that load balancing reverse proxies are usually just referred to as ‘load balancers’. There are specialized load balancing products available, but many general purpose reverse proxies also provide load balancing functionality.

Security

A reverse proxy can hide the topology and characteristics of your back-end servers by removing the need for direct internet access to them. You can place your reverse proxy in an internet facing DMZ, but hide your web servers inside a non-public subnet.

Authentication

You can use your reverse proxy to provide a single point of authentication for all HTTP requests.

SSL Termination

Here the reverse proxy handles incoming HTTPS connections, decrypting the requests and passing unencrypted requests on to the web servers. This has several benefits:

Removes the need to install certificates on many back end web servers.
Provides a single point of configuration and management for SSL/TLS
Takes the processing load of encrypting/decrypting HTTPS traffic away from web servers.
Makes testing and intercepting HTTP requests to individual web servers easier.
Serving Static Content

Not strictly speaking ‘reverse proxying’ as such. Some reverse proxy servers can also act as web servers serving static content. The average web page can often consist of megabytes of static content such as images, CSS files and JavaScript files. By serving these separately you can take considerable load from back end web servers, leaving them free to render dynamic content.

Caching

The reverse proxy can also act as a cache. You can either have a dumb cache that simply expires after a set period, or better still a cache that respects Cache-Control and Expires headers. This can considerably reduce the load on the back-end servers.

Compression

In order to reduce the bandwidth needed for individual requests, the reverse proxy can decompress incoming requests and compress outgoing ones. This reduces the load on the back-end servers that would otherwise have to do the compression, and makes debugging requests to, and responses from, the back-end servers easier.

Centralised Logging and Auditing

Because all HTTP requests are routed through the reverse proxy, it makes an excellent point for logging and auditing.

URL Rewriting

Sometimes the URL scheme that a legacy application presents is not ideal for discovery or search engine optimisation. A reverse proxy can rewrite URLs before passing them on to your back-end servers. For example, a legacy ASP.NET application might have a URL for a product that looks like this:

http://www.myexampleshop.com/products.aspx?productid=1234

You can use a reverse proxy to present a search engine optimised URL instead:

http://www.myexampleshop.com/products/1234/lunar-module

Aggregating Multiple Websites Into the Same URL Space

In a distributed architecture it’s desirable to have different pieces of functionality served by isolated components. A reverse proxy can route different branches of a single URL address space to different internal web servers.

For example, say I’ve got three internal web servers:

http://products.internal.net/
http://orders.internal.net/
http://stock-control.internal.net/

I can route these from a single external domain using my reverse proxy:

http://www.example.com/products/    -> http://products.internal.net/
http://www.example.com/orders/    -> http://orders.internal.net/
http://www.example.com/stock/    -> http://stock-control.internal.net/

To an external customer it appears that they are simply navigating a single website, but internally the organisation is maintaining three entirely separate sites. This approach can work extremely well for web service APIs where the reverse proxy provides a consistent single public facade to an internal distributed component oriented architecture.


## 7. What are the differences HTML4 and HTML5?

The JavaScript API differences are not covered intentionally, as the main topic is HTML.

1. Simpler DOCTYPE

The HTML syntax of HTML5 requires a DOCTYPE to be specified to ensure that the browser renders the page in standards mode. The DOCTYPE has no other purpose and is therefore optional for XML. Documents with an XML media type are always handled in standards mode. [DOCTYPE]

The DOCTYPE declaration is and is case-insensitive in the HTML syntax. DOCTYPEs from earlier versions of HTML were longer because the HTML language was SGML-based and therefore required a reference to a DTD. With HTML5 this is no longer the case and the DOCTYPE is only needed to enable standards mode for documents written using the HTML syntax. Browsers already do this for .

2. The HTML <canvas> element is used to draw graphics, on the fly, via JavaScript.

The <canvas> element is only a container for graphics. You must use JavaScript to actually draw the graphics.

Canvas has several methods for drawing paths, boxes, circles, text, and adding images.

3. New semantically-inclined elements such as <header>, <footer>, <section>, <article>, <menu>, <main>, <aside>, <nav>, <figure>, <audio>, <video>,

4. New syntax for highlighting text. As an example, <strong> instead of <b>
According to the HTML 5 specification, the <b> tag should be used as a LAST resort when no other tag is more appropriate. The HTML 5 specification states that headings should be denoted with the <h1> to <h6> tags, emphasized text should be denoted with the <em> tag, important text should be denoted with the <strong> tag, and marked/highlighted text should use the <mark> tag.

5. <Applet> removed <Object> Added in HTML5

HTML4 contained an <applet> tag that was used for displaying applets in a web browser. However, in HTML5, this applet tag has been removed. In order to display applet type items, a new <object> tag has been introduced in HTML5.

6. Difference in usage of <hr> tag

The <hr> tag was used to draw a line in HTML4 and all the previous versions of HTML, however in HTML5, the functionality of this tag has been changed and it is used for defining a thematic break in the web page.

## 8. What is Common Intermediate Language and what is its purpose?

CIL is a low level language based on the Common language Infrastructure specification document. (http://www.ecma-international.org/publications/standards/Ecma-335.htm). CIL was earlier referred as MSIL (Microsoft Intermediate Language) but later changed to CIL to standardize the  name of the language which is based on the Common Language Infrastructure specification.

CIL is CPU and platform-independent instructions that can be executed in any environment supporting the Common Language Infrastructure, such as the .NET run time  or the cross-platform Mono run time. These instructions are later processed by run time compiler and is then converted into native language. CIL is an object-oriented assembly language, and is entirely stack-based.


## 9. Describe shortly ASP.NET states

A new instance of the Web page class is created each time the page is posted to the server. In traditional Web programming, this would typically mean that all information associated with the page and the controls on the page would be lost with each round trip. For example, if a user enters information into a text box, that information would be lost in the round trip from the browser or client device to the server.
To overcome this inherent limitation of traditional Web programming, ASP.NET includes several options that help you preserve data on both a per-page basis and an application-wide basis. These features are as follows:
View state
Control state
Hidden fields
Cookies
Query strings
Application state
Session state
Profile Properties
View state, control state, hidden fields, cookies, and query strings all involve storing data on the client in various ways. However, application state, session state, and profile properties all store data in memory on the server. Each option has distinct advantages and disadvantages, depending on the scenario.

## 10. What are the major differences between C++ and C#?

A list of differences between the two languages include:

Size of binaries: We mentioned that the two languages are compiled languages that turn your code into binary files. C# has a lot of overhead and libraries included before it will compile. C++ is much more lightweight. Therefore, C# binaries are much larger after it compiles compared to C++.

Performance: C++ is widely used when higher level languages are not efficient. C++ code is much faster than C# code, which makes it a better solution for applications where performance is important. For instance, your network analysis software might need some C++ code, but performance is probably not a huge issue for a standard word processing application coded in C#.

Garbage collection: With C#, you don’t have to worry much about garbage collection. With C++, you have no automatic garbage collection and must allocate and deallocate memory for your objects.

Platform target: C# programs are usually targeted towards the Windows operating system, although Microsoft is working towards cross-platform support for C# programs. With C++, you can code for any platform including Mac, Windows and Linux.

Types of projects: C++ programmers generally focus on applications that work directly with hardware or that need better performance than other languages can offer. C++ programs include server-side applications, networking, gaming, and even device drivers for your PC. C# is generally used for web, mobile and desktop applications.

Compiler warnings: C++ will let you do almost anything provided the syntax is right. It’s a flexible language, but you can cause some real damage to the operating system. C# is much more protected and gives you compiler errors and warnings without allowing you to make some serious errors that C++ will allow.
