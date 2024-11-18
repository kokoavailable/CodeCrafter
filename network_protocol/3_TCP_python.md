## **What is TCP?**

TCP (Transmission Control Protocol) is a widely used network protocol. It serves as the foundation for higher-level protocols such as HTTP and SSH, making it an essential component for reliable data communication.

---

## **Key Functions in Python's `socket` Module**

Python's `socket` module provides essential networking primitives to build TCP servers. Here are the key methods you'll need to know:

### 1. `socket.create_connection`

Used to initiate outbound connections.

#### **Example Usage**

```python
# Connects to a TCP server running on localhost:8080
client_socket = socket.create_connection(("localhost", 8080))
```

---

### 2. `socket.create_server`

Creates a TCP server that listens for incoming connections.

#### **Example Usage**

```python
# Starts a TCP server listening on localhost:8080
server_socket = socket.create_server(("localhost", 8080))
```

---

### 3. `socket.Socket.accept`

Accepts incoming connections and blocks execution until a client connects.

#### **Example Usage**

```python
# Wait for an incoming connection
connection, address = server_socket.accept()
print(f"Accepted connection from {address}")
```

When a client connects, this method returns:

- A new socket object representing the connection.
- A tuple containing the client's address.

---

### 4. `socket.Socket.recv`

Reads data from a connection. The maximum size of data to read is specified by `bufsize`.

#### **Example Usage**

```python
data = connection.recv(1024)  # Reads up to 1024 bytes
```

- Returns a bytes object with the received data.
- An empty bytes object indicates that the client has closed the connection.

---

### 5. `socket.Socket.sendall`

Writes data to a connection. It ensures all data is sent in one go, even if the underlying buffer isn't large enough.

#### **Example Usage**

```python
connection.sendall(b"Hello, client!")  # Sends data as bytes
```

---

## **Building a Simple Echo TCP Server**

Now, let's put everything together to build a TCP server that echoes back any data it receives.

### **Code Example**

```python
import socket

# Start a TCP server on localhost:8080
with socket.create_server(("localhost", 8080), reuse_port=True) as server_socket:

    # Block until we receive an incoming connection
    connection, address = server_socket.accept()

    print(f"Accepted connection from {address}")

    # Read data
    data = connection.recv(1024)

    # Write the same data back
    connection.sendall(data)
```

### **Explanation**

1. **Server Setup**:
   - `socket.create_server(("localhost", 8080))`: Creates a TCP server bound to port 8080 on `localhost`.
   - `reuse_port=True`: Allows multiple processes to reuse the port (optional for most cases).

2. **Accept Connections**:
   - `server_socket.accept()`: Blocks until a client connects, then returns the connection socket and client address.

3. **Read and Echo Data**:
   - `connection.recv(1024)`: Reads up to 1024 bytes from the client.
   - `connection.sendall(data)`: Sends the received data back to the client.

---

## **Summary**

Here’s a quick recap of the functions we covered:

- **`socket.create_connection`**: Connects to a TCP server.
- **`socket.create_server`**: Starts a TCP server that listens for incoming connections.
- **`socket.Socket.accept`**: Accepts an incoming connection and blocks until one is established.
- **`socket.Socket.recv`**: Reads data from a connection.
- **`socket.Socket.sendall`**: Writes data to a connection.
