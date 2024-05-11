# Preliminaries
> [!important]
> References: https://zhuanlan.zhihu.com/p/497982541
> [Sockets](../../../../Machine_Structures/11_Network_Programming/Sockets.md)

## What is Proxy
> [!def]
> ![](Proxy_Lab.assets/image-20240410200003426.png)



## Serving Static Content



## Serving Dynamic Content
> [!important]




## Test and Debugging
> [!important]
> 1. `./proxy portnum` to start the server at localhost:portnum
> 2. `telnet localhost 61230` to connect to the server and send HTTP requests
> 3. `./driver.sh` to test the basic functionality of the program.(Remember to save all the files related to testing as `LF` instead of `CRLF`). Including `driver.sh, free-port.sh, port-for-user.pl`
> 4. If there is `netstat: command not found`, then execute `sudo apt install netstat`.






# Part I: Sequential Proxy Server
## Design Idea
> [!algo]
> 本质上就是在`Client Side`和`Server Side`中加入了一个中转站，做一个请求转发。


## Code Implementation
> [!code]
```c
#include <stdio.h>
#include "csapp.h"

/* Recommended max cache and object sizes */
#define MAX_CACHE_SIZE 1049000
#define MAX_OBJECT_SIZE 102400

/* You won't lose style points for including this long line in your code */
static const char *user_agent_hdr = "User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:10.0.3) Gecko/20120305 Firefox/10.0.3\r\n";


/* 
   Proxy Server Helper Functions
*/
void doit(int fd);
void read_requesthdrs(rio_t *rp);
int parse_line(char* lineBuf, char* key, char* value);
int parse_uri(char *uri, char *hostname, char *filepath, char* port);
void get_filetype(char *filename, char *filetype);
void clienterror(int fd, char *cause, char *errnum, char *shortmsg, char *longmsg);


/*
  Newly Added: Proxy
*/

/**
   Forward the message from client to the server
   - client_rfd: Reliable communication channel between proxy and client
   - client_fd: Socket channel between proxy and client
   - conn_fd: 
*/
void forwardRequestHeaders(rio_t* client_rio, int server_fd, char* hostname);
void forwardResponse(rio_t* server_rio, int client_fd);



int main(int argc, char **argv)
{
    int listenfd, connfd;
    char hostname[MAXLINE], port[MAXLINE];
    socklen_t clientlen;
    struct sockaddr_storage clientaddr;

    /* Check command line args */
    if (argc != 2) {
	fprintf(stderr, "usage: %s <port>\n", argv[0]);
	exit(1);
    }

    listenfd = Open_listenfd(argv[1]);
    while (1) {
        clientlen = sizeof(clientaddr);
        connfd = Accept(listenfd, (SA *)&clientaddr, &clientlen); //line:netp:tiny:accept
        Getnameinfo((SA *) &clientaddr, clientlen, hostname, MAXLINE, 
                    port, MAXLINE, 0);
        printf("Accepted connection from (%s, %s)\n", hostname, port);
        doit(connfd);                                             //line:netp:tiny:doit
        Close(connfd);                                            //line:netp:tiny:close
    }
}
/* $end tinymain */

/*
 * doit - handle one HTTP request/response transaction
 */
/* $begin doit */
void doit(int client_fd) 
{
    // int is_static;
    // struct stat sbuf;
    char buf[MAXLINE], method[MAXLINE], uri[MAXLINE], version[MAXLINE];
    char hostname[MAXLINE], port[MAXLINE], filepath[MAXLINE];
    rio_t rio_client;  // Reliable channel between proxy and client
    rio_t rio_server;  // Reliable channel between proxy and tiny server

    /* 1. Read request line */
    Rio_readinitb(&rio_client, client_fd);
    if (!Rio_readlineb(&rio_client, buf, MAXLINE))  //line:netp:doit:readrequest
        return;
    // printf("%s", buf);

    // e.g. GET https://www.cmu.edu/hub/index.html HTTP/1.1
    sscanf(buf, "%s %s %s", method, uri, version);       //line:netp:doit:parserequest
    
    // Add support for GET and POST requests
    if (strcasecmp(method, "GET") && strcasecmp(method, "POST")) {                     //line:netp:doit:beginrequesterr
        clienterror(client_fd, method, "501", "Not Implemented",
                    "Tiny does not implement this method");
        return;
    }

    // Parse URI
    // printf("Parsing URI");
    memset(port, 0, strlen(port));
    if (parse_uri(uri, hostname, filepath, port)) {
        // error handling
    }

    /* 2. Read/Forward Requests Line and open connection  */ 
    // printf("Reading Request Line...");
    // Request Line:  GET /hub/index/html HTTP/1.0
    char requestLine[MAXLINE];
    strcat(requestLine, method);
    strcat(requestLine, " ");
    strcat(requestLine, filepath);
    strcat(requestLine, " ");
    strcat(requestLine, "HTTP/1.0\r\n");

    // Open connection to the server
    // printf("Open connection to tiny server at %s:%s", hostname, port);
    int server_fd = Open_clientfd(hostname, port);
    // printf("Success openning");

    // Forward Requestline to the tiny server
    // printf("\n Now forwarding the requests\n");
    Rio_writen(server_fd, requestLine, strlen(requestLine));
    memset(requestLine, 0, strlen(requestLine));

    /* 3. Forward the request headers to the server */
    // Forward the request headers to Tiny Server
    forwardRequestHeaders(&rio_client, server_fd, hostname);

    /* 4. Receive the response from the tiny server */
    // printf("Receiving and forwarding Responses\n");
    // Initialize buffered channel
    Rio_readinitb(&rio_server, server_fd);

    // Forward response header and body
    forwardResponse(&rio_server, client_fd);
}
/* $end doit */


/*
  forwardRequestHeaders -  Forwarding Request to the Target Server from Client
  client_rio: Buffered input from client(Rio_readlineb)
  server_fd: Socket descriptor to tiny server(Rio_writen)
*/
void forwardRequestHeaders(rio_t* client_rio, int server_fd, char* hostname) {

    char buf[MAXLINE], lineKey[MAXLINE], lineValue[MAXLINE];

    int isHost = 0;
    int isUserAgent = 0;
    int isConnection = 0;
    int isProxyConnection = 0;
    

    // Parse Request Headers and send to the tiny server
    while(1) {       
        Rio_readlineb(client_rio, buf, MAXLINE);

        // Request header end
        if (!strcmp(buf, "\r\n")) {
            break;
        }

        printf("%s", buf);
        parse_line(buf, lineKey, lineValue);

         if (strcmp(lineKey, "Host") == 0) {
            isHost = 1;
        } else if (strcmp(lineKey, "User-Agent") == 0) {
            isUserAgent = 1;
        } else if (strcmp(lineKey, "Connection") == 0) {
            isConnection = 1;
        } else if (strcmp(lineKey, "Proxy-Connection") == 0) {
            isProxyConnection = 1;
        }

        Rio_writen(server_fd, buf, strlen(buf));
    }

    // If user doesn't provide any of Host/User-Agent/Connection/Proxy-Connection
    if (!isHost) {
        strcpy(buf, "Host: ");
        strcat(buf, hostname);
        Rio_writen(server_fd, buf, strlen(buf));
    }

    if (!isUserAgent) {
        strcpy(buf, "User-Agent: ");
        strcat(buf, user_agent_hdr);
        Rio_writen(server_fd, buf, strlen(buf));
    }

    if (!isConnection) {
        strcpy(buf, "Connection: close\r\n");
        Rio_writen(server_fd, buf, strlen(buf));
    }

    if (!isProxyConnection) {
        strcpy(buf, "Proxy-Connection\r\n");
        Rio_writen(server_fd, buf, strlen(buf));
    }

    // Terminate the request header
    strcpy(buf, "\r\n");
    Rio_writen(server_fd, buf, strlen(buf));

    return;
}


/*
  forwardResponse - Parsing the response from the target server and send it to client
  server_rio: Buffered Input from the server(Rio_readlineb/Rio_readnb)
  client_fd: Socket descriptor of client connection(Rio_writen)
*/
void forwardResponse(rio_t* server_rio, int client_fd) {

    char line[MAXLINE], buf[MAXBUF];

    // Forward response line
    if (!Rio_readlineb(server_rio, line, MAXLINE))  //line:netp:doit:readrequest
        return;
    printf("%s", line);
    Rio_writen(client_fd, line, strlen(line));

    // Forward response header
    while (1) {
        Rio_readlineb(server_rio, line, MAXLINE);
        // Response header end
        if (!strcmp(line, "\r\n")) {
            break;
        }
        Rio_writen(client_fd, line, strlen(line));
    }

    // Separate the response header with response body
    strcpy(line, "\r\n");
    Rio_writen(client_fd, line, strlen(line));


    int nread;
    // Forward Response body, using Rio_readnb since the file is binary
    while((nread = Rio_readnb(server_rio, buf, MAXBUF)) > 0) {
        Rio_writen(client_fd, buf, nread);
    }

    // Rio_readnb returns 0 only on EOF
    return;
}



/*
  Parse one line of request header, extracting its key and value
*/
int parse_line(char* lineBuf, char* key, char* value) 
{
    char buf[MAXBUF];
    memcpy(buf, lineBuf, strlen(lineBuf) + 1); // +1 to include null terminator
    char* delimit = strchr(buf, ':');
    *delimit = 0;
    strcpy(key, buf);
    strcpy(value, delimit + 2);

    return 0;
}


/*
 * parse_uri - parse URI into 
    Host: www.cmu.edu
    pathname: /hub/index.html
 */
/* $begin parse_uri */
int parse_uri(char *uri, char *hostname, char *filepath, char* port) 
{
    // uri : http://www.cmu.edu/hub/index.html
    char* loc = strchr(uri, '/');
    char* start = loc + 2;

    char* end = strchr(start, '/');
    strcpy(filepath, end);
    *end = '\0';

    // See if there is a specified port in the URL
    char* p = strchr(start, ':');
    if (p) {
        strcpy(port, p + 1);
        *p = 0;
    }

    strcpy(hostname, start);

    return 0;
}
/* $end parse_uri */


/*
 * clienterror - returns an error message to the client
 */
/* $begin clienterror */
void clienterror(int fd, char *cause, char *errnum, 
		 char *shortmsg, char *longmsg) 
{
    char buf[MAXLINE];

    /* Print the HTTP response headers */
    sprintf(buf, "HTTP/1.0 %s %s\r\n", errnum, shortmsg);
    Rio_writen(fd, buf, strlen(buf));
    sprintf(buf, "Content-type: text/html\r\n\r\n");
    Rio_writen(fd, buf, strlen(buf));

    /* Print the HTTP response body */
    sprintf(buf, "<html><title>Tiny Error</title>");
    Rio_writen(fd, buf, strlen(buf));
    sprintf(buf, "<body bgcolor=""ffffff"">\r\n");
    Rio_writen(fd, buf, strlen(buf));
    sprintf(buf, "%s: %s\r\n", errnum, shortmsg);
    Rio_writen(fd, buf, strlen(buf));
    sprintf(buf, "<p>%s: %s\r\n", longmsg, cause);
    Rio_writen(fd, buf, strlen(buf));
    sprintf(buf, "<hr><em>The Tiny Web server</em>\r\n");
    Rio_writen(fd, buf, strlen(buf));
}
/* $end clienterror */
```


