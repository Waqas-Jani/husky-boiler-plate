# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)


# Husky, EsLint and Prettier Setup In Fresh

Packages need to install in devDependencies

```sh
cd project-folder
npm i prettier eslint eslint-plugin-prettier husky lint-staged eslint-config-prettier -D
```
### Create the file .prettierrc and paste the config
```sh
{
	"trailingComma": "es5",
	"tabWidth": 4,
	"useTabs": true,
	"printWidth": 80,
	"semi": true,
	"singleQuote": true,
	"endOfLine": "lf"
}
```
### Run the command to generate the eslint configuration
```sh
npm init @eslint/config
```
There are different option and select according to your project.

| Option | Select |
| ------ | ------ |
| How would you like to use ESLint? | To check syntax, find problems, and enforce code style |
| What type of modules does your project use? | JavaScript modules (import/export) |
| Which framework does your project use? | Your Project e.g React | 
| Does your project use TypeScript? | If you are using Typescript "Yes" | 
| Where does your code run? | Browser |
| How would you like to define a style for your project? | Use a popular style guide |
| Which style guide do you want to follow? | Airbnb: [https://github.com/airbnb/javascript] |
| What format do you want your config file to be in? | JSON |
| Would you like to install them now? | Yes |
| Which package manager do you want to use? | Which you are using. e.g npm/yarn/pnpm |

### After that .eslintrc.json file created with default config. Paste below config or add which you want

```sh
{
	"env": {
		"browser": true,
		"es2021": true,
		"jest": true
	},
	"extends": ["plugin:react/recommended", "airbnb", "prettier"],
	"overrides": [
		{
			"files": ["src/**/*.jsx"]
		}
	],
	"parserOptions": {
		"ecmaFeatures": {
			"jsx": true
		},
		"ecmaVersion": "latest",
		"sourceType": "module"
	},
	"plugins": ["react", "prettier"],
	"rules": {
		"indent": [2, "tab"],
		"no-tabs": 0,
		"quotes": ["off", "single"], // error when double quotes
		"semi": "error", // when semi colon missing
		"comma-dangle": "off",
		"prettier/prettier": "error",
		"no-unused-vars": "error", // error when un-used var/let/const etc exist in a file
		"import/prefer-default-export": "off", // disable the export default required in a file,
		// "no-console": ["error", { "allow": ["warn", "error"] }],
		"no-console": "error",
		"react/jsx-props-no-spreading": [
			2,
			{
				"html": "enforce",
				"custom": "ignore",
				"explicitSpread": "ignore",
				"exceptions": ["Image", "img"]
			}
		],
		"jsx-a11y/anchor-is-valid": 0,
		"react/prop-types": "off",
		"react/jsx-curly-brace-presence": "off",
		"react/no-array-index-key": "off",
		"react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }]
	}
}
```
## Add the script into package.json file
```sh
"lint": "eslint . --fix --max-warnings=0",
"format": "prettier . --write",
"husky": "husky install"
```

### Note: In your project, maybe some files you don’t want to lint or format. So you can add them to .eslintignore file if haven't not then create it

```sh
node_modules
public
build
.cache
package-lock.json
```

## Husky 

To force our coding style & format, we will use git hook. So that if anyone commits any code, it runs some linting and check if there is any issue with it. For this, required packages installed above list.


### Edit package.json file and add below code
```sh
"lint-staged": {
		"**/*.{js,jsx}": [
			"npm run lint",
			"prettier --write"
		]
}
```
With these four lines, we are just linting and formatting our code. But it’s not called from anywhere now. So we need to call it from somewhere. But before that, we need to install husky properly to run it –

```sh
npx husky-init && npm install
```

This will create a folder called .husky and inside it a file called pre-commit which will run npm test before committing. But for the current project, we don’t want to run the npm test, so we are going to change it into –

```sh
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

# npm test
npx lint-staged
```

## All Done 


Refference Docs: [https://blog.nerdjfpb.com/how-to-add-eslint-prettier-and-husky-git-hook-in-react-js-2022/]








