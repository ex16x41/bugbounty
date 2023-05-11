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
| Flask    |        TBD     |   google.com         | 
| Ruby on rails    |     Application Trace +  nil:NilClass (10%) TBD        |   google.com         | 
| Ruby on rails    |     Application Trace +  nil:NilClass (10%) TBD        |   google.com         | 

# Triggering exceptions (Improper Error Handling - OWASP)

| Web applications frequently generate error conditions during normal operation. Out of memory, null pointer exceptions, system call failure, database unavailable, network timeout, and hundreds of other common conditions can cause errors to be generated. These errors must be handled according to a well thought out scheme that will provide a meaningful error message to the user, diagnostic information to the site maintainers, and no useful information to an attacker. |
|-----:|
|Laravel (PHP)|  
|  Symfony (PHP) Method 1  |  


## FLASK:
1."TypeError": indicates a type-related error, such as trying to perform an operation on an object of the wrong type.

2."NameError": indicates that a variable or function name was not defined.

3."KeyError": indicates that a key used to access a dictionary does not exist.

4."ValueError": indicates that an argument passed to a function or method is invalid.

5."AttributeError": indicates that an attribute or method does not exist for an object.

6."SyntaxError": indicates that there is a problem with the syntax of the code.

7."IndentationError": indicates that there is a problem with the indentation of the code.

8."ImportError": indicates that there is a problem importing a module or package 
