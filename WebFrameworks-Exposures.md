# Discover web app frameworks and their exposures (low, medium, high, critical) for bug bounties.

## Table of Web Frameworks by priority

| Web Framework | Method | Source|
|-----:|---------------:|---------------|
|Laravel (PHP)|   "Whoops! There was an error."            | google.com         |
|  Symfony (PHP) Method 1  |  +plugin:SymfonyVerbosePlugin OR +plugin:SymfonyProfilerPlugin            | leakix.net        | 
| Symfony (PHP) Method 2    |     Set-Cookie: symfony=           | shodan.com         | 
| Symfony (PHP) Method 3    |     inurl:/frontend_dev.php/$         |   google.com         | 
| Symfony (PHP) Method 4    |     "SF_ROOT_DIR"         |   google.com         | 
| Django (credit fattselimi)   |    http.title:”DisallowedHost at /”      |   shodan.com         |
| Ruby on rails    |     Application Trace +  nil:NilClass (10%) TBD        |   google.com         | 
| Flask    |       Manual Testing    |   Burpsuite & Web Manual         | 
| ASP.NET  |     Manual Testing    |   Burpsuite & Web Manual    | 
| Yii |     intitle:"yii debugger"   |   google.com        | 
| Generic Method 1 (mass)|  site:.tld1.wildcard OR site:wildcard.tld "unexpected error" OR "Uncaught Exception" OR "fatal error" OR "Unknown column"  OR "exception occurred"   |  google.com       | 

## Triggering exceptions (Improper Error Handling - OWASP)

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

## What tech(app,src,framew) may a target be using? (if hidden from basic footprinting)

| indicator |what's likely in use|
|-----:|---------------:|
|got PHP files in specific path order? | CMS:WordPress, Joomla, and Drupal., WEBSRV:Apache, Nginx, and Microsoft IIS, WEBF:Laravel, Symfony, CodeIgniter, and Yii. DB:MySQL, PostgreSQL, and SQLite     |
|JSP files | Spring, Struts, and JavaServer Faces (JSF), Apache Tomcat, Jetty, GlassFish, JBoss, WebLogic, WebSphere, Resin.|
| nsf files | 

# Understanding Errors (Laravel, Symfony, Django)

## Laravel: Type of Errors
1.HttpException: This exception is thrown when an HTTP error occurs, such as a 404 Not Found or 500 Internal Server Error. It is the base class for all HTTP-related exceptions in Laravel.

2.ValidationException: This exception is thrown when a form validation fails in Laravel. It contains information about the validation errors and can be used to redirect the user back to the form with the validation errors displayed.

3.ModelNotFoundException: This exception is thrown when a model is not found in the database. It is commonly used to handle 404 errors when a requested resource is not found in the database.

4.QueryException: This exception is thrown when a database query fails, such as when there is a syntax error or a constraint violation. It contains information about the SQL error that caused the query to fail.

5.AuthenticationException: This exception is thrown when a user is not authenticated and tries to access a protected resource in Laravel. It can be used to redirect the user to the login page or to display a custom error message.

6.AuthorizationException: This exception is thrown when a user is not authorized to access a particular resource or perform a particular action. It can be used to redirect the user to a custom error page or to display a custom error message.

## Symfony: Type of Errors
1.InvalidArgumentException: This exception is thrown when an argument passed to a function or method is not valid.

2.NotFoundHttpException: This exception is thrown when a requested resource or URL is not found.

3.AccessDeniedException: This exception is thrown when a user does not have sufficient permissions to access a resource.

4.RuntimeException: This is a generic exception that is thrown when an unexpected error occurs during the execution of a script or application.

5.HttpException: This is a base exception class for HTTP-related errors, such as 404 (Not Found) or 500 (Internal Server Error).

6.Twig_Error_Runtime: This exception is thrown by the Twig template engine, which is used by Symfony to render templates. It is typically caused by a syntax error or a missing variable in a template.

