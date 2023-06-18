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

   ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f02fb596-b746-48d6-aef8-140042130a8e/Untitled.png)

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

   ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a3fd3ed4-2b75-4085-af69-a837e3be4392/Untitled.png)

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

9. And add devServer with port number to `webpack.congif.js`:
   - Code of `webpack.congif.js`
     ```html
     const path = require("path"); const HtmlWebpackPlugin =
     require("html-webpack-plugin"); module.exports = { entry: "./index.js",
     output: { filename: "bundle.js", path: path.resolve(__dirname, "dist"),
     clean: true, }, plugins: [ new HtmlWebpackPlugin({ template: "index.html",
     }), ], module: { rules: [ { test: /\.s[ac]ss$/i, use: [ // Creates `style`
     nodes from JS strings "style-loader", // Translates CSS into CommonJS
     "css-loader", // Compiles Sass to CSS "sass-loader", ], }, ], }, devServer:
     { port: 9000, open: true, }, };
     ```
10. And change _start_ script in `package.json`:


    ```html
    "start": "npx webpack-dev-server --mode development"
    ```

### So, structure of project is:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a0a9d2b8-3d06-4c7d-8823-422e97b0cd30/Untitled.png)
