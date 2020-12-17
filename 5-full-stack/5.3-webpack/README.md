# 5.3: Webpack

## Why Webpack

When running the front end of our applications we deal with collecting the correct libraries at the last step, that is, when the user's browser is running the link and script tags, as the last step in the process of HTTP request and response.

In fact this system is inefficient, since we know about what set of files the user needs way before each individual user requests for a page- we know what set of JavaScript and CSS _**every**_ user needs when we finish writing the app.

Instead of letting the set of JavaScipt and CSS files collate in _**each**_ users' browser, we can pre-process / prepare the set of front-end files we want before the Express.js server even starts.

We are now building a back-end to the front-end JavaScript that runs in the browser. A back-end that does not depend on or interact with our Express.js app.

Webpack is the command line tool that prepares these sets of files.

![](../../.gitbook/assets/webpac.jpg)



1. The webpack command is run. Webpack, based on the settings, takes the src/script.js file \(or whatever other files or groups of files are specified\) and transforms it, putting the resulting file in `./dist`. The Express.js server starts at some point with `node index.js` in the command line. The server is ready to accept requests.
2. The browser makes a request to the server for a page.
3. The browser reads a script tag in the HTML response. The script tag `src` source triggers a get request.
4. The Express.js server, based on the request path, looks in the hard drive for a file that matches the request. This script tag requests the transformed `script.js` file in `./dist`.
5. Because the request was kicked off from a script tag, the file contents response is digested by the JavaScript interpreter of the browser.

## Webpack Example

Create a directory and install webpack

```text
mkdir webpack-demo
cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev
```

Create some files to work with:

```text
mkdir src dist
touch src/script.js
touch dist/index.html
```

#### src/script.js

```text
const component = () => {

  // create an element
  const element = document.createElement('h1');

  // set the contents
  element.innerHTML = 'Hello!'

  // return the element
  return element;
}

document.body.appendChild(component());
```

#### dist/index.html

```text
 <!DOCTYPE html>
 <html>
   <head>
     <meta charset="utf-8" />
     <title>Getting Started</title>
   </head>
   <body>
    <script src="main.js"></script>
   </body>
 </html>
```

### Webpack configuration:

#### webpack.config.js

```text
const path = require('path');

module.exports = {
  entry: './src/script.js',
  output: {
    filename: 'script.js',
    path: path.resolve(__dirname, 'dist'),
  },
};
```

### Running Webpack

When we run `webpack` it will transform our `script.js` into `script.js` in the `dist` directory.

```text
npx webpack --mode=production
```

Look inside the `dist/script.js` to see the transformed JavaScript file. Note in what ways Webpack has transformed the file. Note that the comments are gone from the output file.

Try to paste in some other JavaScript into the source file and see what changes.
