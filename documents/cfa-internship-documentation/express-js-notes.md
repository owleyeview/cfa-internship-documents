# Express.js

"Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications."
- Without Express, setting up a server in Node.js requires more boilerplate and manual setup.

## Notes
### **How does Express simplify tasks?**

1. **Routing**: With plain Node.js, handling different routes requires manual parsing of the request URL. Express provides a clean API for defining routes.
    
    - With Express:
       ```javascript
        
        app.get('/users', (req, res) => {
           res.send('Users endpoint'); 
        });
        ```
        
        
    - Without Express:
        ```Javascript

        const http = require('http'); 
        const url = require('url');  
        const server = http.createServer((req, res) => {
           const parsedUrl = url.parse(req.url, true);
           if (parsedUrl.pathname === '/users' && req.method === 'GET') {
                res.end('Users endpoint');
           } 
	    });
        ```
        
2. **Middleware**: Express lets you use middleware functions that can execute any code, make changes to the request and response objects, or end the request-response cycle. This is immensely useful for tasks like logging, authentication, and more.
    
3. **Error Handling**: Express provides a default error handler so you don’t need to write your own to start getting useful error responses.
    
4. **Template Engines**: While Node.js can serve HTML files, Express makes it easier to integrate with various template engines like Pug, Mustache, etc., for server-side rendering.
    
5. **Static Files**: Serving static files (e.g., images, CSS, JavaScript) is straightforward with Express's built-in middleware.
    
6. **JSON/URL-encoded Form Parsing**: With built-in middleware in Express, parsing incoming requests with JSON payloads or URL-encoded data is a breeze.
