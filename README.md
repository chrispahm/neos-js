# NEOS Server JavaScript Client

A complete [XML-RPC client](https://neos-server.org/neos/xml-rpc.html) for the [Neos Numerical Optimisation Server](https://neos-server.org/neos/). Works in the browser and Node.js

For parsing the results of a GAMS job returned by NEOS, check out [gams2js](https://github.com/chrispahm/gams2js)!

## Installation
To install via npm:
```
npm install neos-js
```

Or grab a release archive file from the dist folder.

## Examples
Browser:
In the header include
```html
<script src="assets/neos.min.js"></script>
```
then
```html
<script type="text/javascript">
NEOS.xmlstring({
  category: 'LP',
  solver: 'CPLEX',
  inputMethod: 'GAMS',
  model: simulationModelString,
  email: 'test@test.com'
})
.then(NEOS.submitJob)
.then(NEOS.getFinalResults)
.then(res => {
  // work with the resulting listing file
})
.catch(err => {
  // catch errors
})
</script>
```

Check out the [NEOS online editor](https://fruchtfolge.github.io/neos-js/index.html) example

Node.js
```js
const NEOS = require('neos-js')
const fs = require('fs')

// load a simulation model, in this case a GAMS file
const model = fs.readFileSync('transport_model.gms', 'utf-8')

// convert the simulation model into a NEOS XML string,
// solve and await the results
NEOS.xmlstring({
  category: 'LP',
  solver: 'CPLEX',
  inputMethod: 'GAMS',
  model: simulationModelString,
  email: 'test@test.com'
})
.then(NEOS.submitJob)
.then(NEOS.getFinalResults)
.then(res => {
  // work with the resulting listing file
})
.catch(err => {
  // catch errors
})
```
## Methods
For a complete list of the available methods, visit the [Neos Server XML-RPC API documentation](https://neos-server.org/neos/xml-rpc.html).

Additional methods:
```
prepareJob(template, model, email)
```  
Convenience method. Converts your simulation model (string) into the required NEOS XML format that you get from the `getSolverTemplate` method. An email is required for some solvers (e.g. CPLEX), so make sure to pass one.

```
xmlstring(json)
```
Convert a JavaScript object containing the properties required for running a NEOS
job into a NEOS compatible XML string. The object properties should adhere to the
properties retrieved from the `getSolverTemplate` method (without the surrounding `document` tag).

```
parseXML(xmlstring)
```
Parse an XML string retrieved by NEOS, e.g. the result from the `getSolverTemplate`
call.

## Contribution

Contribution is highly appreciated! Make sure to ```npm test``` before submitting a PR

## License
MIT
