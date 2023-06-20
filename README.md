# simplewebpack

Example of Webpack project with vanilia HTML and SASS.
Clone it and run `npm install`.

Guide to create project like this one:

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

4. Create `webpack.config.js` file

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

11. And change _start_ script in `package.json`:

    ```jsx
    "start": "npx webpack-dev-server --mode development"
    ```

12. Add possibility for files coping to a folder:

    Add a CopyPlugin

    ```html
    npm install copy-webpack-plugin --save-dev
    ```

    And add to webpack.config.js this:

    ```jsx
    const CopyPlugin = require("copy-webpack-plugin");
    ```

    This add to plugins configuration:

    ```jsx
    new CopyPlugin({
    	patterns: [{ from: ".src/", to: ".src/" }],
    }),
    ```
