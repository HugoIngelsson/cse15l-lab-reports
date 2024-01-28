# Lab Report 2

## Part 1
Before describing the two screenshots, I wanted to also explain what happens when the server starts up since that's also running a few methods. First, on running ChatServer.java, its main method starts a server from the Server.start() method with the port number used as a command line argument, along with a new Handler() object. When Server.start() runs, it creates a new HttpServer(), which then creates a new context for the Handler() passed in. Then, whenever a new webpage is loaded, the context runs a handle() method, which handles the URI using the Handler() object and prints out something for the user to look at.

### Screenshot 1 (working example)

![Good use of Chat Server](correct_address.png)
