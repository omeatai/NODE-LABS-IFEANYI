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
  <summary>Node Modules </summary>

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
  <summary>Node </summary>

  ### node\myapp\app.js:

  ```js

  ```

  ```
  node app.js
  ```

  

</details>










