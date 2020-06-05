<h1 align="center">
  <br>
  <a href="http://github.com/elbrodelche"><img src="https://img-a.udemycdn.com/course/750x422/2470214_97a0_4.jpg" alt="Testing React with Cypress" width="600"></a>
  <br>
  Testing React with Cypress
  <br>
</h1>
<div align="center">
  :computer:
</div>
<div align="center">
  Usefull tips using <code>cypress</code> with some examples
</div>

<br />

<div align="center">
  <sub>These are some notes shred by
  <a href="https://github.com/elbrodelche">
  Juan Carlos Migliavacca
  </a>
</div>

## Table of Contents
- [Installation](#install-cypress)
- [Configuration](#configuration-file)
- [Example test](#example-test)
- [Running test simultaneously](#running-test-simultaneously)
- [See also](#see-also)
- [License](#license)

## Install Cypress
Cypress will install a whole application itself with the following command:
```bash
npm i --save-dev cypress
```

Once finished it installs an app that is exposed on node_modules, so you can use npx. 

```bash
npx cypress open
```

This command will open cypress and an example test, and create the following structure:

```bash
cypress                      
├── fixtures        // Set objects that can be reused
├── integration     // The actual tests folder
├── plugins         // Cypress plugins
└── support 
    |__commands.js  // Location for custom commands 
cypress.json        // Config file
```

# Configuration file

This is an example of a cypress,js config file

```bash
{
"baseUrl":"http://localhost:8080/"      // Where the app lives
"integrationFolder":"cypress/e2e"       // To change the name of integation folder (optional)
}
```

# Example test

This is the first test

```javascript
/* globals cy */
describe('calculator', () => {
  it('can visit the app', () => {
    cy
      .visit('/')
      .getByText(/^1$/)
      .click()
      .getByText(/^\+$/)
      .click()
      .getByText(/^2$/)
      .click()
      .getByText(/^=$/)
      .click()
      .getByTestId("number-display")    // Select by test id
  })
})

```

We can actually grab any object in the DOM by using **data-testid**

```javascript
<AutoScalingText data-testid="number-display">{formattedValue}</AutoScalingText>
```

# Running test simultaneously
For running simultaneous tests we are gong to use npm-run-all
```bash
npm i --save-dev npm-run-all
```

Now we can add to our script on package.json the following:

```javascript
"cy:run": "cypress run",
"cy:open": "cypress open",
"pretest:e2e": "npm run build",
"test:e2e": "npm-run-all --parallel --race start cy:run",   // for running on CI server
"test:e2e:dev": "npm-run-all --parallel --race dev cy:open",
```

# Testing trophy

![](https://s3.amazonaws.com/media-p.slid.es/uploads/55780/images/4579002/testing-trophy.png)


# See Also
- [Testing React Applications](https://frontendmasters.com/courses/testing-react/) - Front End Masters great course
- [Cypress](http://stack.gl/) - End to end testing software
- [Chromium](http://stack.gl/) - Open Source web browser
- [CI configuration](https://docs.cypress.io/es/guides/guides/continuous-integration.html#Setting-up-CI) - Oficial docs where CI config is described


# License
[MIT](https://tldrlegal.com/license/mit-license)
