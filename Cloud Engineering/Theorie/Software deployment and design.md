# SDLC Software Development Life Cycle

### Phases of SDLC
1. Requirements and analysis
2. design
3. Implementation
4. testing
5. Deployment
6. Maintenance
This is a kind of waterfall method
Newer methods like agile have other steps

# Coding basics

#### What is clean code

- Follow common principles related to formatting , organization
- emphases on standardization
- Inline comments, self commenting code

#### Why clean code
- Easier to understand  | more compact | better organized
- Is modular, tests via unit testing frameworks
- standardized -> easier to scan and check using automated tools
- looks nicer

### Methods and functions
- are blocks of code that performs tasks
- it simplifies the code

#### Methods:
- Blocks of code for object oriented programming
- You define a class object and you can then add methods to it.
	for example:
	```
	calc = calculater().  # calc becomes an object of the class calculator()
	calc.add(5, 3).     # .add is a method
	```

#### Functions:
- Standalone code blocks
##### When create a function or method
- code that performs a concrete task
- It is used more than once

##### Arguments and parameters in functions
- they add flexibility to the function or method (you can supply values that the function can handle)
```
def functionname(parameter1, parameter2):
	print('hallo ' + parameter1 + parameter2)
	# other code .......

# calling the function
functionname("michael", "1986")
```
##### return statement

- the return statement ends the execution of a function

```
def functionsum(var1, var2)
	result = var1 + var2
	return result

myresult = functionsum(5, 5)
```

#### Modules
Purpose:
- divide large portions of code in to smaller parts
- It is packaged as a single file.  for example: module1.py
- It should work as independently


# Code review and testing
### Testing
##### Functional testing
- Does the software work correctly.
- Unit testing
- Integration testing
Non-functional testing
- performance
- security
- resilience
- compliance
- localization
##### TDD = Test drive development
First write the tests based on the requirements THEN develop the software and check if it passes the tests.


# Data formats

###### REST APIs (Representational State Transfer Application Programming Interface)
- Makes use of the HTTP + principles that define how resources should be accessed and manipulated
- it is stateless , so every time you need to supply all the information

###### REST methods are
- GET - POST - PUT - DELETE - ....



Most popular formats for exchanging information between APIs
- YAML
- JSON
- XML


#### Flow of a REST API transaction
1. authenticate
2. execute a GET request
3. Modify the received XML, JSON or YAML
4. Execute a post with the modified XML,JSON,YAML 
5. request a GET again to check if the modification was succesfull


## XML
Extensible markup language
- it is the parent of HTML ( in html the tags are fixed)

#### Header of the XML
only the first 2 lines

#### TAGS
all tags in xml are user-defined. It is your application so you can choose the tags

XML prologue =. the first line in the XML file

#### Attributes
You can add additional information within the tags

#### XML namespace ( defines the standard and version of that xml )

### JSON
JavaScript Object Notation
- Data types: Boolean, string, numbers, nulls

### YAML
Yaml Ain't Markup Language
- Better readable
- Is a superset of JSON  -> a YAML file can embed json code

Always start with    ---

Indentations is important

#### Long strings

## Parsing <-> Serializing

Parsing = from a long string of chars -> retrieve components and values
Serializing = turn a internal data structure into a character string