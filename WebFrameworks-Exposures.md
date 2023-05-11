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
| Django    |    TBD     |   google.com         |
| Ruby on rails    |     Application Trace +  nil:NilClass (10%) TBD        |   google.com         | 
| Flask    |       Manual Testing    |   Burpsuite & Web Manual         | 
| ASP.NET  |     Manual Testing    |   Burpsuite & Web Manual    | 
| Yii |     "exception" + "play slick" (TBD)   |   N/A        | 
| Generic Method 1 (mass)|  site:*.tld.* OR site:*.com "unexpected error" OR "Uncaught Exception" OR "fatal error" OR "Unknown column"     |  google.com       | 
| Generic Method 1 (targeted) |    N/A    |   N/A        | 
| N/A |    N/A    |   N/A        | 
| N/A |    N/A    |   N/A        | 

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

## Flask: Type of Errors
1."TypeError": indicates a type-related error, such as trying to perform an operation on an object of the wrong type.

2."NameError": indicates that a variable or function name was not defined.

3."KeyError": indicates that a key used to access a dictionary does not exist.

4."ValueError": indicates that an argument passed to a function or method is invalid.

5."AttributeError": indicates that an attribute or method does not exist for an object.

6."SyntaxError": indicates that there is a problem with the syntax of the code.

7."IndentationError": indicates that there is a problem with the indentation of the code.

8."ImportError": indicates that there is a problem importing a module or package 

## Symfony: Type of Errors
1.InvalidArgumentException: This exception is thrown when an argument passed to a function or method is not valid.

2.NotFoundHttpException: This exception is thrown when a requested resource or URL is not found.

3.AccessDeniedException: This exception is thrown when a user does not have sufficient permissions to access a resource.

4.RuntimeException: This is a generic exception that is thrown when an unexpected error occurs during the execution of a script or application.

5.HttpException: This is a base exception class for HTTP-related errors, such as 404 (Not Found) or 500 (Internal Server Error).

6.Twig_Error_Runtime: This exception is thrown by the Twig template engine, which is used by Symfony to render templates. It is typically caused by a syntax error or a missing variable in a template.

7.Doctrine\DBAL\Exception: This exception is thrown by the Doctrine database abstraction layer, which is used by Symfony to interact with databases. It is typically caused by a database-related error, such as a missing table or a syntax error in a SQL query.


## Keywords to check inside exceptions (because webf may be config'd with these below)
redis, API, DB, mysql, AD, path, server, database, username, password, key, secret, backend, admin, dir, port, URI, 


## Laravel: High or Critical Priority
![YDQcV](https://github.com/ex16x41/bugbounty/assets/44981946/075dfe16-0995-4be3-9833-2ab7aa8066a3)

## Symfony 1: High or Critical Priority
![error](https://github.com/ex16x41/bugbounty/assets/44981946/c7adac05-c24f-4fc7-951d-4e2ad433081c)

## Symfony 2: High or Critical Priority
![exceptions-in-dev-environment](https://github.com/ex16x41/bugbounty/assets/44981946/eea554ff-0c05-4e29-9bab-43db25f9180c)

## Django: Medium or High Priority
![error_movies_not_imported_in_views](https://github.com/ex16x41/bugbounty/assets/44981946/bfb3d386-b45a-4855-842c-bc6ba9a63830)

## ASP.NET: Medium Priority
![Tuee5](https://github.com/ex16x41/bugbounty/assets/44981946/c80b6d8b-dd15-4c3a-8ffe-3d432ebc52cb)

## RUBY: Medium Priority
<img width="1342" alt="M4x4d" src="https://github.com/ex16x41/bugbounty/assets/44981946/25405166-843b-4983-aac7-d0941f40d258">

## Thymeleaf:
![output](https://github.com/ex16x41/bugbounty/assets/44981946/9156ae2c-d125-45a8-bbd3-bc04494c3a62)

## Apache Tomcat: Medium Priority
![BBOtu](https://github.com/ex16x41/bugbounty/assets/44981946/850de6ef-cc1d-4b7d-92b9-fad29d66a9e3)

## Yii:
![gxcoD](https://github.com/ex16x41/bugbounty/assets/44981946/7ab6ed5f-7096-48ce-bf53-5f381fad5b97)

## Spark:
TBD

## Sinatra:
![LMJIu](https://github.com/ex16x41/bugbounty/assets/44981946/6247d4e8-aca7-44f6-90e2-a9df45afd005)

## Flask:
![ijkqD](https://github.com/ex16x41/bugbounty/assets/44981946/c7baef3b-692b-4390-aaaf-fbd502f79771)
