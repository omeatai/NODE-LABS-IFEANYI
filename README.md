# NODE-LABS-IFEANYI
by Ifeanyi Omeata

<details>
  <summary>Check Node Version</summary>

  ### Confirm Node Version
  
  ```
  node --version
  ```

</details>

<details>
  <summary>Introduction to Node</summary>

  ### node\myapp\app.js:

  ```js
  const amount = 100;
  
  if (amount < 100) {
    console.log("small number");
  } else {
    console.log("large number");
  }
  
  console.log("hey it's my first node app");
  ```

  ```
  node app.js
  ```

  ![image](https://github.com/user-attachments/assets/53dab7a3-7c26-42bf-b911-c4065cd9822a)

</details>

<details>
  <summary>Node Globals</summary>

  ### node\myapp\app.js:

  ```js
  // GLOBALS  - NO WINDOW !!!!
  
  // __dirname  - path to current directory
  // __filename - file name
  // require    - function to use modules (CommonJS)
  // module     - info about current module (file)
  // process    - info about env where the program is being executed
  
  console.log(__dirname);
  console.log(__filename);
  setInterval(() => {
    console.log("hello world");
  }, 1000);
  ```

  ```
  node app.js
  ```

  ![image](https://github.com/user-attachments/assets/1010ee5c-0425-4909-8379-df1cdd9e25f7)

</details>

<details>
  <summary>Node Exports and Require Module </summary>

  ### node\myapp\app.js:

  ```js
  // CommonJS, every file is module (by default)
  // Modules - Encapsulated Code (only share minimum)
  
  const sayHi = require("./data/func");
  const students = require("./data/data");
  const { names, singlePerson } = require("./data/data");
  
  sayHi("Susan");
  sayHi(students.john);
  sayHi(students.peter);
  sayHi(singlePerson.name);
  sayHi(names[0]);
  ```

  ### node\myapp\data\data.js:

  ```js
  // local
  const secret = "SUPER SECRET";
  // share
  const john = "John";
  const peter = "Peter";
  
  const person = {
    name: "Bob",
  };
  
  module.exports = { john, peter };
  module.exports.singlePerson = person;
  module.exports.names = ["James", "John", "Jane"];
  ```

  ### node\myapp\data\func.js:

  ```js
  const sayHi = (name) => {
    console.log(`Hello there, ${name}`);
  };
  
  // export default
  module.exports = sayHi;
  ```

  ![image](https://github.com/user-attachments/assets/57237c99-f617-4ac1-a805-f40400a72a06)

</details>

<details>
  <summary>Node OS Module </summary>

  ### node\myapp\app.js:

  ```js
  const os = require("os");
  
  // info about current user
  const user = os.userInfo();
  console.log("User Info: ", user);
  
  // method returns the system uptime in seconds
  console.log("System Uptime: ", `The System Uptime is ${os.uptime()} seconds`);
  
  const currentOS = {
    name: os.type(),
    release: os.release(),
    totalMem: os.totalmem(),
    freeMem: os.freemem(),
  };
  
  console.log("Current OS: ", currentOS);
  ```

  ```
  node app.js
  ```

  ![image](https://github.com/user-attachments/assets/20c0a217-d187-40db-9e9d-da879a135094)

</details>

<details>
  <summary>Node PATH Module </summary>

  ### node\myapp\app.js:

  ```js
  const path = require("path");
  console.log(path.sep);
  
  const filePath = path.join("/data/", "subfolder", "test.txt");
  console.log(filePath);
  
  const base = path.basename(filePath);
  console.log(base);
  
  const absolute = path.resolve(__dirname, "data", "subfolder", "test.txt");
  console.log(absolute);
  ```

  ```
  node app.js
  ```

  ![image](https://github.com/user-attachments/assets/8b849de5-b122-4014-b9c5-55b2b275b293)

</details>

<details>
  <summary>Node FS Sync Module </summary>

  ### node\myapp\app.js:

  ```js
  const { readFileSync, writeFileSync } = require("fs");
  console.log("start");
  
  const first = readFileSync("./data/content/first.txt", "utf8");
  const second = readFileSync("./data/content/second.txt", "utf8");
  console.log(first, second);
  
  writeFileSync(
    "./data/content/result-sync.txt",
    `Here is the result : ${first}, ${second}`,
    { flag: "a" }
  );
  
  console.log("done with this task");
  console.log("starting the next one");
  ```

  ```
  node app.js
  ```

  ![image](https://github.com/user-attachments/assets/4023b159-1766-4e28-bab3-5a2092c06556)

  ![image](https://github.com/user-attachments/assets/7c5aa4d6-719f-498d-b55e-3f698a5c5f27)

</details>

<details>
  <summary>Node FS Async Module </summary>

  ### node\myapp\app.js:

  ```js
  const { readFile, writeFile } = require("fs");
  
  console.log("start");
  
  readFile("./data/content/first.txt", "utf8", (err, result) => {
    if (err) {
      console.log(err);
      return;
    }
    const first = result;
  
    readFile("./data/content/second.txt", "utf8", (err, result) => {
      if (err) {
        console.log(err);
        return;
      }
      const second = result;
  
      writeFile(
        "./data/content/result-async.txt",
        `Here is the result : ${first}, ${second}`,
        (err, result) => {
          if (err) {
            console.log(err);
            return;
          }
          console.log("done with this task");
        }
      );
    });
  });
  
  console.log("starting next task");
  ```

  # OR

  ```js
  const { readFile, writeFile } = require("fs/promises");
  
  const start = async () => {
    try {
      console.log("start");
      const first = await readFile("./data/content/first.txt", "utf8");
      const second = await readFile("./data/content/second.txt", "utf8");
      await writeFile(
        "./data/content/result-async.txt",
        `Here is the result : ${first}, ${second}`
      );
      console.log("done with this task");
    } catch (err) {
      console.log(err);
    }
    console.log("starting next task");
  };
  
  start();
  ```

  ![image](https://github.com/user-attachments/assets/24925146-f113-4bb3-9b6e-f13d9867290f)

  ![image](https://github.com/user-attachments/assets/5be77fca-b9d1-47a8-adfc-58225a3c0849)

</details>

<details>
  <summary>Node HTTP Module - Simple Request </summary>

  ### node\myapp\app.js:

  ```js
  const http = require("http");
  
  const server = http.createServer((req, res) => {
    console.log("Request Method: ", req.method);
    console.log("Request URL: ", req.url);
    console.log("Request Path: ", req.path);
    console.log("Request Query: ", req.query);
    console.log("Request Params: ", req.params);
    console.log("Request Headers: ", req.headers);
    console.log("Request Body: ", req.body);
    console.log("Request Status Code: ", req.statusCode);
    console.log("Request Status Message: ", req.statusMessage);
  
    res.write("Welcome to our home page");
    res.end();
  });
  
  server.listen(5000);
  ```

  ```
  node app.js
  ```

  ![image](https://github.com/user-attachments/assets/e8648d38-0a03-4c1c-a231-c9cc5a0657ce)
  
  ![image](https://github.com/user-attachments/assets/46a8267b-4e8a-41c5-acbb-80c8385c75ee)

</details>

<details>
  <summary>Node HTTP Module - Conditional Requests </summary>

  ### node\myapp\app.js:

  ```js
  const http = require("http");
  
  const server = http.createServer((req, res) => {
    if (req.url === "/") {
      res.end("Welcome to our home page");
      return;
    }
    if (req.url === "/about") {
      res.end("Here is our short history");
      return;
    }
    res.end(`
      <h1>Oops!</h1>
    <p>We can't seem to find the page you are looking for</p>
    <a href="/">back home</a>
      `);
  
    // OR
    // ###################################
    // ###################################
    // if (req.url === "/") {
    //   res.end("Welcome to our home page");
    // } else if (req.url === "/about") {
    //   res.end("Here is our short history");
    // } else {
    //   res.end(`
    //   <h1>Oops!</h1>
    //   <p>We can't seem to find the page you are looking for</p>
    //   <a href="/">back home</a>
    //   `);
    // }
  });
  
  server.listen(5000, () => {
    console.log("Server is listening on port 5000...");
  });
  ```

  ```
  node app.js
  ```

  ![image](https://github.com/user-attachments/assets/f031aac8-1260-4cad-9b2e-d1dd6a34d3e9)
  
  ![image](https://github.com/user-attachments/assets/ae374dd2-c090-4d70-b736-520b3853c74e)

  ![image](https://github.com/user-attachments/assets/c2573757-b812-43cb-9d5d-e2d5e759585d)

  ![image](https://github.com/user-attachments/assets/afc2b2ea-7ba0-499e-b0e9-dbc45584f028)

</details>

<details>
  <summary>Node NPM Install - Lodash </summary>

  ```js
  // npm - global command, comes with node
  // npm --version

  // local dependency - use it only in this particular project
  // npm i <packagename>

  // global dependency - use it in any project
  // npm install -g <packageName>
  // sudo npm install -g <packageName> (mac)

  // package.json - manifest file (stores important info abvout project/package)
  // manual approach (create package.json in the root, create properties etc)
  // npm init (step by step, press enter to skip)
  // npm init -y (everything default)
  ```

  ```
  npm init -y
  npm i lodash
  ```

  ### node\myapp\package.json:

  ```json
  {
    "name": "myapp",
    "version": "1.0.0",
    "description": "myapp",
    "main": "app.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "author": "",
    "license": "ISC",
    "dependencies": {
      "lodash": "^4.17.21"
    }
  }
  ```

  ### node\myapp\app.js:

  ```js
  const http = require("http");
  const _ = require("lodash");
  
  const items = [1, [2, [3, [4]]]];
  const newItems = _.flattenDeep(items);
  console.log(newItems);
  
  const server = http.createServer((req, res) => {
    if (req.url === "/") {
      res.end("Welcome to our home page");
      return;
    }
    if (req.url === "/about") {
      res.end("Here is our short history");
      return;
    }
    res.end(`
      <h1>Oops!</h1>
    <p>We can't seem to find the page you are looking for</p>
    <a href="/">back home</a>
      `);
  });
  
  server.listen(5000, () => {
    console.log("Server is listening on port 5000...");
  });
  ```

  ![image](https://github.com/user-attachments/assets/8b9cbbef-0fbf-44cd-b53a-8ad4e30a1954)

</details>

<details>
  <summary>Node Github - Repository Command Line with .gitignore</summary>

  ### .gitignore:

  ```
  /node_modules
  ```

  ### create a new repository on the command line:

  ```
  echo "# node-tutorial" >>> README.md
  git init
  git add README.md / git add .
  git commit -m "first commit"
  git branch -M main
  git remote add origin git@github.com: ifeanyi-omeata/node-tut.git
  git push -u origin main
  ```

  ### push an existing repository from the command line:

  ```
  git remote add origin git@github.com: ifeanyi-omeata/node-tut.git
  git branch -M main
  git push -u origin main
  ```

</details>

<details>
  <summary>Node Install as devDependency or Dependency </summary>

  ### Install Nodemon as Dependency:

  ```
  npm i nodemon
  ```

  ### Install Nodemon as devDependency:

  ```
  npm i nodemon -D
  npm i nodemon --save-dev
  ```

  ### node\myapp\package.json:

  ```json
  {
    "name": "myapp",
    "version": "1.0.0",
    "description": "myapp",
    "main": "app.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "author": "",
    "license": "ISC",
    "dependencies": {
      "lodash": "^4.17.21"
    },
    "devDependencies": {
      "nodemon": "^3.1.10"
    }
  }
  ```

</details>

<details>
  <summary>Node NPM Uninstall Dependency </summary>

  ```
  npm uninstall bootstrap
  ```

  OR

  - [ ] Delete node_modules Folder
  - [ ] Delete package-lock.json File
  - [ ] Remove Bootstrap dependency ("bootstrap": "^4.6.0") from package.json
  - [ ] Run "npm install"

</details>


<details>
  <summary>Node Package.json scripts run </summary>
  
  ### node\myapp\package.json:

  ```json
  {
    "name": "myapp",
    "version": "1.0.0",
    "description": "myapp",
    "main": "app.js",
    "scripts": {
      "start": "node app.js",
      "dev": "nodemon app.js",
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "author": "",
    "license": "ISC",
    "dependencies": {
      "lodash": "^4.17.21"
    },
    "devDependencies": {
      "nodemon": "^3.1.10"
    }
  }
  ```

  ### Run Script Command:

  ```
  npm run dev
  ```

  ### node\myapp\app.js:

  ```js
  const http = require("http");
  const _ = require("lodash");
  
  const items = [1, [2, [3, [4]]]];
  const newItems = _.flattenDeep(items);
  console.log(newItems);
  
  const server = http.createServer((req, res) => {
    if (req.url === "/") {
      res.end("WELCOME TO OUR HOME PAGE!!!");
      return;
    }
    if (req.url === "/about") {
      res.end("Here is our short history");
      return;
    }
    res.end(`
      <h1>Oops!</h1>
    <p>We can't seem to find the page you are looking for</p>
    <a href="/">back home</a>
      `);
  });
  
  server.listen(5000, () => {
    console.log("Server is listening on port 5000...");
  });
  ```

  ![image](https://github.com/user-attachments/assets/6a6984e8-88d0-4c25-a2ca-dc0bfd879ff6)

  ![image](https://github.com/user-attachments/assets/1d555468-951b-4e53-8756-dd8953c2f19c)

</details>

<details>
  <summary>Node Async Patterns with Promises </summary>

  ### 1-node\myapp\app.js:

  ```js
  const { readFile } = require("fs");

  readFile("./data/content/first.txt", "utf8", (err, data) => {
    if (err) {
      console.log(err);
      return;
    } else {
      console.log(data);
      return;
    }
  });
  ```

  ![image](https://github.com/user-attachments/assets/7d6a76c8-0c7c-462f-a61f-7bececa15cea)

  ### 2-node\myapp\app.js:

  ```js
  const { readFile } = require("fs");

  const getText = (path) => {
    return new Promise((resolve, reject) => {
      readFile(path, "utf8", (err, data) => {
        if (err) {
          reject(err);
          return;
        } else {
          resolve(data);
          return;
        }
      });
    });
  };
  
  getText("./data/content/first.txt")
    .then((result) => console.log(result))
    .catch((err) => console.log(err));
  ```

  ![image](https://github.com/user-attachments/assets/f75a5ac1-69aa-447a-a26a-6cf2a8be1cae)

  ### 3-node\myapp\app.js:

  ```js
  const { readFile } = require("fs");
  
  const getText = (path) => {
    return new Promise((resolve, reject) => {
      readFile(path, "utf8", (err, data) => {
        if (err) {
          reject(err);
          return;
        } else {
          resolve(data);
          return;
        }
      });
    });
  };
  
  const start = async () => {
    try {
      const first = await getText("./data/content/first.txt");
      const second = await getText("./data/content/second.txt");
      console.log(first, second);
    } catch (error) {
      console.log(error);
    }
  };
  
  start();
  ```

  ![image](https://github.com/user-attachments/assets/4a0c84bc-4de9-466a-bb88-7231bbbdbb5f)

  ### 4-node\myapp\app.js:

  ```js
  // const { readFile, writeFile } = require("fs");
  // const util = require('util')
  // const readFilePromise = util.promisify(readFile)
  // const writeFilePromise = util.promisify(writeFile)
  
  const { readFile, writeFile } = require("fs/promises");
  
  const start = async () => {
    try {
      const first = await readFile("./data/content/first.txt", "utf8");
      const second = await readFile("./data/content/second.txt", "utf8");
      await writeFile(
        "./data/content/result-mind-grenade.txt",
        `THIS IS AWESOME : ${first} ${second}`,
        { flag: "a" }
      );
      console.log(first, second);
    } catch (error) {
      console.log(error);
    }
  };
  
  start();
  ```

  ![image](https://github.com/user-attachments/assets/cafd8b76-0651-4f2e-8156-17a5760406a4)

  ![image](https://github.com/user-attachments/assets/d3b9cf33-d2f8-4bae-af3e-c879cc214367)

</details>

<details>
  <summary>Node Events Emitter </summary>

  ### node\myapp\app.js:

  ```js
  const EventEmitter = require("events");
  
  const customEmitter = new EventEmitter();
  
  customEmitter.on("response", () => {
    console.log("data collection started");
  });
  
  customEmitter.on("response", (name, id) => {
    console.log(
      `data recieved user ${name || "unknown"} with id:${id || "unknown"}`
    );
  });
  
  customEmitter.on("response", () => {
    console.log("data collection ended");
  });
  
  customEmitter.emit("response");
  customEmitter.emit("response", "john", 34);
  customEmitter.emit("response", "peter", 34);
  ```

  ![image](https://github.com/user-attachments/assets/bbcf5adf-c5fa-4f8d-bb86-426b9747b2a6)

  ### node\myapp\app.js:

  ```js
  const http = require('http')
  
  // const server = http.createServer((req, res) => {
  //   res.end('Welcome')
  // })
  
  // Using Event Emitter API
  const server = http.createServer()
  // emits request event
  // subcribe to it / listen for it / respond to it
  server.on('request', (req, res) => {
    res.end('Welcome')
  })
  
  server.listen(5000)
  ```

</details>

<details>
  <summary>Node Streams - Create Big File </summary>

  ### node\myapp\app.js:

  ```js
  const { writeFileSync } = require("fs");
  for (let i = 0; i < 100000; i++) {
    writeFileSync("./data/content/big.txt", `hello world ${i}\n`, { flag: "a" });
  }
  ```

  ![image](https://github.com/user-attachments/assets/5b89625d-3e96-438b-8388-6c509835af02)

</details>

<details>
  <summary>Node Streams - Create Read Stream </summary>

  ### node\myapp\app.js:

  ```js
  const { createReadStream } = require("fs");
  
  // default 64kb
  // last buffer - remainder
  // highWaterMark - control size
  // const stream = createReadStream('./content/big.txt', { highWaterMark: 90000 })
  // const stream = createReadStream('../content/big.txt', { encoding: 'utf8' })
  const stream = createReadStream("./data/content/big.txt", {
    highWaterMark: 90000,
    encoding: "utf8",
  });
  
  stream.on("data", (result) => {
    console.log(result);
  });
  stream.on("error", (err) => console.log(err));
  ```

  ![image](https://github.com/user-attachments/assets/a100602a-4ec7-461e-a257-0db55202878c)

</details>

<details>
  <summary>Node Streams - HTTP Stream Example </summary>

  ### node\myapp\app.js:

  ```js
  var http = require("http");
  var fs = require("fs");
  
  http
    .createServer(function (req, res) {
      // const text = fs.readFileSync('./content/big.txt', 'utf8')
      // res.end(text)
      const fileStream = fs.createReadStream("./data/content/big.txt", "utf8");
      fileStream.on("open", () => {
        fileStream.pipe(res);
      });
      fileStream.on("error", (err) => {
        res.end(err);
      });
    })
    .listen(5000);
  ```

  ![image](https://github.com/user-attachments/assets/e7f875b5-570a-4a36-8ea6-a6800da36319)

  ![image](https://github.com/user-attachments/assets/26a6d9a9-4604-4c22-9b2a-2c0ea8955d01)

</details>

<details>
  <summary>Node - HTTP Basic Home Page </summary>

  ### node\myapp\app.js:

  ```js
  const http = require("http");
  
  const server = http.createServer((req, res) => {
    console.log("User accessed the home page");
    res.end("<h1>Home Page</h1>");
  });
  
  server.listen(5000, () => {
    console.log("Server is running on port 5000");
  });
  ```

  ![image](https://github.com/user-attachments/assets/a1311098-7bce-43ed-b27b-03e39faa7725)

  ![image](https://github.com/user-attachments/assets/7d504b67-5d9f-4f50-b30e-a66d61dcb328)

</details>

<details>
  <summary>Node - HTTP Basic Headers </summary>

  ### node\myapp\app.js:

  ```js
  const http = require("http");
  
  const server = http.createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/html" });
    res.write("<h1>Home Page</h1>");
    res.end();
  });
  
  server.listen(5000, () => {
    console.log("Server is running on port 5000");
  });
  ```

  ![image](https://github.com/user-attachments/assets/fb9bdfcc-4a61-4f70-9eea-dae06f49a9f5)

  ![image](https://github.com/user-attachments/assets/6178f99c-8c76-46e9-96e8-1f89000f2647)

</details>

<details>
  <summary>Node - HTTP Request Object to navigate Pages </summary>

  ### node\myapp\app.js:

  ```js
  const http = require("http");
  
  const server = http.createServer((req, res) => {
    const url = req.url;
    const method = req.method;
    console.log(url, method);
  
    if (url === "/") {
      // home page
      res.writeHead(200, { "Content-Type": "text/html" });
      res.write("<h1>Home Page</h1>");
      res.end();
    } else if (url === "/about") {
      // about page
      res.writeHead(200, { "Content-Type": "text/html" });
      res.write("<h1>About Page</h1>");
      res.end();
    } else {
      // 404 page
      res.writeHead(404, { "Content-Type": "text/html" });
      res.write("<h1>404 | Page not found</h1>");
      res.end();
    }
  });
  
  server.listen(5000, () => {
    console.log("Server is running on port 5000");
  });
  ```

  ![image](https://github.com/user-attachments/assets/8889105e-be8c-437f-be14-da8acbe9a9da)
  ![image](https://github.com/user-attachments/assets/e01edb42-2b16-4758-8dcd-3f1eaef7b1db)
  ![image](https://github.com/user-attachments/assets/e54f4533-b338-4cbe-abf6-0f5f2f42c166)
  ![image](https://github.com/user-attachments/assets/0d21dfa3-8727-42cf-9892-6a1729abfa7d)

</details>

<details>
  <summary>Node - HTTP Route HTML File Pages </summary>

  ### node\myexpressapp\app.js

  ```js
  const http = require("http");
  const { readFileSync } = require("fs");
  
  // get all files
  const homePage = readFileSync("./pages/index.html");
  const aboutPage = readFileSync("./pages/about.html");
  // const styles = readFileSync("./navbar-app/styles.css");
  // const logo = readFileSync("./navbar-app/logo.svg");
  // const browserIcon = readFileSync("./navbar-app/browser-app-512x512.png");
  
  const server = http.createServer((req, res) => {
    const url = req.url;
    const method = req.method;
    console.log(url, method);
  
    if (url === "/") {
      // home page
      res.writeHead(200, { "Content-Type": "text/html" });
      res.write(homePage);
      res.end();
    } else if (url === "/about") {
      // about page
      res.writeHead(200, { "Content-Type": "text/html" });
      res.write(aboutPage);
      res.end();
    } else {
      // 404 page
      res.writeHead(404, { "Content-Type": "text/html" });
      res.write("<h1>404 | Page not found</h1>");
      res.end();
    }
  });
  
  server.listen(5000, () => {
    console.log("Server is running on port 5000");
  });
  ```

  ### node\myexpressapp\pages\index.html
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Home Page</title>
    </head>
    <body>
      <h1>Home Page</h1>
      <a href="/about">Go to About</a>
    </body>
  </html>
  ```

  ### node\myexpressapp\pages\about.html
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>About Page</title>
    </head>
    <body>
      <h1>About Page</h1>
      <a href="/">Go to Home</a>
    </body>
  </html>
  ```

  ![image](https://github.com/user-attachments/assets/7a31de36-0d0a-4963-91c7-3ee3958b7a91)
  ![image](https://github.com/user-attachments/assets/38b04870-509a-4bca-9445-2ba284903606)
  ![image](https://github.com/user-attachments/assets/1d6b4da9-f727-4181-a19d-191a40a516f5)

</details>

<details>
  <summary>Node Express - Install Express </summary>

  ```
  npm install express
  npm install express@4.17.1
  npm install express@4.17.1 --save
  ```

  ### node\myexpressapp\package.json

  ```json
  {
    "name": "myexpressapp",
    "version": "1.0.0",
    "main": "app.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "start": "nodemon app.js"
    },
    "author": "",
    "license": "ISC",
    "description": "",
    "devDependencies": {
      "nodemon": "^3.1.10"
    },
    "dependencies": {
      "express": "^5.1.0"
    }
  }
  ```

</details>

<details>
  <summary>Node Express - Basic Example </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  app.get("/", (req, res) => {
    console.log("user hit the Home Page");
    res.status(200).send("Home Page");
  });
  
  app.get("/about", (req, res) => {
    console.log("user hit the About Page");
    res.status(200).send("About Page");
  });
  
  app.all("/*path", (req, res) => {
    res.status(404).send("<h1>404 | Resource not found</h1>");
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });
  
  // app.get
  // app.post
  // app.put
  // app.delete
  // app.all
  // app.use
  // app.listen
  ```

  ![image](https://github.com/user-attachments/assets/ae4a2228-d51b-4267-8dd3-5e4b9004558a)

</details>

<details>
  <summary>Node Express - Display HTML Files </summary>

  ### node\myexpressapp\app.js

  ```js
  const path = require("path");
  const express = require("express");
  const app = express();
  const port = 5000;
  
  app.get("/", (req, res) => {
    console.log("user hit the Home Page");
    res.status(200).sendFile(path.resolve(__dirname, "./pages/index.html"));
    // res.status(200).sendFile(path.join(__dirname, "./pages/index.html"));
  });
  
  app.get("/about", (req, res) => {
    console.log("user hit the About Page");
    res.status(200).sendFile(path.resolve(__dirname, "./pages/about.html"));
  });
  
  app.all("/*path", (req, res) => {
    res.status(404).send("<h1>404 | Resource not found</h1>");
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });
  ```

  ### node\myexpressapp\pages\index.html
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Home Page</title>
    </head>
    <body>
      <h1>Home Page</h1>
      <a href="/about">Go to About</a>
    </body>
  </html>
  ```

  ### node\myexpressapp\pages\about.html
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>About Page</title>
    </head>
    <body>
      <h1>About Page</h1>
      <a href="/">Go to Home</a>
    </body>
  </html>
  ```

  ![image](https://github.com/user-attachments/assets/8a825200-1c07-45b0-8eb5-a9cdd83212da)
  ![image](https://github.com/user-attachments/assets/cdd7e015-58d7-467a-aa1d-b4b46185007e)
  ![image](https://github.com/user-attachments/assets/fdedfdec-8a1a-4d4e-a057-2aaee0fa41ca)

</details>

<details>
  <summary>Node Express - Display Static Files </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const path = require("path");
  const port = 5000;
  
  //Serve static files middleware
  app.use(express.static("./public"));
  
  app.get("/", (req, res) => {
    console.log("user hit the Home Page");
    res.status(200).sendFile(path.resolve(__dirname, "./pages/index.html"));
    // res.status(200).sendFile(path.join(__dirname, "./pages/index.html"));
  });
  
  app.get("/about", (req, res) => {
    console.log("user hit the About Page");
    res.status(200).sendFile(path.resolve(__dirname, "./pages/about.html"));
  });
  
  app.all("/*path", (req, res) => {
    res.status(404).send("<h1>404 | Resource not found</h1>");
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });
  ```

  ### node\myexpressapp\public\styles.css
  
  ```css
  .btn {
      background-color: red;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
  }
  
  .btn:hover {
      background-color: black;
  }
  
  .btn-link {
      text-decoration: none;
      color: white;
  }
  
  .btn-link:hover {
      color: white;
  }
  ```

  ### node\myexpressapp\public\app.js
  
  ```js
  const portfolio = document.querySelector("#portfolio");
  const portfolioName = portfolio.textContent;
  
  portfolio.addEventListener("click", () => {
    alert(`${portfolioName} button clicked`);
  });
  ```

  ### node\myexpressapp\pages\index.html
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Home Page</title>
      <link rel="stylesheet" href="./styles.css" />
    </head>
    <body>
      <nav>
        <img src="./logo.svg" alt="logo" />
      </nav>
      <h1>Home Page</h1>
      <button class="btn" id="portfolio">View our Portfolio</button>
      <a href="/about" class="btn btn-link">Go to About</a>
      <script src="./app.js"></script>
    </body>
  </html>
  ```

  ### node\myexpressapp\pages\about.html
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>About Page</title>
      <link rel="stylesheet" href="./styles.css" />
    </head>
    <body>
      <nav>
        <img src="./logo.svg" alt="logo" />
      </nav>
      <h1>About Page</h1>
      <a href="/" class="btn btn-link">Go to Home</a>
    </body>
  </html>
  ```

![image](https://github.com/user-attachments/assets/a42903d8-b525-47b7-9266-11e3b0d59005)
![image](https://github.com/user-attachments/assets/18f2e127-735b-4367-8b8b-0bc1afcef667)
![image](https://github.com/user-attachments/assets/b7f61adc-bf0b-4fd7-90b9-dcb9181e4082)
![image](https://github.com/user-attachments/assets/ab0264ae-c001-454e-889d-7cadecd0e179)

</details>

<details>
  <summary>Node Express - Send JSON Data </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const path = require("path");
  const port = 5000;
  
  const { products, people } = require("./data/data");
  
  //Serve static files middleware
  app.use(express.static("./public"));
  
  app.get("/", (req, res) => {
    res.status(200).json(products);
  });
  
  app.get("/api/v1/people", (req, res) => {
    res.status(200).json(people);
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });
  ```

  ### node\myexpressapp\data\data.js
  
  ```js
  const products = [
    {
      id: 1,
      name: "albany sofa",
      image:
        "https://dl.airtable.com/.attachments/6ac7f7b55d505057317534722e5a9f03/9183491e/product-3.jpg",
      price: 39.95,
      desc: `I'm baby direct trade farm-to-table hell of, YOLO readymade raw denim venmo whatever organic gluten-free kitsch schlitz irony af flexitarian.`,
    },
    {
      id: 2,
      name: "entertainment center",
      image:
        "https://dl.airtable.com/.attachments/da5e17fd71f50578d525dd5f596e407e/d5e88ac8/product-2.jpg",
      price: 29.98,
      desc: `I'm baby direct trade farm-to-table hell of, YOLO readymade raw denim venmo whatever organic gluten-free kitsch schlitz irony af flexitarian.`,
    },
    {
      id: 3,
      name: "albany sectional",
      image:
        "https://dl.airtable.com/.attachments/05ecddf7ac8d581ecc3f7922415e7907/a4242abc/product-1.jpeg",
      price: 10.99,
      desc: `I'm baby direct trade farm-to-table hell of, YOLO readymade raw denim venmo whatever organic gluten-free kitsch schlitz irony af flexitarian.`,
    },
    {
      id: 4,
      name: "leather sofa",
      image:
        "https://dl.airtable.com/.attachments/3245c726ee77d73702ba8c3310639727/f000842b/product-5.jpg",
      price: 9.99,
      desc: `I'm baby direct trade farm-to-table hell of, YOLO readymade raw denim venmo whatever organic gluten-free kitsch schlitz irony af flexitarian.`,
    },
  ];
  const people = [
    { id: 1, name: "john" },
    { id: 2, name: "peter" },
    { id: 3, name: "susan" },
    { id: 4, name: "anna" },
    { id: 5, name: "emma" },
  ];
  module.exports = { products, people };
  ```

  ![image](https://github.com/user-attachments/assets/8124ee76-9ec8-4e9a-939b-0f7658a0acda)
  ![image](https://github.com/user-attachments/assets/fd501397-ce9d-45ee-b787-3302a6cf8f9d)
  ![image](https://github.com/user-attachments/assets/a5ffedea-a15d-4c93-8950-9ee645e4dd47)

</details>











<details>
  <summary>Node Express -  </summary>

  ### node\myexpressapp\app.js

  ```js

  ```

  ### node\myexpressapp\pages\index.html
  
  ```html

  ```

  ```
  node app.js
  ```



</details>










