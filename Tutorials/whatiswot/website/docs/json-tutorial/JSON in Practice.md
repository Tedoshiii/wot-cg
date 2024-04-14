---
id: json2
---

# JSON in Practice

In the previous section, we showed mostly primitive types of JSON. In this section, we will first focus on arrays and objects, and then we will go over some common mistakes when writing JSON. At the end, we will demonstrate the usage of JSON generation and parsing.

### JSON Array

In JSON, each value in an array is called an item.
Arrays with items of different types are also allowed.

Accepted types:

- Number
- String
- Boolean
- Null

![json array](/img/4-JSON-In-Practice/json-array.png)

### Nested objects

Nested objects are allowed in JSON. The “measurement” keyword is an example of this.

Objects start and end with curly brackets. We are essentially defining keywords and mapping these keywords to values.
In this example, we define the name and value pairs to describe the data sent by sensors.

![nested object](/img/4-JSON-In-Practice/nested-object.png)

Here is a JSON array in which all of its items are JSON objects:

![json object array](/img/4-JSON-In-Practice/json-object-array.png)

## Common Mistakes

Now let's cover some common mistakes which can occur while writing JSON files.

### Space character

Let's start with the space character which is frequently overlooked.
Space counts as a character too.

> For example “isActive” is not the same as “isActive ”.

### Case sensitivity

JSON is also case sensitive. Paying attention to this is important to make sure that object assignments and comparisons work.

> "isActive" with an upper case "A" is not the same as “isactive” with a lower case "a".

### Quotation marks

Be careful not to forget any necessary quotation marks.

> "name: "Web of Things" is missing a quotation mark after name, which will lead to validation errors.

Conversely, putting them where you should not, can cause unwanted results.

> For example → “name”: ”true” is not the same as “name”: true without quotation marks. The first one is not a boolean but a string; so it will be interpreted as a string.

> The same problem would happen with numbers as well - "value": "90" would be interpreted as a string because of the unnecessary quotation marks.

We should always pay attention to the type we want to use and use quotation marks with intent. This way, the types will be correctly interpreted by your programming language.

### Comments

Putting comments inside JSON documents is not valid in contrast to most of the programming languages.

![comment](/img/4-JSON-In-Practice/comment.png)

### Trailing Commas

Commas should not be used at the final name-value pair - that is why the left example is not valid. This is more difficult to see if you are using it inside of a Javascript editor rather than a JSON editor.

![json js](/img/4-JSON-In-Practice/json-js.png)

### Programming Language Syntax

Similar to the previous issue depending on the programming language that you use syntax might differ.

- In JSON key-value pairs have to be with quotation marks whereas in JavaScript files it is not necessary to have quotation marks, both work.

![quotation marks syntax example](/img/tutorial/JSON-In-Practice/syntaxquotation.png)

- The syntax of the keywords might differ as well. For example, the true and false keywords in JSON, Rust, JavaScript, and Golang are written lowercase while in Python the first letter of these keywords needs to be capitalized.

![quotation marks syntax example](/img/tutorial/JSON-In-Practice/syntaxboolean.png)

- Similar to the previous one, the null keyword differs in JSON and Python. In JSON and JavaScript it is null with lowercase while in Python, the same meaning is given with the «None» keyword.

![quotation marks syntax example](/img/tutorial/JSON-In-Practice/syntaxnull.png)

## Practice exercise

Now let's put our new knowledge to practice! Open a code editor of your choice. Create a JSON file and save it by giving it a file name and adding a .json extension. Then the editor will recognize this file as a JSON document.

We will now read a JSON file from the file system using a JSON library in Python. First, we will open the JSON file that we have previously saved to the file system with open-as-file key words. Then, we can load that JSON file with the load function into the data object. We can also print it to see what is inside the JSON file:

```py
import json

with open('JSON_example.json') as file:
    data: json.load(file)

print(data)
```

Printing the data object in the console can look something like this:

```json
[{'name': 'Temperature sensor', ‘sensorID': '20014’,
'type': 'Temperature', 'unit': 'Celsius', 'value': 42}]
```

There are many ways to send a JSON file via different protocols, one of them is using Python and its request library for sending an HTTP request. With this library, you can use the post function to send an HTTP POST request with a JSON Payload. As a parameter, it takes the URL to send to and the JSON object.

```py
import requests

url = 'https://example.com/myResource'
jsonObj = {'someKey': 'someValue'}

x = requests.post(url, json = jsonObj)

print(x.text)
```