7.Doctrine\DBAL\Exception: This exception is thrown by the Doctrine database abstraction layer, which is used by Symfony to interact with databases. It is typically caused by a database-related error, such as a missing table or a syntax error in a SQL query.


## Django: Type of Errors
1.TemplateSyntaxError: This error is thrown when there is a syntax error in a Django template. This error can occur when a developer forgets to close a tag or uses incorrect syntax in a template.

2.ImportError: This error is thrown when there is a problem importing a module or package in a Django application. This error can occur when a developer misspells the name of a module or package or when there is a problem with the environment configuration.

3.OperationalError: This error is thrown when there is an error executing a database query in a Django application. This error can occur when a database connection is lost or when there is a problem with the database configuration.

4.ImproperlyConfigured: This error is thrown when there is a problem with the configuration of a Django application. This error can occur when a developer forgets to set a required setting or when there is a problem with the environment configuration.

5.ValidationError: This error is thrown when there is a problem with data validation in a Django application. This error can occur when a form field is left blank or when a user enters invalid data.

6.SuspiciousOperation: This error is thrown when there is a suspicious or potentially malicious operation detected in a Django application. This error can occur when a user tries to access a restricted resource or perform an action that is not allowed.


# Keywords to check inside exceptions (because webf may be config'd with these below)
redis, API, PHP, DB, mysql, AD, path, server, database, username, password, key, secret, backend, admin, dir, port, URI, 


## Laravel: High or Critical Priority
![YDQcV](https://github.com/ex16x41/bugbounty/assets/44981946/075dfe16-0995-4be3-9833-2ab7aa8066a3)

### REAL LIFE EXAMPLE EXPOSURE LARAVEL POC- 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/b8f70723-8ab7-43e2-861d-8cf483180c7d)

## Symfony 1: High or Critical Priority
![error](https://github.com/ex16x41/bugbounty/assets/44981946/c7adac05-c24f-4fc7-951d-4e2ad433081c)

### REAL LIFE EXAMPLE EXPOSURE SYMFONY POC- 

![image](https://github.com/ex16x41/bugbounty/assets/44981946/d5007b3b-0803-4a8d-9af5-8d9e9e7368b7)


## Symfony 2: High or Critical Priority
![exceptions-in-dev-environment](https://github.com/ex16x41/bugbounty/assets/44981946/eea554ff-0c05-4e29-9bab-43db25f9180c)

## Django: Medium or High Priority
![error_movies_not_imported_in_views](https://github.com/ex16x41/bugbounty/assets/44981946/bfb3d386-b45a-4855-842c-bc6ba9a63830)

## ASP.NET: Medium Priority
![Tuee5](https://github.com/ex16x41/bugbounty/assets/44981946/c80b6d8b-dd15-4c3a-8ffe-3d432ebc52cb)

## RUBY: Medium Priority
<img width="1342" alt="M4x4d" src="https://github.com/ex16x41/bugbounty/assets/44981946/25405166-843b-4983-aac7-d0941f40d258">

## Apache Tomcat: Medium Priority
![BBOtu](https://github.com/ex16x41/bugbounty/assets/44981946/850de6ef-cc1d-4b7d-92b9-fad29d66a9e3)

## Yii: Example from test (shows in two pages one debug & one exception) - Medium or High Priority
![image](https://github.com/ex16x41/bugbounty/assets/44981946/3760db70-db81-469c-b2ad-93047fa15ee8)

## Yii: Exception - Medium Priority

![image](https://github.com/ex16x41/bugbounty/assets/44981946/bbfaf23e-4954-4e67-af45-762d5fd7a1b7)

## Thymeleaf:
![output](https://github.com/ex16x41/bugbounty/assets/44981946/9156ae2c-d125-45a8-bbd3-bc04494c3a62)

## Spark:
TBD

## Sinatra:
![LMJIu](https://github.com/ex16x41/bugbounty/assets/44981946/6247d4e8-aca7-44f6-90e2-a9df45afd005)

## Flask:
![ijkqD](https://github.com/ex16x41/bugbounty/assets/44981946/c7baef3b-692b-4390-aaaf-fbd502f79771)
