# ed-php-cgi-fpm
By [article](https://medium.com/@miladev95/cgi-vs-fastcgi-vs-php-fpm-afbc5a886d6d)


## CGI:
CGI stands for “Common Gateway Interface.” It is a standard protocol that defines how web servers can interact with external applications or scripts to process HTTP requests and generate dynamic web content. CGI was one of the first methods used for dynamic web page generation before the advent of server-side scripting languages like PHP, Python, and Ruby.

When a client (usually a web browser) sends an HTTP request to a web server, the server processes the request and, in the case of static content (like HTML and images), directly serves the requested file. However, when the requested content is dynamic and needs to be generated on the fly, the server can use CGI to communicate with external programs to handle the processing.

Here’s a basic overview of how CGI works:

- Client sends an HTTP request to the web server.
- The web server receives the request and identifies that the requested content requires dynamic processing.
- The web server passes the request to the CGI program or script along with the necessary environment variables and data from the request (e.g., query parameters, form data, etc.).
- The CGI program processes the request and generates the dynamic content, typically in the form of HTML.
- The CGI program sends the generated content back to the web server.
- The web server returns the dynamic content in the HTTP response to the client, which renders it in the web browser.

CGI programs can be written in various programming languages, such as Perl, Python, Ruby, C, C++, etc. They are executed as separate processes from the web server, which means that each request to a CGI program incurs the overhead of starting a new process.

While CGI was revolutionary in its time and enabled dynamic web content, it has certain limitations, including performance overhead and scalability issues. As a result, modern web development has largely moved away from CGI in favor of more efficient and scalable server-side scripting technologies like PHP, Node.js, and various application frameworks.

Today, CGI is mostly used in specific cases where compatibility with legacy systems or specialized environments is required. For general-purpose web development, more efficient alternatives are preferred.

## FastCGI:

FastCGI is a variation of the Common Gateway Interface (CGI) that addresses the performance and scalability limitations of traditional CGI. It is a protocol that allows web servers to communicate with external application processes efficiently, enabling dynamic content generation for web applications.

With traditional CGI, a new process is spawned for each request, leading to a significant performance overhead. FastCGI improves upon this by introducing a persistent application process pool that remains alive even after processing a request. This process pool eliminates the need to start a new process for each incoming request, reducing the overhead and providing better performance and resource utilization.

Here’s how FastCGI works:

- Client sends an HTTP request to the web server.
- The web server passes the request to the FastCGI application via a socket or TCP/IP connection, along with the necessary environment variables and request data.
- The FastCGI application processes the request and generates the dynamic content (e.g., HTML, JSON, etc.).
- Instead of terminating the application process, the FastCGI process remains alive and waits for the next request.
- The web server receives the response from the FastCGI application and sends it back to the client in the HTTP response.

FastCGI offers several advantages over traditional CGI:

- Reduced Overhead: By reusing application processes, FastCGI eliminates the overhead of creating and terminating processes for each request.
- Improved Performance: The persistent process pool leads to faster response times for subsequent requests, as the application doesn’t need to be reloaded for each new request.
- Resource Efficiency: The persistent process pool consumes fewer resources compared to spawning new processes for every request.
- Scalability: FastCGI allows web servers to handle a higher number of concurrent requests, improving the scalability of web applications.

FastCGI is widely used in web server configurations to handle dynamic content generation efficiently. Popular web servers like Nginx and Apache support FastCGI, making it a standard choice for hosting dynamic web applications written in languages like PHP, Python, Ruby, and more.

In summary, FastCGI is an extension of CGI that significantly improves the performance and resource utilization of web applications by employing a persistent application process pool to handle incoming requests.

## PHP-FPM:

PHP-FPM (FastCGI Process Manager) is a PHP-FPM is an alternative PHP FastCGI implementation that is widely used to serve PHP applications efficiently and securely. It works in conjunction with a web server (e.g., Nginx or Apache) to handle PHP requests via the FastCGI protocol.

PHP-FPM provides several benefits over traditional PHP CGI or mod_php (the Apache PHP module):

- FastCGI Process Management: PHP-FPM uses a process manager to control PHP child processes. These child processes handle incoming PHP requests, and PHP-FPM manages them based on configuration settings. The process manager allows for better control of process spawning, termination, and resource management, resulting in improved performance and reduced resource usage.
- Resource Pooling: PHP-FPM maintains a pool of worker processes that are kept alive and ready to handle incoming requests. This avoids the overhead of starting and stopping PHP processes for each request, making PHP-FPM more efficient and faster than traditional CGI.
- Isolation and Security: PHP-FPM runs PHP requests in separate isolated processes, which enhances security by isolating individual PHP requests from one another. This isolation prevents the potential sharing of data between different PHP requests and increases the overall security of PHP applications.
- Customizable Configuration: PHP-FPM allows users to customize the process manager’s behavior and configuration to match the server’s resources and requirements. This enables users to fine-tune PHP-FPM for optimal performance and stability.
- Scaling: PHP-FPM’s process management makes it easier to scale PHP applications horizontally by adjusting the number of PHP worker processes to handle increased traffic and workload.

PHP-FPM is the recommended way to serve PHP applications in modern web server configurations. It is commonly used with Nginx, but it can also be used with Apache or other web servers that support FastCGI.

To use PHP-FPM, you typically need to install it separately from your web server and configure it to work with the web server of your choice. The configuration process varies depending on the operating system and web server you are using, but most PHP installations come with PHP-FPM as an option.

Overall, PHP-FPM is a valuable tool for PHP application deployment, providing improved performance, security, and scalability for serving PHP-driven web applications.

In summary, CGI is the simplest and oldest method for executing server-side scripts but suffers from performance overhead. FastCGI improves upon CGI by introducing a persistent process pool, resulting in better performance. PHP-FPM, on the other hand, is a specific FastCGI implementation tailored for PHP execution, providing superior performance, scalability, and security for serving PHP applications. For modern PHP applications, PHP-FPM is the recommended method for handling dynamic content.
