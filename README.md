# Data analysis in base python


## Understanding File paths 
Understanding file paths is crucial for navigating and accessing files on a computer's file system. A file path specifies the location of a file or directory in a hierarchical structure. Here's a brief introduction to file paths:

1. **Absolute Path**: An absolute path specifies the exact location of a file or directory from the root directory of the file system. It includes the full directory hierarchy necessary to locate the file. For example:
   - On Unix-like systems (Linux, macOS): `/home/user/documents/file.txt`
   - On Windows: `C:\Users\User\Documents\file.txt`

2. **Relative Path**: A relative path specifies the location of a file or directory relative to the current working directory. It does not start from the root directory. For example:
   - `documents/file.txt`: Relative to the current working directory, assuming the file is located in the `documents` directory.
   - `../data/file.txt`: Relative to the parent directory of the current working directory, assuming the file is located in the `data` directory, which is one level above the current directory.

3. **File Path Components**:
   - **Directory**: Part of the path that specifies folders or directories. For example, `/home/user/documents/` or `C:\Users\User\Documents\`.
   - **File Name**: The name of the file, such as `file.txt`.
   - **Extension**: The part of the file name after the last dot, indicating the file type. For example, `.txt`, `.pdf`, `.jpg`.

4. **Special Symbols**:
   - **`.` (Dot)**: Represents the current directory.
   - **`..` (Double Dot)**: Represents the parent directory.
   - ~ **(Tilde)**: Represents the home directory (linux/unix)

5. **Platform Differences**:
   - Unix-like systems (Linux, macOS) use forward slashes (`/`) as directory separators.
   - Windows uses backslashes (`\`) as directory separators.
   - Python provides the `os.path` module, which offers functions to manipulate file paths in a platform-independent manner.

Understanding file paths allows you to locate, access, and manipulate files and directories programmatically, which is essential for file I/O operations like reading from and writing to files in Python.

## File IO

File I/O in Python refers to Input/Output operations involving files. It allows you to read from and write to files on your computer's storage. Here's a brief overview:

1. **Opening a File**: You start by opening a file using the `open()` function, specifying the file path and the mode ('r' for reading, 'w' for writing, 'a' for appending, etc.).

2. **Reading from a File**: Once the file is open for reading, you can use various methods like `read()`, `readline()`, or `readlines()` to read the content of the file.

3. **Writing to a File**: When a file is open for writing, you can use the `write()` method to write data to the file. If the file doesn't exist, Python will create it.

4. **Appending to a File**: If you want to add content to an existing file, you can open it in append mode ('a') and use the `write()` method to add content at the end of the file.

5. **Closing a File**: It's essential to close the file after you've finished working with it, using the `close()` method. Failing to close a file can lead to resource leaks.

6. **Context Manager (with Statement)**: Python provides a `with` statement that automatically handles opening and closing files. This ensures that the file is properly closed, even if an exception occurs.

## opening a file

``` python
# example
with open('./data/hello.txt', 'r') as f:
    data = f.read()
    print(data)
```

## File opening modes

* `r`: Open the file for reading. (default)
* ` w`: Open the file for writing. Create a new file if it does not exist or truncate the file if it exists.
* `x`: Create a  new file for writing only. Returns an error if the file already exists.
* `a`: Open the file for appending. Create a new file if it does not exist or append to the file if it exists.
* `t`: Open in text mode. (default)
* `b`: Open  in binary mode.
* `+`: Open a file for updating (reading and writing)
* `U`: Universal newline mode. This mode is intended for compatibility with different newline conventions on different operating systems. 

`The modes can be combined e.g`

`+r`


## Read Example


```python
# read() example
# reads all file content into a string 
with open('./data/hello.txt') as my_file:
    print(my_file.read())
```

    hello world
    
    hello neptune



```python
# readline()
# reads a single line from the file 
with open('./data/hello.txt') as file:
    print(file.readline())
```

    hello world
    



```python

# readlines()
# reads all lines from a file and returns them as a list
with open('./data/hello.txt') as file:
    print(file.readlines())
```

    ['hello world\n', '\n', 'hello neptune']


## Write Example

```python
# Example
with open('file. txt', 'w') as f:
    f.write('Hello, world!')
```


writes to a file if the file already exists its replaced if not a new file is created

## Write Example 


```python
# write to a file example

with open('writen_text.txt',"w") as file:
    
    for i in range(10):
        # \n is a special character to represent a new line
        file.write("hello word \n") 
```

## Append

```python
# example
with open('file.txt', 'a') as f:
    # Append some data to the file
    f.write('Hello, world!')
```

Appends new content to an existing files

## Append example


```python
# append to a file example 

with open('./writen_text.txt','+a') as file:
    file.write("this text was appended ")
```


```python
with  open('./writen_text.txt') as file:
    print(file.read())
```

    hello word 
    hello word 
    hello word 
    hello word 
    hello word 
    hello word 
    hello word 
    hello word 
    hello word 
    hello word 
    this text was appended 


## CSV

CSV (Comma Separated Values) data is a simple format for storing tabular data in plain text, where each line of the file represents a row, and the values within each row are separated by commas (or other delimiters like tabs, semicolons, etc.). It's a common file format used for data exchange between different software applications because of its simplicity and widespread support.

Here's an example of CSV data representing a simple table:

```
Name, Age, City
John, 25, New York
Alice, 30, Los Angeles
Bob, 22, Chicago
```

To read and manipulate CSV data in Python, you can use the built-in `csv` module.

Here's a step-by-step guide with examples:

## READING CSV DATA

```python
# example
with open("./data/test.csv") as f:
    reader = csv.reader(f)
    print(list(reader))

```


```python
# example
# includes the first row as part of the data even if its just column names
import csv

