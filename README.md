
Socket:

N clients are connected to a server and send messages. In this program, one of the clients send messages to the server and it will send back the messages to all other clients. The code is implemented using C language, with a TCP connection.

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

Client:
n the client program, first is the establishment of connection to the server and running on the localhost.
Connection is established by using connect().
Then select() is used for either reading or writing as in the server program.
It sends message to the server from the keyboard input using stdin.
If there is data in the recv_buf, it receives data using recv().