## Testing Results
> [!test]
> ![](Proxy_Lab.assets/image-20240511093753348.png)







# Part II: Concurrent Proxy Server
## Design Idea I: Prethreading
> [!important]
> ![](Proxy_Lab.assets/image-20240511095524146.png)
> **Prethreading**, also known as **thread pooling**, is a technique used in concurrent programming where a fixed number of threads are created and maintained in a pool to handle tasks or requests. Instead of creating a new thread for each task, tasks are assigned to existing threads from the pool.
> 
> This approach **improves performance by reducing the overhead associated with creating and destroying threads.**
> ![](Proxy_Lab.assets/image-20240511102221546.png)



## Design Idea II: Producer&Consumer
> [!important]
> See [Semaphores in Producer and Consumer Problem](../../../3_Synchronizations/Synchronization_Problems.md#Solution%202%20-%20Semaphores)
> The functionalities of semaphore is integrated into a `sbuf` package, which uses the idea of circular buffer.
> https://csapp.cs.cmu.edu/3e/code.html

> [!algo]
> 本质上我们只需要使用把`doit()`函数作为线程的任务，然后使用`sbuf`管理任务的执行即可。
> - 原来的`doit(int connfd)`有一个参数，表示`Client`连接，但是现在这个参数会被存放在一个多线程共享的`Circular Buffer`中，每个线程从这个数据结构中取`clientfd`(如果有的话)即可，所以我们可以将这个参数去掉。
> - 定义线程的时候只需要`Pthread_create(&tid[i], NULL, doit, NULL)`即可。


## Code Implementation
> [!code]
```c
#include <stdio.h>
#include "csapp.h"
#include "sbuf.h"

/* Recommended max cache and object sizes */
#define MAX_CACHE_SIZE 1049000
#define MAX_OBJECT_SIZE 102400
#define NTHREADS 8
#define SBUFSIZE 32

/* You won't lose style points for including this long line in your code */
static const char *user_agent_hdr = "User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:10.0.3) Gecko/20120305 Firefox/10.0.3\r\n";
sbuf_t sbuf; /* Circular Buffer used for Thread Pooling */

/* 
   Proxy Server Helper Functions
*/
void* thread_func(void* args);
void doit(int fd);
void read_requesthdrs(rio_t *rp);
int parse_line(char* lineBuf, char* key, char* value);
int parse_uri(char *uri, char *hostname, char *filepath, char* port);
void get_filetype(char *filename, char *filetype);
void clienterror(int fd, char *cause, char *errnum, char *shortmsg, char *longmsg);


/*
  Newly Added: Proxy
*/

/**
   Forward the message from client to the server
   - client_rfd: Reliable communication channel between proxy and client
   - client_fd: Socket channel between proxy and client
   - conn_fd: 
*/
void forwardRequestHeaders(rio_t* client_rio, int server_fd, char* hostname);
void forwardResponse(rio_t* server_rio, int client_fd);



int main(int argc, char **argv)
{
    int listenfd, connfd;
    char hostname[MAXLINE], port[MAXLINE];
    socklen_t clientlen;
    struct sockaddr_storage clientaddr;
    pthread_t threads[NTHREADS];


    /* Check command line args */
    if (argc != 2) {
        fprintf(stderr, "usage: %s <port>\n", argv[0]);
        exit(1);
    }


    /* Don't forget to initialize the sbuf */
    sbuf_init(&sbuf, SBUFSIZE);


    // Create a thread pool with NTHREADS in it.
    for (int i = 0; i < NTHREADS; i++) {
        Pthread_create(&threads[i], NULL, thread_func, NULL);
    }

    listenfd = Open_listenfd(argv[1]);
    while (1) {
        clientlen = sizeof(clientaddr);
        connfd = Accept(listenfd, (SA *)&clientaddr, &clientlen); //line:netp:tiny:accept
        sbuf_insert(&sbuf, connfd);      
        Getnameinfo((SA *) &clientaddr, clientlen, hostname, MAXLINE, 
                    port, MAXLINE, 0);
        printf("Accepted connection from (%s, %s)\n", hostname, port);
        // Insert the task(connfd) into the circular buffer                                                          
    }
}
/* $end tinymain */


/*
 * thread_func
*/
void* thread_func(void* args) {
    // Detach the thread, so that it will free up all the resources
    // (like those allocated on the stack above) immediately after it
    // terminates.
    Pthread_detach(Pthread_self());
    // Constantly fetching connection descriptor from the circular buffer to do the work
    while(1) {
        /* Get the connfd */
        int client_fd = sbuf_remove(&sbuf);
        doit(client_fd);
            
        // Don't forget the close the connection 
        Close(client_fd);   
    }
}


// ... 下面的都一样
/*
 * doit - handle one HTTP request/response transaction
 */
/* $begin doit */
//void doit(int client_fd)
```


## Testing Results
> [!test]
> Remember to add a `python3` at the front to perform the testing as expected.
> ![](Proxy_Lab.assets/image-20240511112820902.png)
> Testing Result:
> 
> ![](Proxy_Lab.assets/image-20240511112313801.png)



## Caveats I: Prematurely Closed Connections
> [!important]
> ![](Proxy_Lab.assets/image-20240511112513727.png)
> **CSAPP pp1000**
> 
> So even if we pass the test above, we still need to handle this scenario in order to be a robust server.
> 
```c
/*
    sigpipe_handler: Handle the prematurely closed connection
    instead of ignoring it(otherwise it will terminate the main process)
    and all the threads(casuse the server to shut down)

    So we need to at least capture it instead of the default behavior of the
    SIGPIPE(terminate the process).
*/
void sigpipe_handler(int signum) {
    printf("Caught SIGPIPE signal %d\n", signum);
}


/* Main function begins */
int main(int argc, char **argv)
{
    int listenfd, connfd;
    char hostname[MAXLINE], port[MAXLINE];
    socklen_t clientlen;
    struct sockaddr_storage clientaddr;
    pthread_t threads[NTHREADS];


    /* Check command line args */
    if (argc != 2) {
        fprintf(stderr, "usage: %s <port>\n", argv[0]);
        exit(1);
    }

    /* Install the SIGPIPE Handler */
    Signal(SIGPIPE, sigpipe_handler);


    /* Don't forget to initialize the sbuf */
    sbuf_init(&sbuf, SBUFSIZE);


    // Create a thread pool with NTHREADS in it.
    for (int i = 0; i < NTHREADS; i++) {
        Pthread_create(&threads[i], NULL, thread_func, NULL);
    }

    listenfd = Open_listenfd(argv[1]);
    while (1) {
        clientlen = sizeof(clientaddr);
        connfd = Accept(listenfd, (SA *)&clientaddr, &clientlen); //line:netp:tiny:accept
        sbuf_insert(&sbuf, connfd);      
        Getnameinfo((SA *) &clientaddr, clientlen, hostname, MAXLINE, 
                    port, MAXLINE, 0);
        printf("Accepted connection from (%s, %s)\n", hostname, port);
        // Insert the task(connfd) into the circular buffer                                                          
    }
}
```



# Part III: Caching 
## Design Idea I: Proxy Caching


## Design Idea II: Reader and Writer Problem



## Code Implementation
> [!code]
```c

```



## Testing Results
> [!test]

