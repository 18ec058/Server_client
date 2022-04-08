Program : Chat Application using client-server protocol(TCP/IP)

This program helps to connect multiple computers which are connected to the common network, so that they can communicate with each other.
It contains a single server which handles multiple clients.
Clients(computers) send request to server , so that it can connect with other clients.
Server process these requests and grant permission for the connection establishment.

Server Program:

In the server program, first step is establishing connection to a port. we get the socket file descriptor.

int socket(int domain, int type, int protocol);

Once we have a socket, we can associate that socket with a port on our local machine. This can be done by using the ‘bind’.

int bind(int sockfd, struct sockaddr *myaddr, int addrlen);

we can use 'listen', to wait for the incoming connectionn.
int listen(int sockfd, int backlog);

sockfd is the usual socket file descriptor from the socket() system call.
backlog is the number of connections allowed on the incoming queue 

Server, it wants to listen for incoming connections as well as keep reading from the connections it already have. select() gives the power to monitor several sockets at the same time.

After ‘select’, it run through the existing connections looking for data to read. If we got one, new connections are handled and the new file descriptor is added to the master set by keeping track of the maximum file descriptor. If there is no need to handle new connection, handle data from a client. If there is any data in the recv_buf, it can be received by using recv(). Or , the data is send to all other clients by using the function send_all().

Client Program:
n the client program, first is the establishment of connection to the server and running on the localhost.
Connection is established by using connect().
Then select() is used for either reading or writing as in the server program.
It sends message to the server from the keyboard input using stdin.
If there is data in the recv_buf, it receives data using recv().

