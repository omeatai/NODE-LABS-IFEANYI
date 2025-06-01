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













































