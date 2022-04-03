# webserv

42 project, recoding our own web server in C++. A program capable of running an HTTP server, handling requests, and parsing configuration files.
webserv is a HTTP/1.1 server written in C++98. It must be conditionnal compliant with RFC 7230 to 7235.

## Usage

```shell
# Compile the sources
make
```
```shell
# Run the server
./webserv [config_file]
```
## Configuration File

#### host : ```host ip address```

sets configuration depending on the given uri.

#### port : ```listen ports (support multiple);```

bind the given address to the port. if no address is given, binds 0.0.0.0.

#### server_name : ```server_name name ...;```

sets names of a virtual server.

#### root : ```root path;```

sets the directory for requests.

#### allowed_methods : ```allowed_methods: GET,POST,...```

sets the allowed methods for the root.

#### error_page : ```error_page:[error code]:[error page path]```

defines the URI that will be shown for the specified errors.

#### location : ```upload: / | /*.extension | /path/folder ```

defines the requests location.

#### autoindex : ```autoindex=on|off``` (default off)

enables or disables the directory listing output.

#### index : ```index file ...;```

defines files that will be used as an index.

#### cgi : ```cgi_uri=uri;```

defines a CGI binary that will be executed for the given extension.

#### limit_client_body : ```limit_client_body=number``` (default unlimited)

It sets the maximum allowed size of the client request body, specified in the “Content-Length” request header field.


### Example

```
server
[
    host:0.0.0.0
    port:80
    port:22

    server_name:localhost
    allowed_methods:GET

    location:/
    {
        root=website
        default=index.html
        autoindex=on
    }

    error_page:401:website/error_page/401.html
    error_page:403:website/error_page/403.html

    location:/*.bla
    {
        allowed_methods=POST
        cgi_uri=/users/layeredchoas/test/
    }

    location:/dir
    {
        root=/users/layeredchoas
        default=TestFile
        autoindex=on
    }

    location:/autoindex
    {
        root=/users/layeredchoas/files
        default=nothing
        autoindex=on
    }

    location:/upload
    {
        root=/users/layeredchoas/upload_folder
        allowed_methods=GET,PUT,HEAD,POST
        limit_client_body=20
    }

    location:/methods
    {
        allowed_methods=HEAD
    }

    location:/private/
    {
        root=/goinfre/ayennoui/ybouddou/private
        default=payments
        access=/goinfre/ayennoui/ybouddou/private/.access.prv
    }

]
```


### HTTP 1.1 (standard to follow) :

[HTTP/1.1 (RFC 2616)](https://www.rfc-editor.org/rfc/rfc2616.html)

[HTTP/1.1 : Message Syntax and Routing (RFC 7230)](https://www.rfc-editor.org/rfc/rfc7230.html)

[HTTP/1.1 : Semantics and Content (RFC 7231)](https://www.rfc-editor.org/rfc/rfc7231.html)

[HTTP/1.1 : Conditional Requests (RFC 7232)](https://www.rfc-editor.org/rfc/rfc7232.html)

[HTTP/1.1 : Range Requests (RFC 7233)](https://www.rfc-editor.org/rfc/rfc7233.html)

[HTTP/1.1 : Caching (RFC 7234)](https://www.rfc-editor.org/rfc/rfc7234.html)

[HTTP/1.1 : Authentication (RFC 7235)](https://www.rfc-editor.org/rfc/rfc7235.html)

### Other HTTP (legacy / future) :

[HTTP/1.0 (RFC 1945)](https://www.rfc-editor.org/rfc/rfc1945.html)

[HTTP/2 (RFC 7240)](https://www.rfc-editor.org/rfc/rfc7540.html)

[HTTP/2 : Header Compression (RFC 7241)](https://www.rfc-editor.org/rfc/rfc7541.html)

[FTP (RFC 959)](https://www.rfc-editor.org/rfc/rfc959.html)

### HTTP Header Syntax

[HTTP Request Methods](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)

[HTTP Status Codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

[HTTP Header Break Style](https://stackoverflow.com/questions/5757290/http-header-line-break-style)

### Select and non-blocking

[Select](https://www.lowtek.com/sockets/select.html)

[Non-blocking I/O](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzab6/xnonblock.htm)

### CGI

[CGI : Getting Started](http://www.mnuwer.dbasedeveloper.co.uk/dlearn/web/session01.htm)

[CGI 1.1 Documentation](http://www.wijata.com/cgi/cgispec.html#4.0)
