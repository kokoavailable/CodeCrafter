# Redis Protocol Overview

Redis supports various data structures, such as **lists**, **hashes**, **hyperloglogs**, and **pub/sub**, making it versatile for a wide range of use cases. It is known for its **high throughput**, and as a **single-threaded** server, it avoids concurrency issues.

---

### Example: Setting a Key in Redis with Python

**Python Code:**

```python
import redis

cli = redis.Redis()
cli.set('a', 'hello')
```

**Client Transmission to Redis Server (Redis Protocol):**

```
*3\r\n                # Total number of arguments (3)
$3\r\n                # Byte length of the first argument (3 bytes: "SET")
SET\r\n
$1\r\n                # Byte length of the second argument (1 byte: "a")
a\r\n
$5\r\n                # Byte length of the third argument (5 bytes: "hello")
hello\r\n
```

**Server Response:**

```
+OK\r\n               # Indicates successful execution of the SET command
```

---

### Example: Error Handling

If you attempt to increment the value of the key `'a'` (which is a string) using the `INCR` command, you will encounter an error:

**Python Code:**

```python
cli.incr('a')
```

**Server Response:**

```
-ERR value is not an integer or out of range\r\n
```

---

### Retrieving the Value of a Key

**Python Code:**

```python
cli.get('a')
```

**Client Transmission:**

```
*2\r\n                # Total number of arguments (2)
$3\r\n                # Byte length of the first argument (3 bytes: "GET")
GET\r\n
$1\r\n                # Byte length of the second argument (1 byte: "a")
a\r\n
```

**Response (if the key exists):**

```
$5\r\n                # Byte length of the value (5 bytes: "hello")
hello\r\n
```

---

### Capturing Redis Traffic with `ngrep`

To monitor Redis communication on a local server, you can use `ngrep` to capture traffic:

```bash
sudo ngrep -d lo0 -t '' 'tcp and port 6379'
```

This command:

- **`-d lo0`**: Specifies the loopback interface (used when Redis is bound to localhost).
- **`-t`**: Enables timestamped output.
- **`'tcp and port 6379'`**: Filters traffic on the Redis default port (6379)

- # Redis Serialization Protocol (RESP)

RESP is a protocol used by Redis for communication between clients and servers. 
Each data type is identified by a specific prefix, allowing clients to efficiently process responses.

## RESP Types and Prefixes

| **RESP Type**     | **Prefix** | **Description**                                              |
| ----------------- | ---------- | ------------------------------------------------------------ |
| **Simple String** | `+`        | Represents a success message in plain text. (`+OK`, `+PONG`) |
| **Error Message** | `-`        | Represents an error message. (`-ERROR`, `-WRONGTYPE`)        |
| **Integer**       | `:`        | Represents an integer value. (`:1000`)                       |
| **Array**         | `*`        | Represents multiple data values. (`*2\r\n$3\r\nfoo\r\n$3\r\nbar\r\n`) |
| **Bulk String**   | `$`        | Represents a string with a specified length. (`$3\r\nfoo\r\n`) |
| **Null Value**    | `-1`       | Indicates the absence of a value. (`$-1` or `*-1`)           |


https://lethain.com/redis-protocol/
