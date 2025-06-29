# NODE-LABS-IFEANYI
by Ifeanyi Omeata

## NODE

### [Node Course 1](https://www.codingaddict.io/l/products)

<details>
  <summary>Check Node Version</summary>

  ### Confirm Node Versions
  
  ```sh
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

  ```sh
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

  ```sh
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

  ```sh
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

  ```sh
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

  ```sh
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

  ```sh
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

  ```sh
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

  ```sh
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

  ```sh
  npm i nodemon
  ```

  ### Install Nodemon as devDependency:

  ```sh
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

  ```sh
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

  ```sh
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
  <summary>Node Express - Using Params to filter Data </summary>

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
    res.status(200).send(
      `<h1>Home Page</h1>
      <link rel="stylesheet" href="/styles.css">
      <a class='btn btn-link' href='/api/v1/products'>products</a>
      <a class='btn btn-link' href='/api/v1/people'>people</a>`
    );
  });
  
  app.get("/api/v1/products", (req, res) => {
    const newProducts = products.map((product) => {
      const { id, name, image } = product;
      return { id, name, image };
    });
    return res.status(200).json(newProducts);
  });
  
  app.get("/api/v1/products/:productID", (req, res) => {
    const { productID } = req.params;
    const singleProduct = products.find(
      (product) => product.id === Number(productID)
    );
    if (!singleProduct) {
      return res.status(404).send("404 | Product not found");
    }
    return res.status(200).json(singleProduct);
  });
  
  app.get("/api/v1/products/:productID/reviews/:reviewID", (req, res) => {
    const { productID, reviewID } = req.params;
    console.log(productID, reviewID);
    res.send(`ProductID: ${productID} | ReviewID: ${reviewID}`);
  });
  
  app.get("/api/v1/people", (req, res) => {
    res.status(200).json(people);
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

  ![image](https://github.com/user-attachments/assets/d0fd8248-a9db-4802-97c3-9af4ec40728b)
  ![image](https://github.com/user-attachments/assets/f5564ab9-ffaf-46b8-ae93-37ea291e20fe)
  ![image](https://github.com/user-attachments/assets/75c250f4-4912-4d38-bf29-03d1539b07b8)
  ![image](https://github.com/user-attachments/assets/8564ea22-4b83-48c7-9d1b-cba5ee10d7fe)
  ![image](https://github.com/user-attachments/assets/2b8f111b-ecdf-4d29-9bab-6dddf6780743)
  ![image](https://github.com/user-attachments/assets/332dd07a-ac7a-42b5-94b6-c65bc832ddd5)
  ![image](https://github.com/user-attachments/assets/6a1ddbf7-64d1-4607-ae58-9549d6036cc0)

</details>

<details>
  <summary>Node Express - Using Query Strings to search Data </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const path = require("path");
  const port = 5000;
  
  const { products, people } = require("./data/data");
  
  //Serve static files middleware
  app.use(express.static("./public"));
  
  // Home Page
  app.get("/", (req, res) => {
    res.status(200).send(
      `<h1>Home Page</h1>
      <link rel="stylesheet" href="/styles.css">
      <a class='btn btn-link' href='/api/v1/products'>products</a>
      <a class='btn btn-link' href='/api/v1/people'>people</a>`
    );
  });
  
  // Products Page
  app.get("/api/v1/products", (req, res) => {
    const newProducts = products.map((product) => {
      const { id, name, image } = product;
      return { id, name, image };
    });
    return res.status(200).json(newProducts);
  });
  
  // Products Query Page
  app.get("/api/v1/products/query", (req, res) => {
    const { search, limit } = req.query;
    console.log({ search, limit });
    // return res.status(200).json({ search, limit });
    let sortedProducts = [...products];
    if (search) {
      sortedProducts = sortedProducts.filter((product) => {
        return product.name.startsWith(search);
      });
    }
    if (limit) {
      sortedProducts = sortedProducts.slice(0, Number(limit));
    }
    if (sortedProducts.length < 1) {
      // return res.status(200).send("No products found");
      return res.status(200).json({ success: true, data: [] });
    }
    return res.status(200).json(sortedProducts);
  });
  
  // Single Product Page
  app.get("/api/v1/products/:productID", (req, res) => {
    const { productID } = req.params;
    const singleProduct = products.find(
      (product) => product.id === Number(productID)
    );
    if (!singleProduct) {
      return res.status(404).send("404 | Product not found");
    }
    return res.status(200).json(singleProduct);
  });
  
  // Single Product Reviews Page
  app.get("/api/v1/products/:productID/reviews/:reviewID", (req, res) => {
    const { productID, reviewID } = req.params;
    console.log(productID, reviewID);
    res.send(`ProductID: ${productID} | ReviewID: ${reviewID}`);
  });
  
  // People Page
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

  ![image](https://github.com/user-attachments/assets/5d00b5bd-d6b6-4dc7-b7fc-48e159ce75c4)
  ![image](https://github.com/user-attachments/assets/d00a9964-872d-49a9-aaeb-ca57ca2fde26)
  ![image](https://github.com/user-attachments/assets/5537a8c4-d47d-4961-86e7-b208090a4d5f)

</details>

<details>
  <summary>Node Express - Middleware Basics </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  //Serve static files middleware
  app.use(express.static("./public"));
  
  const logger = (req, res, next) => {
    const method = req.method;
    const url = req.url;
    const time = new Date().getFullYear();
    const data = { method, url, time };
    console.log(data);
    req.data = data;
    next();
  };
  
  // Home Page
  app.get("/", logger, (req, res) => {
    const { method, url, time } = req.data;
    res.status(200).send(`<h1>Home Page</h1>
    <h2>Method: ${method}</h2>
    <h2>URL: ${url}</h2>
    <h2>Time: ${time}</h2>`);
  });
  
  //About Page
  app.get("/about", logger, (req, res) => {
    res.status(200).send(`<h1>About Page</h1>`);
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ![image](https://github.com/user-attachments/assets/3df4c95d-fa16-4c66-83de-7f6a5a87d01c)
  ![image](https://github.com/user-attachments/assets/6394eade-c108-41f0-b499-480713a273d3)

</details>

<details>
  <summary>Node Express - app.use Middleware with logger </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  const logger = require("./middleware/logger");
  
  //Serve static files middleware
  app.use(express.static("./public"));
  
  // Middleware
  app.use("/", logger);
  
  // Routes
  // Home Page
  app.get("/", (req, res) => {
    const { method, url, time } = req.data;
    res.status(200).send(`<h1>Home Page</h1>
    <h2>Method: ${method}</h2>
    <h2>URL: ${url}</h2>
    <h2>Time: ${time}</h2>`);
  });
  
  //About Page
  app.get("/about", (req, res) => {
    res.status(200).send(`<h1>About Page</h1>`);
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\middleware\logger.js
  
  ```js
  const logger = (req, res, next) => {
    const method = req.method;
    const url = req.url;
    const time = new Date().getFullYear();
    const data = { method, url, time };
    console.log(data);
    req.data = data;
    next();
  };
  
  module.exports = logger;

  ```

  ![image](https://github.com/user-attachments/assets/a5cb065b-fdb0-41b6-93b2-c235656d3e14)
  ![image](https://github.com/user-attachments/assets/7a79a3f5-ddcf-4dd9-9a99-b49c0acc16f2)


</details>

<details>
  <summary>Node Express -  app.use Multiple Middleware Functions with logger and auth </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  const logger = require("./middleware/logger");
  const auth = require("./middleware/auth");
  
  //Serve static files middleware
  app.use(express.static("./public"));
  
  // Middleware
  app.use("/", [logger, auth]);
  
  // Routes
  // Home Page
  app.get("/", (req, res) => {
    const { method, url, time } = req.data;
    res.status(200).send(`<h1>Home Page</h1>
    <h2>Method: ${method}</h2>
    <h2>URL: ${url}</h2>
    <h2>Time: ${time}</h2>
    <h2>User: ${req.user}</h2>`);
  });
  
  //About Page
  app.get("/about", (req, res) => {
    res.status(200).send(`<h1>About Page</h1>`);
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\middleware\logger.js

  ```js
  const logger = (req, res, next) => {
    const method = req.method;
    const url = req.url;
    const time = new Date().getFullYear();
    const data = { method, url, time };
    console.log(data);
    req.data = data;
    next();
  };
  
  module.exports = logger;

  ```

  ### node\myexpressapp\middleware\auth.js

  ```js
  const auth = (req, res, next) => {
    const { user } = req.query;
    if (user === "john") {
      req.user = "john";
      next();
    } else {
      res.status(401).send("<h1>401 | Unauthorized</h1>");
    }
  };
  
  module.exports = auth;

  ```

  ![image](https://github.com/user-attachments/assets/4f4d4e0b-af8b-452f-881d-19e190012b3f)
  ![image](https://github.com/user-attachments/assets/a015055b-3f05-4354-837e-1c9dba27a856)
  ![image](https://github.com/user-attachments/assets/fc784a65-191c-4579-b6d2-e538f8ca3708)
  ![image](https://github.com/user-attachments/assets/867dc109-a173-4325-bb98-c828da07f753)
  ![image](https://github.com/user-attachments/assets/f9087fb9-9d6b-43fc-9bea-ca5af9dfc833)

</details>

<details>
  <summary>Node Express - app.use Morgan Loggng Middleware </summary>

  ### Install Morgan Middleware
  
  ```
  npm i morgan
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
      "express": "^5.1.0",
      "morgan": "^1.10.0"
    }
  }

  ```

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  const morgan = require("morgan");
  const logger = require("./middleware/logger");
  const auth = require("./middleware/auth");
  
  //Serve static files middleware
  app.use(express.static("./public"));
  
  // Middleware
  app.use("/", morgan("tiny")); //morgan is a middleware that logs the request to the console: morgan("dev")
  
  // Routes
  // Home Page
  app.get("/", [logger, auth], (req, res) => {
    const { method, url, time } = req.data;
    res.status(200).send(`<h1>Home Page</h1>
    <h2>Method: ${method}</h2>
    <h2>URL: ${url}</h2>
    <h2>Time: ${time}</h2>
    <h2>User: ${req.user}</h2>`);
  });
  
  //About Page
  app.get("/about", (req, res) => {
    res.status(200).send(`<h1>About Page</h1>`);
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ![image](https://github.com/user-attachments/assets/dbff3ea4-dc4a-4def-bc6d-897d8c9068c8)
  ![image](https://github.com/user-attachments/assets/248a1a96-957f-4a38-b866-23a230d8c402)

</details>

<details>
  <summary>Node Express - GET Request </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  const { people } = require("./data/data");
  
  app.get("/api/v1/people", (req, res) => {
    res.status(200).json({ success: true, data: people });
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\data\data.js
  
  ```js
  const people = [
    { id: 1, name: "john" },
    { id: 2, name: "peter" },
    { id: 3, name: "susan" },
    { id: 4, name: "anna" },
    { id: 5, name: "emma" },
  ];
  module.exports = { products, people };

  ```

  ![image](https://github.com/user-attachments/assets/21cda0e2-c961-4dc7-8878-55cd516804c2)
  ![image](https://github.com/user-attachments/assets/cdab8ee5-6bca-4c2a-934f-df7588bec52e)

</details>

<details>
  <summary>Node Express - POST Request </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  const { people } = require("./data/data");
  
  // static assets
  app.use(express.static("./public"));
  
  // parse form data
  app.use(express.urlencoded({ extended: false }));
  
  app.post("/login", (req, res) => {
    console.log(req.body);
    const { name } = req.body;
    if (name) {
      return res
        .status(200)
        .send(
          `<h1>Welcome ${name.slice(0, 1).toUpperCase() + name.slice(1)}!</h1>`
        );
    }
    res.status(401).send("Please Provide Credentials");
  });
  
  app.get("/api/v1/people", (req, res) => {
    res.status(200).json({ success: true, data: people });
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\public\index.html
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <link rel="stylesheet" href="./styles.css" />
      <link rel="stylesheet" href="./normalize.css" />
      <title>Traditional</title>
    </head>
    <body>
      <nav>
        <div class="nav-center">
          <h5>HTTP Methods</h5>
          <div>
            <a href="index.html">regular </a>
            <a href="javascript.html">javascript </a>
          </div>
        </div>
      </nav>
      <main>
        <form action="/login" method="POST">
          <h3>Traditional Form</h3>
          <div class="form-row">
            <label for="name"> enter name </label>
            <input type="text" name="name" id="name" autocomplete="false" />
          </div>
          <button type="submit" class="block">submit</button>
        </form>
      </main>
    </body>
  </html>

  ```

  ![image](https://github.com/user-attachments/assets/f0a3be7b-d35e-454e-984a-89205eb20d8b)
  ![image](https://github.com/user-attachments/assets/69b387c6-e300-4596-a8ed-a5ad2518d25b)
  ![image](https://github.com/user-attachments/assets/253ca508-8d06-472d-a5db-c33a0b30c620)
  ![image](https://github.com/user-attachments/assets/65bd691c-623a-4986-81cb-f18be496a02f)
  ![image](https://github.com/user-attachments/assets/e8c579cd-041d-457e-8efe-5532245b3c47)

</details>

<details>
  <summary>Node Express - GET Request with Postman </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  const { people } = require("./data/data");
  
  // static assets
  app.use(express.static("./public"));
  
  // parse form data
  app.use(express.urlencoded({ extended: false }));
  
  // parse json
  app.use(express.json());
  
  // get all people
  app.get("/api/v1/people", (req, res) => {
    res.status(200).json({ success: true, data: people });
  });
  
  // post request
  app.post("/api/v1/people", (req, res) => {
    const { name } = req.body;
    if (!name) {
      return res
        .status(400)
        .json({ success: false, msg: "Please Provide Credentials" });
    }
    res
      .status(201)
      .json({
        success: true,
        data: [...people, { id: people.length + 1, name: name }],
      });
  });
  
  app.post("/login", (req, res) => {
    console.log(req.body);
    const { name } = req.body;
    if (!name) {
      return res.status(401).send("Please Provide Credentials");
    }
    return res
      .status(200)
      .send(
        `<h1>Welcome ${name.slice(0, 1).toUpperCase() + name.slice(1)}!</h1>`
      );
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\data\data.js
  
  ```js
  const people = [
    { id: 1, name: "john" },
    { id: 2, name: "peter" },
    { id: 3, name: "susan" },
    { id: 4, name: "anna" },
    { id: 5, name: "emma" },
  ];

  module.exports = { people };
  ```

  ![image](https://github.com/user-attachments/assets/c477c59d-1c36-46d7-a8a1-e76af370e93d)
  ![image](https://github.com/user-attachments/assets/7f4739c8-7703-4a51-9ac0-ae3f7fd423f9)

</details>

<details>
  <summary>Node Express - POST Request with Postman </summary>

 ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  const { people } = require("./data/data");
  
  // static assets
  app.use(express.static("./public"));
  
  // parse form data
  app.use(express.urlencoded({ extended: false }));
  
  // parse json
  app.use(express.json());
  
  // get all people
  app.get("/api/v1/people", (req, res) => {
    res.status(200).json({ success: true, data: people });
  });
  
  // post request
  app.post("/api/v1/people", (req, res) => {
    const { name } = req.body;
    if (!name) {
      return res
        .status(400)
        .json({ success: false, msg: "Please Provide Credentials" });
    }
    res
      .status(201)
      .json({
        success: true,
        data: [...people, { id: people.length + 1, name: name }],
      });
  });
  
  app.post("/login", (req, res) => {
    console.log(req.body);
    const { name } = req.body;
    if (!name) {
      return res.status(401).send("Please Provide Credentials");
    }
    return res
      .status(200)
      .send(
        `<h1>Welcome ${name.slice(0, 1).toUpperCase() + name.slice(1)}!</h1>`
      );
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\data\data.js
  
  ```js
  const people = [
    { id: 1, name: "john" },
    { id: 2, name: "peter" },
    { id: 3, name: "susan" },
    { id: 4, name: "anna" },
    { id: 5, name: "emma" },
  ];

  module.exports = { people };
  ```

  ![image](https://github.com/user-attachments/assets/b24cc1f9-695d-4669-b33a-c089407de088)
  ![image](https://github.com/user-attachments/assets/14d8b3e9-53e6-4ebe-93b8-6aa4e0dbbb58)
  ![image](https://github.com/user-attachments/assets/d017988f-e935-4013-966d-76b2a8ff2b92)

</details>

<details>
  <summary>Node Express - PUT Request with Postman </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  const { people } = require("./data/data");
  
  // static assets
  app.use(express.static("./public"));
  
  // parse form data
  app.use(express.urlencoded({ extended: false }));
  
  // parse json
  app.use(express.json());
  
  // get all people
  app.get("/api/v1/people", (req, res) => {
    res.status(200).json({ success: true, data: people });
  });
  
  // post request
  app.post("/api/v1/people", (req, res) => {
    const { name } = req.body;
    if (!name) {
      return res
        .status(400)
        .json({ success: false, msg: "Please Provide Credentials" });
    }
    res.status(201).json({
      success: true,
      data: [...people, { id: people.length + 1, name: name }],
    });
  });
  
  app.put("/api/v1/people/:id", (req, res) => {
    const { id } = req.params;
    const { name } = req.body;
    if (!name) {
      return res.status(400).json({ success: false, msg: "Please Provide Name" });
    }
    const person = people.find((person) => person.id === Number(id));
    if (!person) {
      return res
        .status(404)
        .json({ success: false, msg: `Person Not Found with id ${id}` });
    }
    const newPeople = people.map((person) => {
      if (person.id === Number(id)) {
        person.name = name;
      }
      return person;
    });
    res.status(200).json({ success: true, data: newPeople });
  });
  
  app.post("/login", (req, res) => {
    console.log(req.body);
    const { name } = req.body;
    if (!name) {
      return res.status(401).send("Please Provide Credentials");
    }
    return res
      .status(200)
      .send(
        `<h1>Welcome ${name.slice(0, 1).toUpperCase() + name.slice(1)}!</h1>`
      );
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\data\data.js
  
  ```js
  const people = [
    { id: 1, name: "john" },
    { id: 2, name: "peter" },
    { id: 3, name: "susan" },
    { id: 4, name: "anna" },
    { id: 5, name: "emma" },
  ];

  module.exports = { people };

  ```

  ![image](https://github.com/user-attachments/assets/a5228ade-7933-464b-9a8c-70b685bda333)
  ![image](https://github.com/user-attachments/assets/191478ae-ad18-4c88-8164-100c0c1e9955)
  ![image](https://github.com/user-attachments/assets/7b370513-2e2a-4afc-acbf-de3c6d9ccc8f)
  ![image](https://github.com/user-attachments/assets/63a376e5-8f95-4748-bb7c-4f29abad293b)

</details>

<details>
  <summary>Node Express - DELETE Request with Postman </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  const { people } = require("./data/data");
  
  // static assets
  app.use(express.static("./public"));
  
  // parse form data
  app.use(express.urlencoded({ extended: false }));
  
  // parse json
  app.use(express.json());
  
  // get all people
  app.get("/api/v1/people", (req, res) => {
    res.status(200).json({ success: true, data: people });
  });
  
  // post request
  app.post("/api/v1/people", (req, res) => {
    const { name } = req.body;
    if (!name) {
      return res
        .status(400)
        .json({ success: false, msg: "Please Provide Credentials" });
    }
    res.status(201).json({
      success: true,
      data: [...people, { id: people.length + 1, name: name }],
    });
  });
  
  app.delete("/api/v1/people/:id", (req, res) => {
    const { id } = req.params;
    const person = people.find((person) => person.id === Number(id));
    if (!person) {
      return res
        .status(404)
        .json({ success: false, msg: `Person Not Found with id: ${id}` });
    }
    const newPeople = people.filter((person) => person.id !== Number(id));
    res.status(200).json({ success: true, data: newPeople });
  });
  
  app.put("/api/v1/people/:id", (req, res) => {
    const { id } = req.params;
    const { name } = req.body;
    if (!name) {
      return res.status(400).json({ success: false, msg: "Please Provide Name" });
    }
    const person = people.find((person) => person.id === Number(id));
    if (!person) {
      return res
        .status(404)
        .json({ success: false, msg: `Person Not Found with id ${id}` });
    }
    const newPeople = people.map((person) => {
      if (person.id === Number(id)) {
        person.name = name;
      }
      return person;
    });
    res.status(200).json({ success: true, data: newPeople });
  });
  
  app.post("/login", (req, res) => {
    console.log(req.body);
    const { name } = req.body;
    if (!name) {
      return res.status(401).send("Please Provide Credentials");
    }
    return res
      .status(200)
      .send(
        `<h1>Welcome ${name.slice(0, 1).toUpperCase() + name.slice(1)}!</h1>`
      );
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\data\data.js
  
  ```js
  const people = [
    { id: 1, name: "john" },
    { id: 2, name: "peter" },
    { id: 3, name: "susan" },
    { id: 4, name: "anna" },
    { id: 5, name: "emma" },
  ];

  module.exports = { people };

  ```

  ![image](https://github.com/user-attachments/assets/39f39a7b-c368-4311-b7c1-0fdaa9fd3ca1)
  ![image](https://github.com/user-attachments/assets/79de82ea-e8d4-49ff-8d73-7b26e294cb0a)
  ![image](https://github.com/user-attachments/assets/540ccb3c-7ea4-49e5-963d-af68dea7edff)

</details>

<details>
  <summary>Node Express - Routes with Express Router </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  const people = require("./routes/people");
  const auth = require("./routes/auth");
  
  // static assets
  app.use(express.static("./public"));
  
  // parse form data
  app.use(express.urlencoded({ extended: false }));
  
  // parse json
  app.use(express.json());
  
  // people route
  app.use("/api/v1/people", people);
  
  // auth route
  app.use("/login", auth);
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\routes\people.js
  
  ```js
  const express = require("express");
  const router = express.Router();
  
  const { people } = require("../data/data");
  
  // get all people
  router.get("/", (req, res) => {
    res.status(200).json({ success: true, data: people });
  });
  
  // post request
  router.post("/", (req, res) => {
    const { name } = req.body;
    if (!name) {
      return res
        .status(400)
        .json({ success: false, msg: "Please Provide Credentials" });
    }
    res.status(201).json({
      success: true,
      data: [...people, { id: people.length + 1, name: name }],
    });
  });
  
  router.delete("/:id", (req, res) => {
    const { id } = req.params;
    const person = people.find((person) => person.id === Number(id));
    if (!person) {
      return res
        .status(404)
        .json({ success: false, msg: `Person Not Found with id: ${id}` });
    }
    const newPeople = people.filter((person) => person.id !== Number(id));
    res.status(200).json({ success: true, data: newPeople });
  });
  
  router.put("/:id", (req, res) => {
    const { id } = req.params;
    const { name } = req.body;
    if (!name) {
      return res.status(400).json({ success: false, msg: "Please Provide Name" });
    }
    const person = people.find((person) => person.id === Number(id));
    if (!person) {
      return res
        .status(404)
        .json({ success: false, msg: `Person Not Found with id ${id}` });
    }
    const newPeople = people.map((person) => {
      if (person.id === Number(id)) {
        person.name = name;
      }
      return person;
    });
    res.status(200).json({ success: true, data: newPeople });
  });
  
  module.exports = router;

  ```

  ### node\myexpressapp\routes\auth.js

  ```js
  const express = require("express");
  const router = express.Router();
  
  router.post("/", (req, res) => {
    console.log(req.body);
    const { name } = req.body;
    if (!name) {
      return res.status(401).send("<h1>Please Provide Credentials</h1>");
    }
    return res
      .status(200)
      .send(
        `<h1>Welcome ${name.slice(0, 1).toUpperCase() + name.slice(1)}!</h1>`
      );
  });
  
  module.exports = router;

  ```

  ### node\myexpressapp\data\data.js

  ```js
  const people = [
    { id: 1, name: "john" },
    { id: 2, name: "peter" },
    { id: 3, name: "susan" },
    { id: 4, name: "anna" },
    { id: 5, name: "emma" },
  ];
  module.exports = { products, people };
  ```

  ![image](https://github.com/user-attachments/assets/807d705c-649a-48bb-b8de-7231008725c6)
  ![image](https://github.com/user-attachments/assets/bd288ac0-ed5e-4644-af18-4b0f5f1f9034)
  ![image](https://github.com/user-attachments/assets/dbfa0e9c-060a-4be2-9b96-742a73d26550)
  ![image](https://github.com/user-attachments/assets/81a6912c-a6bf-4193-ab5f-156d8ff20439)

</details>

<details>
  <summary>Node Express - Controllers with Routes </summary>

  ### node\myexpressapp\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 5000;
  
  const people = require("./routes/people");
  const auth = require("./routes/auth");
  
  // static assets
  app.use(express.static("./public"));
  
  // parse form data
  app.use(express.urlencoded({ extended: false }));
  
  // parse json
  app.use(express.json());
  
  // people route
  app.use("/api/v1/people", people);
  
  // auth route
  app.use("/login", auth);
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\myexpressapp\routes\people.js
  
  ```js
  const express = require("express");
  const router = express.Router();
  
  const {
    getPeople,
    createPerson,
    deletePerson,
    updatePerson,
  } = require("../controllers/peopleControllers");
  
  // get all people
  router.get("/", getPeople);
  
  // post request
  router.post("/", createPerson);
  
  // router.route("/").get(getPeople).post(createPerson);
  
  // delete person
  router.delete("/:id", deletePerson);
  
  // update person
  router.put("/:id", updatePerson);
  
  module.exports = router;

  ```

  ### node\myexpressapp\controllers\peopleControllers.js

  ```js
  const { people } = require("../data/data");
  
  // get all people
  const getPeople = (req, res) => {
    res.status(200).json({ success: true, data: people });
  };
  
  // post request
  const createPerson = (req, res) => {
    const { name } = req.body;
    if (!name) {
      return res
        .status(400)
        .json({ success: false, msg: "Please Provide Credentials" });
    }
    res.status(201).json({
      success: true,
      data: [...people, { id: people.length + 1, name: name }],
    });
  };
  
  // delete person
  const deletePerson = (req, res) => {
    const { id } = req.params;
    const person = people.find((person) => person.id === Number(id));
    if (!person) {
      return res
        .status(404)
        .json({ success: false, msg: `Person Not Found with id: ${id}` });
    }
    const newPeople = people.filter((person) => person.id !== Number(id));
    res.status(200).json({ success: true, data: newPeople });
  };
  
  // update person
  const updatePerson = (req, res) => {
    const { id } = req.params;
    const { name } = req.body;
    if (!name) {
      return res.status(400).json({ success: false, msg: "Please Provide Name" });
    }
    const person = people.find((person) => person.id === Number(id));
    if (!person) {
      return res
        .status(404)
        .json({ success: false, msg: `Person Not Found with id ${id}` });
    }
    const newPeople = people.map((person) => {
      if (person.id === Number(id)) {
        person.name = name;
      }
      return person;
    });
    res.status(200).json({ success: true, data: newPeople });
  };
  
  module.exports = { getPeople, createPerson, deletePerson, updatePerson };

  ```

  ### node\myexpressapp\data\data.js
  
  ```js
  const people = [
    { id: 1, name: "john" },
    { id: 2, name: "peter" },
    { id: 3, name: "susan" },
    { id: 4, name: "anna" },
    { id: 5, name: "emma" },
  ];

  module.exports = { people };
  ```

  ![image](https://github.com/user-attachments/assets/8af8990e-d080-45dc-b55e-1cecb559ac20)
  ![image](https://github.com/user-attachments/assets/b639c838-b857-4c71-9c5f-9cfe7160d4f7)
  ![image](https://github.com/user-attachments/assets/472365ce-cb07-4b35-8df9-d80ec8114ce1)

</details>

<details>
  <summary>Node myTaskManager Project - Setup </summary>

  ### node\mytaskmanager\app.js
  
  ```js
  console.log("Task Manager App");
  ```

  ### node\mytaskmanager\package.json

  ```json
  {
    "name": "jobs",
    "version": "1.0.0",
    "description": "",
    "main": "app.js",
    "scripts": {
      "start": "nodemon app.js"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "dependencies": {
      "dotenv": "^8.2.0",
      "express": "^4.17.1",
      "mongoose": "^5.11.10"
    },
    "devDependencies": {
      "nodemon": "^2.0.7"
    }
  }
  ```

  ### Install dependencies and start project

  ```
  npm install && npm start
  ```

  ![image](https://github.com/user-attachments/assets/b953b7db-1baa-4d3f-9a98-7bd571b8e476)

</details>

<details>
  <summary>Node myTaskManager Project - First Page </summary>

  ### node\mytaskmanager\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 3000;
  
  // routes
  app.get("/", (req, res) => {
    res.send("<h1>Task Manager App</h1>");
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ![image](https://github.com/user-attachments/assets/d1691776-907e-4a0f-bedf-11623433578f)
  ![image](https://github.com/user-attachments/assets/11f0a91a-0ab2-4107-8643-76c2dd3d07d9)

</details>

<details>
  <summary>Node myTaskManager Project - Setup getAllTasks Route and Controller </summary>

  ### node\mytaskmanager\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 3000;
  const tasks = require("./routes/tasks");
  
  //middleware
  app.use(express.json());
  
  // routes
  app.get("/", (req, res) => {
    res.send("<h1>Task Manager App</h1>");
  });
  
  //get all tasks
  app.use("/api/v1/tasks", tasks);
  
  //create a task
  app.post("/api/v1/tasks", (req, res) => {
    res.send("Create a task");
  });
  
  //get a single task
  app.get("/api/v1/tasks/:id", (req, res) => {
    res.send("Get a single task");
  });
  
  //update a task
  app.patch("/api/v1/tasks/:id", (req, res) => {
    res.send("Update a task");
  });
  
  //delete a task
  app.delete("/api/v1/tasks/:id", (req, res) => {
    res.send("Delete a task");
  });
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });

  ```

  ### node\mytaskmanager\routes\tasks.js
  
  ```js
  const express = require("express");
  const router = express.Router();
  const { getAllTasks } = require("../controllers/tasksController");
  
  router.route("/").get(getAllTasks);
  
  module.exports = router;
  ```

  ### node\mytaskmanager\controllers\tasksController.js

  ```js
  const getAllTasks = (req, res) => {
    // res.send("<h1>Get all tasks</h1>");
    res.json({
      status: "success",
      data: {
        tasks: ["task1", "task2", "task3"],
      },
    });
  };
  
  module.exports = { getAllTasks };
  ```

  ![image](https://github.com/user-attachments/assets/ee48f881-624d-4c94-a123-dec06ee9ec5b)
  ![image](https://github.com/user-attachments/assets/f8ac9298-2251-4a50-9c68-1042d3a95e44)

</details>

<details>
  <summary>Node myTaskManager Project - Setup All Routes and Controllers </summary>

  ### node\mytaskmanager\app.js

  ```js
  const express = require("express");
  const app = express();
  const port = 3000;
  const tasks = require("./routes/tasks");
  
  //middleware
  app.use(express.json());
  
  // routes
  app.get("/", (req, res) => {
    res.send("<h1>Task Manager App</h1>");
  });
  
  // tasks
  app.use("/api/v1/tasks", tasks);
  
  app.listen(port, () => {
    console.log(`server is listening on port ${port}...`);
  });
  ```

  ### node\mytaskmanager\routes\tasks.js
  
  ```js
  const express = require("express");
  const router = express.Router();
  const {
    getAllTasks,
    createTask,
    getTask,
    updateTask,
    deleteTask,
  } = require("../controllers/tasksController");
  
  router.route("/").get(getAllTasks).post(createTask);
  router.route("/:id").get(getTask).patch(updateTask).delete(deleteTask);
  
  module.exports = router;
  ```

  ### node\mytaskmanager\controllers\tasksController.js

  ```js
 //get all tasks
  const getAllTasks = (req, res) => {
    // res.send("<h1>Get all tasks</h1>");
    try {
      res.json({
        status: "success",
        code: 200,
        data: {
          tasks: ["task1", "task2", "task3"],
        },
      });
    } catch (error) {
      res.status(500).json({
        status: "error",
        code: 500,
        message: "Internal server error",
      });
    }
  };
  
  //get a single task
  const getTask = (req, res) => {
    //   res.send("Get a single task");
    res.json({
      status: "success",
      code: 200,
      message: "single task fetched successfully",
      data: {
        task: { id: req.params.id },
      },
    });
  };
  
  //create a task
  const createTask = (req, res) => {
    //   res.send("Create a task");
    res.json({
      status: "success",
      code: 201,
      message: "task created successfully",
      data: {
        task: req.body.task,
      },
    });
  };
  
  //update a task
  const updateTask = (req, res) => {
    //   res.send("Update a task");
    res.json({
      status: "success",
      code: 200,
      message: "task updated successfully",
      data: {
        id: req.params.id,
        task: req.body.task,
      },
    });
  };
  
  //delete a task
  const deleteTask = (req, res) => {
    //   res.send("Delete a task");
    res.json({
      status: "success",
      code: 200,
      message: "task deleted successfully",
      data: {
        task: { id: req.params.id },
      },
    });
  };
  
  module.exports = { getAllTasks, createTask, getTask, updateTask, deleteTask };
  ```

  ![image](https://github.com/user-attachments/assets/7be67666-dbf2-47ea-822e-a74c8d09230f)
  ![image](https://github.com/user-attachments/assets/6a433926-6663-433f-a398-be15a6e31ea9)
  ![image](https://github.com/user-attachments/assets/8a20bdb9-85dc-47fa-96bb-bf013c6e40dc)
  ![image](https://github.com/user-attachments/assets/8491c26e-10c6-4394-9d66-d6e15227c798)
  ![image](https://github.com/user-attachments/assets/22721c54-f525-492d-a052-3d0f29a21005)
  ![image](https://github.com/user-attachments/assets/0946d2ad-9344-488c-b5c3-52e83083808c)

</details>

<details>
  <summary>Node myTaskManager Project - Setup Database Connection with Mongoose and Mongodb.com </summary>

  ### Install Mongoose 

  ```sh
  npm i mongoose
  npm install mongoose@latest  
  ```

  ### Mongodb.com Connection String

  ```sh
  mongodb+srv://<username>:<db_password>@cluster0.unp2imh.mongodb.net/<db_name>?retryWrites=true&w=majority&appName=Cluster0
  ```

  ### LABS\node\mytaskmanager\app.js

  ```js
  const connectDB = require("./db/connect");
  const express = require("express");
  const app = express();
  const port = 3000;
  const tasks = require("./routes/tasks");
  
  //middleware
  app.use(express.json());
  
  // routes
  app.get("/", (req, res) => {
    res.send("<h1>Task Manager App</h1>");
  });
  
  // tasks
  app.use("/api/v1/tasks", tasks);
  
  app.listen(port, () => {
    // Connect to database
    connectDB();
    console.log(`server is listening on port ${port}...`);
  });
  ```

  ### LABS\node\mytaskmanager\db\connect.js
  
  ```js
  const mongoose = require("mongoose");
  
  const connectDB = async () => {
    try {
      const username = "";
      const password = "";
      const db_name = "";
  
      const connectionString = `mongodb+srv://${username}:${password}@cluster0.unp2imh.mongodb.net/${db_name}?retryWrites=true&w=majority&appName=Cluster0`;
  
      const conn = await mongoose.connect(connectionString);
  
      console.log(`MongoDB: CONNECTED TO THE DB.... ${conn.connection.host}`);
    } catch (error) {
      console.error(`MongoDB: CONNECTION ERROR.... ${error.message}`);
      process.exit(1);
    }
  };
  
  module.exports = connectDB;
  ```

  ![image](https://github.com/user-attachments/assets/a560f090-cf9a-4ad6-af92-a774db3a6ee2)


</details>

<details>
  <summary>Node myTaskManager Project - Setup ENV VARS for Credentials </summary>

  ### Install dotenv

  ```js
  npm install dotenv@latest
  ```

  ### LABS\node\mytaskmanager\app.js

  ```js
  require("dotenv").config();
  const connectDB = require("./db/connect");
  const express = require("express");
  const app = express();
  const port = 3000;
  const tasks = require("./routes/tasks");
  
  //middleware
  app.use(express.json());
  
  // routes
  app.get("/", (req, res) => {
    res.send("<h1>Task Manager App</h1>");
  });
  
  // tasks
  app.use("/api/v1/tasks", tasks);
  
  app.listen(port, async () => {
    // Connect to database
    await connectDB();
    console.log(`server is listening on port ${port}...`);
  });
  ```

  ### LABS\node\mytaskmanager\db\connect.js
  
  ```js
  const mongoose = require("mongoose");

  const connectDB = async () => {
    const USERNAME = process.env.DB_USERNAME;
    const PASSWORD = process.env.DB_PASSWORD;
    const DB_NAME = process.env.DB_NAME;
  
    try {
      const connectionString = `mongodb+srv://${USERNAME}:${PASSWORD}@cluster0.unp2imh.mongodb.net/${DB_NAME}?retryWrites=true&w=majority&appName=Cluster0`;
  
      const conn = await mongoose.connect(connectionString);
      console.log(`MongoDB: CONNECTED TO THE DB.... ${conn.connection.host}`);
    } catch (error) {
      console.error(`MongoDB: CONNECTION ERROR.... ${error.message}`);
      process.exit(1);
    }
  };
  
  module.exports = connectDB;
  ```

  ### LABS\node\mytaskmanager\.env

  ```sh
  NODE_ENV=development

  DB_USERNAME=******
  DB_PASSWORD=*****
  DB_NAME=*********
  ```

  ### LABS\node\mytaskmanager\.gitignore

  ```sh
  /node_modules
  .env
  keys.txt 
  ```

  ![image](https://github.com/user-attachments/assets/c1414f9b-b49d-4a0a-9a09-04520b475681)

</details>

<details>
  <summary>Node myTaskManager Project - Setup Mongoose Schema and Model </summary>

  ### LABS\node\mytaskmanager\app.js

  ```js

  ```

  ### n
  
  ```js

  ```

  ### n

  ```js
 
  ```



</details>































<details>
  <summary>Node myTaskManager Project -  </summary>

  ### LABS\node\mytaskmanager\app.js

  ```js

  ```

  ### n
  
  ```js

  ```

  ### n

  ```js
 
  ```



</details>























<hr>











