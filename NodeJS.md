# 1. Purpose of `res.redirect()` in Express.js? Does `res.redirect()` Send an HTML File or Redirect Directly?



The `res.redirect()` method in Express.js is used to **instruct the client (such as a browser) to navigate to a different URL**. It does this by sending an HTTP redirect response (usually with status code 302 by default), along with a `Location` header pointing to the new URL.

---

### **Does `res.redirect()` Send an HTML File or Redirect Directly?**

- **It does not send an HTML file.**
- Instead, it sends an HTTP response with a redirect status code (such as 302 or 301) and a `Location` header.
- The browser (or HTTP client) receives this response and then automatically makes a new request to the specified URL.
- The actual content (such as an HTML file or JSON data) is served by the handler at the new URL, not by the `res.redirect()` itself.

---

### **Example**

```
app.get('/old-route', (req, res) => {
  res.redirect('/new-route');
});

app.get('/new-route', (req, res) => {
  res.send('You have been redirected!');
});
```
- Visiting `/old-route` will cause the browser to receive a redirect response and then automatically navigate to `/new-route`, where the actual content is sent.

---

### **Summary Table**

| Method                | What It Does                                                        |
|-----------------------|---------------------------------------------------------------------|
| `res.redirect(url)`   | Sends an HTTP redirect response (302 by default) to the client      |
|                       | Client then requests the new URL                                    |
|                       | Does **not** send an HTML file directly                            |

---

**In summary:**  
`res.redirect()` in Express.js sends an HTTP redirect response, causing the client to navigate to a new URL. It does **not** send an HTML file itself; the new content is served by the route handler at the destination URL.


# 2. What does `res.status(404).send()` do?

The `res.status(404).send()` method in Express.js is used to send an HTTP response with a **404 status code** ("Not Found") and a response body to the client.

### **How it Works**

- **`res.status(404)`** sets the HTTP status code of the response to 404, which means "Not Found".
- **`.send()`** sends the response body to the client. You can pass a string, object, or other data as the response body (e.g., `res.status(404).send('Not Found')`).

### **Example Usage**

```js
app.get('/some-route', (req, res) => {
  res.status(404).send('Not Found');
});
```
- This will respond to the client with a 404 status and the message "Not Found" in the response body.

### **Summary Table**

| Method                   | What it does                                    |
|--------------------------|-------------------------------------------------|
| `res.status(404)`        | Sets HTTP status code to 404 ("Not Found")      |
| `.send('Not Found')`     | Sends "Not Found" as the response body          |
| `res.status(404).send()` | Combines both: sets status and sends response   |

---

**In summary:**  
`res.status(404).send()` sets the response status to 404 (Not Found) and sends a response body to the client, indicating that the requested resource could not be found.

# 3. Which Core Module Provides Utility Functions in Node.js?

The **`util`** core module in Node.js provides a collection of utility functions that are useful for application and module developers. These functions assist with tasks such as formatting strings, debugging, type checking, inheritance, and converting callback-based functions to promises.

---

### **Key Points about the `util` Module**

- The `util` module contains functions like `util.format()`, `util.inspect()`, `util.promisify()`, `util.callbackify()`, and more.
- It is a core module, so you can use it directly without installing any external packages:

```js
const util = require('util');
```

- Other core modules like `os` and `path` also provide utility methods, but **`util`** is the dedicated general-purpose utility module in Node.js.

---

### **Summary Table**

| Core Module | Provides Utility Functions? | Description                                 |
|-------------|-----------------------------|---------------------------------------------|
| `util`      | Yes                         | General-purpose utility functions           |
| `os`        | Yes                         | OS-related utility functions                |
| `path`      | Yes                         | File and directory path utilities           |

---

**In summary:**  
The primary core module that provides utility functions in Node.js is the **`util`** module.



# 4. What Does the `readline` Module Allow You to Do in Node.js?

The **`readline` module** in Node.js allows you to:

- **Read input from a readable stream (like `process.stdin` or a file) one line at a time**.
- **Create interactive command-line interfaces** that can prompt the user for input and handle their responses.
- **Process input from users or files line by line**, making it useful for CLI tools, file processing, and chatbots.

---

### **Key Features and Methods**

- **`readline.createInterface()`**: Creates an interface for reading data line by line from a stream.
- **`rl.question(query, callback)`**: Prompts the user with a question and handles their response.
- **`rl.on('line', callback)`**: Listens for each line of input from the user or file.
- **`rl.close()`**: Closes the interface, ending the input session.
- **Other methods**: `setPrompt()`, `prompt()`, `pause()`, `resume()`, `clearLine()`, `clearScreenDown()`, etc..

---

### **Example Usage**

**Reading user input from the command line:**
```js
const readline = require('readline');
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('What is your name? ', (answer) => {
  console.log(`Hello, ${answer}!`);
  rl.close();
});
```

**Reading a file line by line:**
```js
const fs = require('fs');
const readline = require('readline');
const rl = readline.createInterface({
  input: fs.createReadStream('example.txt')
});

rl.on('line', (line) => {
  console.log(`Line from file: ${line}`);
});
```


---

### **Summary Table**

