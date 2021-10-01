>   mkdir project-manual
>   mkdir src
>   mkdir dist
# genearete package.json using npm init
>   npm init
> npm install type script --save-dev

 create a new file called tsconfig.json
 add following :

 { 
  "compilerOptions": { 
    "target": "es5", 
    "module": "es6", 
    "moduleResolution": "node", 
    "lib": ["es6", "dom"],
    "sourceMap": true, 
    "jsx": "react", 
    "strict": true, 
    "noImplicitReturns": true,
    "rootDir": "src",
    "outDir": "dist",
  },
  "include": ["**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}

# add static analysis tool that checks TypeScript code for readability, maintainability, and functionality errors.
npm install tslint --save-dev

create file 
tslint.json :
pate following in tslint.json 
{
  "extends": ["tslint:recommended", "tslint-react", "tslint-config-prettier"],
  "linterOptions": {
    "exclude": ["node_modules/**/*.ts"]
  }
}

#Adding React with types
npm install react react-dom
npm install @types/react @types/react-dom --save-dev

# create index.html 
with following :

<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8"/>
</head>
<body>
  <div id="root"></div>
  <script src="bundle.js"></script>
</body>
</html>

add src/index.tsx
import * as React from "react";
import * as ReactDOM from "react-dom";

const App: React.SFC = () => {
  return <h1>My React App!</h1>;
};

ReactDOM.render(<App />, document.getElementById("root") as HTMLElement);


# Adding webpack
Webpack is a popular tool that we can use to bundle all our JavaScript code into the bundle.js file that our index.html is expecting.

Install webpack and its command-line interface into our project as development dependencies, by entering the following command in the terminal:

npm install webpack webpack-cli --save-dev

# Webpack also has a handy web server that we can use during development. So, let's install that as well via the terminal:
npm install webpack webpack-dev-server --save-dev


# There's one final task to complete before we can start configuring webpack. This is to install a webpack plugin called ts-loader, which will help it load our TypeScript code. Install this as follows:


npm install ts-loader --save-dev

# Now that we have all this webpack stuff in our project, it's time to configure it. Create a file called webpack.config.js in the project root, and enter the following into it:

const path = require("path");

module.exports = {
  entry: "./src/index.tsx",
  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: "ts-loader",
        exclude: /node_modules/
      }
    ]
  },
  resolve: {
    extensions: [".tsx", ".ts", ".js"]
  },
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js"
  },
  devServer: {
    contentBase: path.join(__dirname, "dist"),
    compress: true,
    port: 9000
  }
};

# Project folders and files

├─ dist/
  ├─ bundle.js
  ├─ index.html
├─ node_modules/
├─ src/
  ├─ index.tsx 
├─ package.json
├─ tsconfig.json
├─ tslint.json
├─ webpack.config.js
