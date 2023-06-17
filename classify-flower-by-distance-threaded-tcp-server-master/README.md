# classify-flower-by-distance-on-tcp-with-thread


this project is made by Adi Tal and Daniel Singer, as our fourth excersize for advanced programming course.<br>
this code can only be compiled and run in linux.
### compiling and running
for compiling the code, just write in the terminal the command make.<br>
this will make 2 execuatable files, one is named server.out and the another is named client.out<br>
for running the server. type the command ./server.out [port](in the port you have to put the port number that you want to give to the server)
for running  the client. type the command ./client.out [ip][port])(server's ip and code that we want to connect to)
## what the code does
### client-
the client connects the server,and is having connection with it by tcp protocol.
the client is "silly"- all the work is the done in the server.
### server-
the server sends to client this menu-<br>
![server menu](https://user-images.githubusercontent.com/118116425/214846619-e9c6bd2b-a430-494e-9ac3-85d8ae84cc7c.png)
<br>
the server can do all these functions:<br>
upload files from the client,sending files to client , calculate knn distance(according to the methood).<br>
after the server finishes doing a task, it sends to the client the menu.<br>
the connection with a client is closed after the client presses 8.
### working with multiple clients
this server uses multiple threads.<br>
whenever a new client connects the server, the server creates new thread special for it.<br>
so that the server can handle multipe clients in the same time.<br>
for identifing a client. __each client get an ID that's it's uique for him__.<br>
when the server saves file for the client, it will name the files with the client id,<br>
so that we will be able to identify to which client this files belong.<br>
for example, when client with id number 3 will upload file to classify. in the server,<br>
it will name the file Unclassified_3.csv.

### transporting data over tcp

how we send and recive data on tcp sockets?<br>
when we send data on tcp, the data is stored in the reciving socket of the reciving side.<br>
when the application layer pulls it with the command "recv", it can't tell when a "message" starts and when it ends, because there isn't such thing as message in tcp.<br>
so, in our project we made up sending and reciving protocol.>br>
supose I want to send "hello world", and immidietly after it, "what's up?" but the reciving side, pulled the data after the moment the socket recived it.<br>
so the reciving side can't tell if it's 1 "message" or 2.<br>
our solution is this one: after every message we send "$"; so "hello world$what's up?$" is 2 different "messsages"<br>
the client and server can know now how to seperate the data in the reciving buffer to "messages" in the way the sending side sent them.<br>

__note for the checker__ - the class the we name handleClient,does the same as the class "cli" that you explained about in the task<br>,
we decided to name it HandleClient