with open("./data/example.csv") as f:
    reader = csv.reader(f)
    print(list(reader))

```

    [['sam', '10'], ['john', '20'], ['angela', '30']]


## USING DICT READER

```python
# example
with open("./data/test.csv") as f:
    reader = csv.DictReader(f)
    print(list(reader))

```


```python
# example using csv.DictReader(f)
# assumes that the first row contains the keys i.e column names

with open("./data/example.csv") as f:
    reader = csv.DictReader(f)
    print(list(reader))
```

    [{'sam': 'john', '10': '20'}, {'sam': 'angela', '10': '30'}]


## JSON Data

JSON (JavaScript Object Notation) is another common format for storing and exchanging data. It's more structured than CSV and supports nested data structures.

Here's how you can read and manipulate JSON data in Python using the built-in `json` module:

JSON objects are useful for storing and exchanging data because they are:

* **Lightweight:** JSON objects are represented as text, which makes them easy to store and transmit.
* **Human-readable :** JSON objects are easy for humans to read and understand.
* **Machine-readable:** JSON objects can be easily parsed by computers.

The primitive JSON data types are:

* **String:** A sequence of characters  enclosed in double quotes, e.g. "Hello world".
* **Number:** A numeric value, e.g. 123.4 5.
* **Boolean:** A logical value, either true or false.
* **Null:** A value that represents the absence of a value.

**Examples**

```json
{
  "name": "John Doe",  // String
  "age": 30,          // Number 
  "isMarried": false,  // Boolean
  "job": null         // Null
}
``` 

## How to read JSON Data

```python
# example
import json

with open("./data/data.json") as f:
  data =  json.load(f)
  print(data)
```


```python
# example on reading json file 
import json

with open("./data/data.json") as f:
  data =  json.load(f)
  employees = data['employees']
  # looping over a json list
  for employee in employees:
    print(employee)
```

    {'id': 1, 'name': 'John', 'department': 'Engineering', 'skills': ['Python', 'Java', 'C++'], 'projects': [{'name': 'Project A', 'status': 'Completed'}, {'name': 'Project B', 'status': 'In Progress'}]}
    {'id': 2, 'name': 'Alice', 'department': 'Marketing', 'skills': ['Marketing Strategy', 'Social Media'], 'projects': [{'name': 'Campaign X', 'status': 'Completed'}, {'name': 'Campaign Y', 'status': 'In Progress'}]}



```python
import json

with open("./data/data.json") as f:
  data =  json.load(f)
  # directly accessing a nested object  
  employee_2 = data['employees'][1]["name"]
  print(employee_2)
```

    Alice


## JSON OBJECTS


A JSON object is a collection of  key-value pairs. It is used to represent data in a structured way. The keys are strings, and the values can be any type of data, including  strings, numbers, booleans, arrays, and even other objects.


**How to Create a JSON Object**

To create a JSON object, you can use the following syntax:

```json
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
```

The keys must be enclosed in double quotes, and the values can be any type of data.

**Example**

The following is an example of a JSON object that represents a person: 

```json
{
  "name": "John Doe",
  " age": 30,
  "occupation": "Software Engineer"
}
```

**How to Access Data from a JSON Object**

To access data from a JSON object, you can use the dot notation or the bracket notation.

**Dot Notation**

The dot notation is used to access data from a JSON object using the following syntax:

```python
object.key
```

**Bracket Notation**

The bracket notation is used to access data from a JSON object using the following syntax:

```python
object["key"]
```




```python
# example 

import json

with open("./data/data.json") as f:
  data =  json.load(f)
  print(data['employees'])
```

    [{'id': 1, 'name': 'John', 'department': 'Engineering', 'skills': ['Python', 'Java', 'C++'], 'projects': [{'name': 'Project A', 'status': 'Completed'}, {'name': 'Project B', 'status': 'In Progress'}]}, {'id': 2, 'name': 'Alice', 'department': 'Marketing', 'skills': ['Marketing Strategy', 'Social Media'], 'projects': [{'name': 'Campaign X', 'status': 'Completed'}, {'name': 'Campaign Y', 'status': 'In Progress'}]}]


## JSON List

A JSON list is an ordered collection  of values. It is used to represent data that can be iterated over, such as an array of strings, numbers, or objects.

**How to Create a JSON List**

To create a JSON list, you can use the following syntax:

```json
[
  "value1",
  "value2",
  "value3"
]
```

The values in a list can be any type of data, including strings, numbers, booleans, and even other objects.

**Example**

The following is an example of a JSON list that represents an array of strings:

```json
["red", "green", "blue"]
```

**How to Access Data from a  JSON List**

To access data from a JSON list, you can use the index of the item you want to access. The index of the first item in a list is 0.



```python
# example

import json

with open("./data/students.json") as f:
  data =  json.load(f)
  print(data[0])
  
```

    {'name': 'John Doe', 'grade': 'A', 'scores': {'math': 90, 'science': 85, 'english': 95}}


## Complex JSON Data

```json
{
  "name": "John Doe",
  "age": 30,
  "address": {
    "street": "123 Main Street",
    "city": " Anytown",
    "state": "CA",
    "zipcode": "12345"
  },
  "hobbies": ["coding", "reading", "travel"]
}

```

`Hint:` create a file and save the above json data or load use json.loads() to load data from a variable containing the above data

using the above examples try accessing `zipcode` and the last `hobby` from the data above 



```python
# example
# zipcode = 12345
```


```python
# example 2
# hobby = travel
```

## Bonus data from an API

Run this cell to get a joke from the chuck norris API 

documentation available here

https://api.chucknorris.io/



```python
import requests

response = requests.get('https://api.chucknorris.io/jokes/random')

data = response.json()

data['value']
```




    'Hitler killed him self because he found out Chuck Norris is jewish.'


