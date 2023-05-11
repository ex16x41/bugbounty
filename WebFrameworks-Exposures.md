## Discover web app frameworks and their exposures (low, medium, high, critical) for bug bounties.

# Table of Web Frameworks by priority

| Web Framework | Method | Source|
|-----:|---------------:|---------------|
|Laravel (PHP)|   "Whoops! There was an error."            | google.com         | 
|  Symfony (PHP) Method 1  |  +plugin:SymfonyVerbosePlugin OR +plugin:SymfonyProfilerPlugin            | leakix.net        | 
| Symfony (PHP) Method 2    |     Set-Cookie: symfony=           | shodan.com         | 
| Symfony (PHP) Method 3    |     inurl:/frontend_dev.php/$         |   google.com         | 
| Symfony (PHP) Method 4    |     "SF_ROOT_DIR"         |   google.com         | 
| Django (credit fattselimi)   |    http.title:”DisallowedHost at /”      |   shodan.com         |
| Ruby on rails    |     Application Trace +  nil:NilClass (10%) TBD        |   google.com         | 
| Flask    |       Manual Testing    |   Burpsuite        | 
| ASP.NET  |     Manual Testing    |   Burpsuite        | 
| Play Framework |     Manual Testing    |   Burpsuite        | 

# Triggering exceptions (Improper Error Handling - OWASP)

| Type | Method|
|-----:|---------------:|
|Web Server |Search for random files and folders that will not be found (404s)      |
|Web Server | Try to request folders that exist and see the server behavior (403s, blank page, or directory listing).  |  
|Web Server | send a very large path, break the headers format, or change the HTTP version.     |
|Application | Identify possible input points where the application is expecting data.  | 
|Application|Analyse the expected input type (strings, integers, JSON, XML, etc.). |
|Application| Fuzz every input point based on the previous steps to have a more focused test scenario.   | 
|Application| Understand the service responding with the error message and try to make a more refined fuzz list to bring out more information or error details from that service (it could be a database, a standalone service, etc.). | 
|Application| Try access host via IP, may trigger this also  | 

## FLASK:
1."TypeError": indicates a type-related error, such as trying to perform an operation on an object of the wrong type.

2."NameError": indicates that a variable or function name was not defined.

3."KeyError": indicates that a key used to access a dictionary does not exist.

4."ValueError": indicates that an argument passed to a function or method is invalid.

5."AttributeError": indicates that an attribute or method does not exist for an object.

6."SyntaxError": indicates that there is a problem with the syntax of the code.

7."IndentationError": indicates that there is a problem with the indentation of the code.

8."ImportError": indicates that there is a problem importing a module or package 
