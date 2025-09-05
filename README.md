

# Multi-Threaded Proxy Server with Cache

**Author:** Nishtha Dahiya
**Language:** C
**Project Type:** Systems Programming / Networking

---

## Table of Contents

1. [Introduction](#introduction)
2. [Project Motivation](#project-motivation)
3. [Features](#features)
4. [System Components Used](#system-components-used)
5. [Limitations](#limitations)
6. [Potential Extensions](#potential-extensions)
7. [Project Files](#project-files)
8. [How to Run](#how-to-run)
9. [Demo Instructions](#demo-instructions)


---

## Introduction

This project implements a **multi-threaded HTTP proxy server** with caching functionality. The proxy server acts as an intermediary between a client (such as a web browser) and a remote server.

Key objectives:

* Handle multiple client requests concurrently using **threads**.
* Store frequently requested responses in a **cache** for faster retrieval.
* Demonstrate proper concurrency handling with **semaphores** and **mutex locks**.

### Working Flow

1. A client sends an HTTP GET request to the proxy server.
2. The proxy server checks if the requested URL is present in the **cache**.

   * If the URL is found, the cached response is sent to the client.
   * If the URL is not found, the request is forwarded to the remote server.
3. The response from the remote server is received by the proxy, forwarded to the client, and stored in the cache for future requests.
4. The proxy server handles multiple client connections simultaneously using **threads**, and limits concurrency using a **semaphore**.

##  System Architecture diagramatic layout 
![system_architecture](https://github.com/user-attachments/assets/268b3b1a-6d9d-4b6c-8ad1-c2c45044223a)

## Sustem block diagram 
<img width="1368" height="865" alt="system_blockdiag" src="https://github.com/user-attachments/assets/474300a4-7d30-4e14-8208-dcfb72132d8d" />

## Request handling flowchart
<img width="464" height="693" alt="flowachart" src="https://github.com/user-attachments/assets/68814b34-308d-4928-9702-9f949a2f224c" />

## Sequence Diagram 
<img width="851" height="756" alt="sequence diag" src="https://github.com/user-attachments/assets/9393c89f-4a3e-438d-8658-ad641cff44f5" />


## Socket Client server model 
<img width="330" height="375" alt="Socket_server-1" src="https://github.com/user-attachments/assets/0394f5b4-8a42-4c6a-9dfc-0e9861c458eb" />

## Project Motivation

The project is designed to help understand:

* How HTTP requests flow from a client to a server and back.
* How to handle multiple clients efficiently using **multi-threading**.
* The implementation of **locking mechanisms** for safe concurrent access to shared resources like the cache.
* Concepts of caching used in browsers and servers, including the **Least Recently Used (LRU)** algorithm.

Benefits of using a proxy server:

* Reduces server load and improves response time through caching.
* Can filter and restrict access to certain websites.
* Enhances privacy by masking the client’s IP address.
* Can be extended to provide encryption or secure request handling.

---

## Features

* **Multi-threaded server:** Each client request is handled in a separate thread.
* **Semaphore-based concurrency control:** Limits the number of simultaneous clients without needing to use `pthread_join()`.
* **LRU cache implementation:** Stores responses in a linked list, evicting the least recently used elements when the cache is full.
* **Error handling:** Sends appropriate HTTP error codes (400, 403, 404, 500, 501, 505) for invalid or unsupported requests.
* **Supports HTTP/1.0 and HTTP/1.1 GET requests**.
* **Extensible for future enhancements** like POST requests or request filtering.



---

## System Components Used

## UML diag 
<img width="851" height="730" alt="umldiag" src="https://github.com/user-attachments/assets/f977e37c-67bb-47cf-bd1b-145da3c452dd" />

* **Threads:** `pthread_create` for multi-threading.
* **Semaphore:** `sem_wait` and `sem_post` to control maximum concurrent clients.
* **Mutex locks:** To safely access and modify the shared cache.
* **Cache:** Implements an LRU cache using a linked list.
* **Sockets:** TCP sockets to communicate with clients and remote servers.

---

## Limitations

* The cache stores separate responses for multiple clients accessing the same URL simultaneously. This may cause incomplete responses during retrieval.
* Fixed cache element size may prevent very large websites from being cached completely.
* Only GET requests are supported; POST or other HTTP methods are not implemented.
* Currently tested only for **HTTP** (non-SSL) sites; HTTPS is not supported.

---

## Potential Extensions

* Implement **multiprocessing** for parallel execution to improve performance.
* Add support for **POST** and other HTTP methods.
* Implement **website filtering** based on URL or content.
* Add SSL/TLS support for secure requests.
* Enhance cache management with dynamic sizing or alternative eviction strategies.

---

## Project Files

* `proxy_server_with_cache.c` – Main proxy server implementation with caching.
* `proxy_server_without_cache.c` – Version of the server without caching (optional).
* `proxy_parse.c` and `proxy_parse.h` – HTTP parsing and request handling functions.
* `Makefile` – Build instructions for compiling the project.
* `README.md` – Project documentation.

---

## RUNNING DEMO 

!. proxy URL 
 ![proxyurl](https://github.com/user-attachments/assets/cfa46b62-79f9-4fc0-9f43-c1077bb31f2a)

 2.terminal 
 ![terminal](https://github.com/user-attachments/assets/2bda00ba-4ea8-4f5f-adff-b37a04dee125)




3. Example site 
<img width="1470" height="956" alt="testsite" src="https://github.com/user-attachments/assets/dd06365c-dc5d-44f0-a10f-c221232e7f6e" />


## How to Run

1. Clone the repository


2. Compile the project using the Makefile:

```bash
$ make all
```

3. Start the proxy server on a desired port (e.g., 8080):

```bash
$ ./proxy 8080
```

4. Configure your browser to use the proxy:

   * **Server:** `127.0.0.1`
   * **Port:** `8080`

5. Open websites in the browser using the format:

```
http://localhost:8080/http://example.com
```

---

### Example Sites to Test

Use only **HTTP** (non-SSL) sites:

* `http://neverssl.com` – For testing non-SSL connections.
* `http://example.com` – Standard example domain.
* `http://info.cern.ch` – First website ever created.
* `http://portquiz.net:80` – Test service that responds on any port.
* `http://httpforever.com` – For testing persistent connections.
* `http://speedtest.tele2.net` – For downloading test files over HTTP.

**Note:** Disable your browser cache to see proxy caching in action.

---

## Demo Instructions

1. Run the proxy server.
2. Access a website for the **first time**:

   * Output will show **“url not found”**, indicating a cache miss.
3. Access the same website **again**:

   * Output will show **“Data retrieved from the Cache”**, demonstrating cache hit and faster response.



If you want, I can also **create a “Code Walkthrough” section** explaining the main files and functions line by line. It would make the README even more thorough for evaluators. Do you want me to do that?
