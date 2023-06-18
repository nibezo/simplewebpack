# simplewebpack

Example of Webpack project with vanilia HTML and SASS.

1. Create nodejs project:

   ```jsx
   node init
   ```

2. Add webpack as dev dependence:

   ```jsx
   npm i -D webpack webpack-cli
   ```

3. In `package.json` add two scripts for dev and prod:

   ```jsx
   "scripts": {
   		"build": "npx webpack --mode production",
   		"start": "npx webpack --mode development"
   	},
   ```

4. Create `webpack.config.js` file:

   <img src="https://github.com/nibezo/simplewebpack/assets/52705623/643e2b65-8144-421b-8133-0aa2ec5b5e65" width="250" height="40">


5. Add HTML plugin and setup it:

   ```jsx
   npm install --save-dev html-webpack-plugin
   ```

   - `webpack.congif.js` after adding HTML plugin
     ```jsx
     const path = require("path");
     const HtmlWebpackPlugin = require("html-webpack-plugin");

     module.exports = {
     	entry: "./index.js",
     	output: {
     		filename: "bundle.js",
     		path: path.resolve(__dirname, "dist"),
     		clean: true,
     	},
     	plugins: [
     		new HtmlWebpackPlugin({
     			template: "index.html",
     		}),
     	],
     };
     ```

6. Install 3 loader for basic SASS styling:

   ```jsx
   npm install --save-dev style-loader
   ```

   ```jsx
   npm install --save-dev css-loader
   ```

   ```jsx
   npm install sass-loader sass webpack --save-dev
   ```

7. Create style.scss, simple HTML template and edit `webpack.congif.js`:
   
   <img src="https://github.com/nibezo/simplewebpack/assets/52705623/bd565f9e-133f-4eaa-ba5c-6596a69ba699" width="250" height="30">

   - index.html
     ```html
     <!DOCTYPE html>
     <html lang="en">
     	<head>
     		<meta charset="UTF-8" />
     		<meta
     			name="viewport"
     			content="width=device-width, initial-scale=1.0"
     		/>
     		<title>Document</title>
     	</head>
     	<body>
     		This is a simple example of project with webpack!
     	</body>
     </html>
     ```
   - index.js
     ```jsx
     import "./style.scss";
     ```
   - style.scss
     ```sass
     $body-color: rgb(138, 255, 160);

     body {
     	background-color: black;
     	font-size: 2em;
     	color: $body-color;
     }
     ```
   - webpack.congif.js
     ```jsx
     const path = require("path");
     const HtmlWebpackPlugin = require("html-webpack-plugin");

     module.exports = {
     	entry: "./index.js",
     	output: {
     		filename: "bundle.js",
     		path: path.resolve(__dirname, "dist"),
     		clean: true,
     	},
     	plugins: [
     		new HtmlWebpackPlugin({
     			template: "index.html",
     		}),
     	],
     	module: {
     		rules: [
     			{
     				test: /\.s[ac]ss$/i,
     				use: [
     					// Creates `style` nodes from JS strings
     					"style-loader",
     					// Translates CSS into CommonJS
     					"css-loader",
     					// Compiles Sass to CSS
     					"sass-loader",
     				],
     			},
     		],
     	},
     };
     ```

8. Add dev server for live-coding: 
    
    ```html
    npm i -D webpack-dev-server
    ```
9. And add devServer with port number to ```webpack.congif.js```:
   ```js
   const path = require("path");
   const HtmlWebpackPlugin = require("html-webpack-plugin");
   
   module.exports = {
   	entry: "./index.js",
   	output: {
   		filename: "bundle.js",
   		path: path.resolve(__dirname, "dist"),
   		clean: true,
   	},
   	plugins: [
   		new HtmlWebpackPlugin({
   			template: "index.html",
   		}),
   	],
   	module: {
   		rules: [
   			{
   				test: /\.s[ac]ss$/i,
   				use: [
   					// Creates `style` nodes from JS strings
   					"style-loader",
   					// Translates CSS into CommonJS
   					"css-loader",
   					// Compiles Sass to CSS
   					"sass-loader",
   				],
   			},
   		],
   	},
   	devServer: {
   		port: 9000,
   		open: true,
   	},
   };
   ```
10.  And change *start* script in `package.json`:
      ```jsx
      "start": "npx webpack-dev-server --mode development"
      ```
### So, structure of project is:

   <img src="https://github.com/nibezo/simplewebpack/assets/52705623/846cd477-2b79-4651-8382-bd86c6c8426f" width="400" height="350">
