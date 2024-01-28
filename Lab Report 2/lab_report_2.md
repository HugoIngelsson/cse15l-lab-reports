# Lab Report 2

## Part 1
Before describing the two screenshots, I wanted to also explain what happens when the server starts up since that's also running a few methods. First, on running ChatServer.java, its main method starts a server from the Server.start() method with the port number used as a command line argument, along with a new Handler() object. When Server.start() runs, it creates a new HttpServer(), which then creates a new context for the Handler() passed in. Then, whenever a new webpage is loaded, the context runs a handle() method, which handles the URI using the Handler() object and prints out something for the user to look at.

### Screenshot 1 (working example)

![Good use of Chat Server](correct_address.png)

In this example, the handle(final HttpExchange exchange) method first gets called (as described above), which then calls handleRequest(URI uri) from ChatServer.java.

In the handle() function, "exchange" is the parameter that lets the program speak to the server. It is what lets us ask for the URI using "exchange.getRequestURI()"; it is also what lets us write to the server by using "exchange.getResponseBody()".

For the handleRequest() function, "url" is the parameter that lets us know what the user typed into the search bar. It can be split up into its components using "url.getPath()" and "url.getQuery()" (you can also get the host address using "url.getHost()", but we don't need that for this server). In particular, using the URL in the screenshot, "url.getPath()" returns "/add-message" and "url.getQuery()" returns "s=So%20True&user=jpolitz" in this case.

The Handler() class has a String field named "chat", which is a record of the chat up until this point. In this case, it is a very long value containing "\n"s to split up the four messages sent before typing in this URL. The Handler() class also contains an int field named "chatNumber", which I just chose to include in case I ever wanted to expand on the server and needed to know how many messages had been sent so far; it currently has a value of 4.

After this specific request, the field "chat" had the String "jpolitz: So true\n" appended to it (this happened before printing to the server, so it shows the updated version of "chat" on the webpage). "chatNumber" was also incremented to 5.

### Screenshot 2 (incorrect formatting)

![Bad use of Chat Server](wrong_address.png)
