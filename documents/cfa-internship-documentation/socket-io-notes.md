# Socket.io
A library for real-time, bidirectional, and event-driven communication between the server and the client. It uses the WebSocket protocol.  It abstracts away many of the complexities of websockets while also providing fallbacks for browsers that don't support them.
- [Official docs](https://socket.io/docs/v4)
## Basics

1. **WebSocket and Fallbacks**: At its core, Socket.io uses the WebSocket protocol for real-time communication. If WebSocket is not supported in a given situation (like some restrictive network environments or older browsers), Socket.io will seamlessly downgrade to other methods like long polling.
    
2. **Emitters and Listeners**: Socket.io's primary pattern is based on emitting events from one side (server or client) and listening for those events on the other side. It works similarly to the way the Observer pattern or Event Emitter pattern works.
    
3. **Namespaces**: Socket.io allows you to divide your application into different "rooms" or "channels" via namespaces. This can help segment different parts of your application or allow you to create chat rooms, for example.
    
4. **Broadcasting**: This allows you to send messages to everyone else except for the current socket. It's useful in situations like chat apps where you want to broadcast a message sent by one user to all other users.
    
5. **Connection & Disconnection**: Every user gets represented by a socket on connection. The server can listen to specific events on this socket. When the user disconnects, the socket for that user gets removed.
    
6. **Middleware**: Like Express, Socket.io also supports middleware. This allows you to run some code before an incoming socket handshakes or connects.
    

Now, a basic flow of using Socket.io would look like:

1. **Initialization**:
    
    - Server: Create an HTTP server and attach socket.io to it.
    - Client: Load the socket.io-client script and initialize a connection to the server.
2. **Event Communication**:
    
    - **Server-Side**: Listen to events from the client and potentially emit events back.
        ```javascript
        io.on('connection', (socket) => {
            socket.on('client-event', (data) => {
                // handle data from client   
            });
        socket.emit('server-event', { data: 'Hello from server!' });
        });
        ```

	-  **Client-Side**: Similarly, listen to events from the server and emit events to the server.

        ```javascript
        const socket = io('http://localhost:3000'); 
        socket.on('server-event', (data) => {
           // handle data from server 
           }); 
        socket.emit('client-event', { data: 'Hello from client!' });
        ```
         
3. **Disconnection**:
    
    - On the server, you can handle client disconnections.
        ```javascript
        socket.on('disconnect', () => {
           console.log('A user disconnected');
	    });
        ```

To effectively use Socket.io:

- **Understanding the Event-Driven Nature**: Grasping the concept of emitting and listening for events is crucial. Design your application's communication flow based on events.
    
- **Know the Difference**: Understand the difference between `io.emit`, `socket.emit`, `socket.broadcast.emit`, and when to use each.
    
- **Error Handling**: Handle connection errors, reconnection attempts, and manage different connection states.
    
- **Scaling**: If your application needs to scale across multiple nodes or processes, consider using the `socket.io-redis` adapter. It ensures events are broadcasted to all clients, no matter which process or node they're connected to.
    
- **Security**: Just like any other part of your application, consider security. Authenticate and validate incoming socket connections and emitted data.
    

In essence, Socket.io offers a high-level API for real-time communication on the web. By grasping its event-driven nature, you can easily build interactive applications that work in real-time.

## Additional Considerations
1. **Reserved Event Names**: There are a few reserved event names that you shouldn't use for your custom events, such as `connect`, `disconnect`, `connect_error`, and a few others. Using these can lead to unintended behaviors since Socket.io uses them internally.
    
2. **Descriptive Names**: While you can use almost any string as an event name, it's a good practice to use descriptive names. For example, if you're building a chat app, names like `message`, `typing`, or `user_joined` are clear and intuitive.
    
3. **Case Consistency**: Maintain consistency in case. If you're using camelCase for one event, try to stick with it for others as well to maintain code readability.
    
4. **Avoid Special Characters**: It's generally a good idea to avoid special characters or spaces in event names to prevent potential issues or confusion. Stick with alphanumeric characters.
    
5. **Data Limits**: Socket.io uses WebSockets underneath (with fallbacks). The protocol itself doesn't impose a strict limit on message size, but practical limitations come from network constraints, client/server memory, and processing capabilities. If you're sending large amounts of data, it might be better to use a different mechanism or split the data into smaller chunks.
    
6. **Data Serialization**: Socket.io uses JSON to serialize data. This means you can send any data that can be converted to JSON, including objects, arrays, strings, numbers, and more. However, functions, custom JavaScript classes, or objects with circular references can't be serialized directly. Make sure the data you're sending is serializable.
    
7. **Performance**: Sending many small messages in rapid succession can have more overhead than sending fewer, larger messages. On the other hand, very large messages can block the event loop or lead to performance issues. Aim for a balance based on your application's needs.
    
8. **Data Integrity and Validation**: Always validate and sanitize the data received from clients. Never trust the client-side data implicitly, as malicious users can tamper with it.