| Capability                              | Description                                             |
|------------------------------------------|---------------------------------------------------------|
| Read from command line                   | Get user input interactively                            |
| Read files line by line                  | Efficiently process large files without loading all data|
| Build CLI tools                          | Create prompts, handle responses, and process commands  |
| Control cursor and output                | Move cursor, clear lines, and customize terminal output |

---

**In summary:**  
The `readline` module lets you read input from streams (like the command line or files) one line at a time, enabling interactive CLI applications and efficient file processing in Node.js.



# 5. Which command updates All npm Packages to Latest Version Without Any External Library

To update all npm packages in your project to the latest versions **within the version ranges specified in your `package.json`** (i.e., up to the latest minor/patch version allowed by your semver constraints), use:

```js
npm update
```

- This command checks for newer versions of your dependencies and updates them, but **only within the version ranges defined in your `package.json`** (e.g., from `^1.0.0` to `^1.2.0` but not to `2.0.0`) .
- It does **not** require any external libraries or tools.

---

### **Limitations**

- `npm update` will **not** update to the absolute latest major versions if your `package.json` restricts it with semver ranges (like `^` or `~`) .
- To update to the latest versions regardless of your current semver constraints, you would need to manually edit `package.json` or use a third-party tool like `npm-check-updates` (`ncu`), but that requires an external library .

---

### **Summary Table**

| Command         | Updates To                    | Requires External Library? |
|-----------------|------------------------------|---------------------------|
| `npm update`    | Latest allowed by semver      | No                        |
| `ncu -u` + `npm install` | Absolute latest versions         | Yes                       |

---

**In summary:**  
Run `npm update` to update all npm packages to the latest versions allowed by your `package.json` semver constraints, without using any external library.



# 6. How to Read Command Line Arguments in Node.js

In Node.js, command line arguments passed to a script are accessible via the built-in global array:

```js
process.argv
```

### Key Details about `process.argv`

- It is an **array** containing all command line arguments.
- The **first element** (`process.argv[0]`) is the path to the Node.js executable.
- The **second element** (`process.argv[1]`) is the path to the JavaScript file being executed.
- The **subsequent elements** (`process.argv[2]` and onwards) are the actual command line arguments passed by the user.

---

### Example: Logging Command Line Arguments

```js
// script.js
console.log(process.argv);
```

Run the script with arguments:

```
node script.js arg1 arg2
```

Output:

```js
[
  '/path/to/node',
  '/path/to/script.js',
  'arg1',
  'arg2'
]
```

---

### Example: Accessing User Arguments Only

To get only the user-passed arguments, slice off the first two elements:

```js
const args = process.argv.slice(2);
console.log(args);
```

---

### Example: Using Arguments in a Script

```js 
// add.js
const args = process.argv.slice(2);
const a = parseInt(args);
const b = parseInt(args[1]);
console.log(`Sum: ${a + b}`);
```

Run:

```
node add.js 5 10
```

Output:

```
Sum: 15
```

---

### Summary Table

| Concept                | Description                                      |
|------------------------|-------------------------------------------------|
| `process.argv`         | Array of command line arguments                  |
| `process.argv[0]`      | Node.js executable path                           |
| `process.argv[1]`      | Path of the executing script                      |
| `process.argv.slice(2)`| User-passed arguments                             |

---

**In summary:**  
Use `process.argv` array to read command line arguments in Node.js, slicing from index 2 to get only the user inputs.



# 7. What Does `stream.pipe()` Do in Node.js?

The `stream.pipe()` method is used to **connect a readable stream to a writable stream**. As data is read from the readable stream, it is automatically passed (or "piped") into the writable stream. This enables efficient, incremental data transfer between streams without loading all data into memory at once.

---

### **Key Behaviors**

- **Automatic Data Flow:** Data is read from the source (readable stream) and written to the destination (writable stream) as it becomes available, managing buffering and backpressure automatically.
- **Efficient for Large Data:** Useful for processing large files or data sources, since only small chunks are kept in memory at any time.
- **Chaining:** You can chain multiple streams together, such as reading a file, transforming it (e.g., compressing), and then writing the result to another file.

---

### **Example**

```js
const fs = require('fs');
const readable = fs.createReadStream('input.txt');
const writable = fs.createWriteStream('output.txt');

// Pipe data from input.txt to output.txt
readable.pipe(writable);
```
- This reads data from `input.txt` and writes it to `output.txt` as it is read, without loading the entire file into memory.

---

### **Chaining Example (Compression)**

```js
const fs = require('fs');
const zlib = require('zlib');

const readable = fs.createReadStream('input.txt');
const gzip = zlib.createGzip();
const writable = fs.createWriteStream('input.txt.gz');

// Chain: read -> compress -> write
readable.pipe(gzip).pipe(writable);
```
- This reads `input.txt`, compresses it with gzip, and writes the compressed data to `input.txt.gz`.

---

### **Summary Table**

| Method              | What It Does                                      |
|---------------------|---------------------------------------------------|
| `readable.pipe(writable)` | Forwards data from a readable to a writable stream |
| Chaining            | Allows connecting multiple streams for processing |
| Automatic Handling  | Manages buffering, backpressure, and flow         |

---

**In summary:**  
`stream.pipe()` connects a readable stream to a writable stream, automatically transferring data between them efficiently and incrementally, making it ideal for handling large files or streaming data in Node.js.
