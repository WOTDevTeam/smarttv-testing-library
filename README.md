# smarttv-testing-library


## Getting Started
1. Add the tests folder to the project's root
2. Create a new webpack config with the following plugin: (An example is included in this repo)
```
plugins: [
    new CopyWebpackPlugin({
        patterns: [
            { from: 'tests', to: 'tests' },
        ],
    }),
    new DefinePlugin({
        TESTING: JSON.stringify(true),
    }),
]
```
3. Add the following plugin to all other webpack configs
```
plugins: [
    new DefinePlugin({
        TESTING: JSON.stringify(false),
    }),
]
```
4. Add the following scripts to the package.json:
```
"build-test": "webpack --config webpack.testing.js"
"start-test": "webpack serve --open --hot --config webpack.testing.js"
```
5. Add the following lines to your index.jsx file:
```
if (TESTING) {
    const testingLib = document.createElement('script')
    testingLib.type = 'text/javascript'
    testingLib.src = './tests/testingLib.js'
    document.body.appendChild(testingLib)
}
```
6. Add your commands to tests.json
7. Launch the app with build-test or start-test


## Commands
```waitForElement(selector)```: Waits for an element to load

```keyPress(key)```: Simulates a key press

```click(selector)```: Simulates a click on a element

```wait(time in ms)```: Adds a delay

```type(selector,text)```: Changes the value of a field

```typeWithKeyboard(selector,text)```: Uses the keyboard with a matching selector to type the given text

```asserts(selector,expected)```: Checks if the value of an element matches an expected value

```beaconStart()```: Starts a timer and prepares a report. Only commands included after this one will be included
