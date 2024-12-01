# cypress-visual-regression
using cypress-visual-regression plugin for verifying web page

Assume you already installed Cypress and done ready to code :)

Install Cypress visual regression
npm install cypress-visual-regression

JavaScript
Configure visual regression plugin 
where? in cypress.config.js

importing the configureVisualRegression function from the cypress-visual-regression plugin
const { configureVisualRegression } = require('cypress-visual-regression')

configure environment variables
module.exports = defineConfig({
  e2e: {
    env: {
      visualRegressionType: "base",
      visualRegressionBaseDirectory: "cypress/snapshots/base",
      visualRegressionDiffDirectory: "cypress/snapshots/diff",
    },
    setupNodeEvents(on, config) {
      // implement node event listeners here
      configureVisualRegression(on);
    },
  },
});

your test/spect file
describe("Visual Regression Test", () => {
  it("should capture the base screenshot", () => {
    cy.visit("https://example.cypress.io/todo"); // Replace with your site URL
    cy.compareSnapshot("base-screenshot"); // screenshot name
  });
});

execute
you will notice two folders created under cypress 
cypress\snapshots\base (cypress\screenshots\cypress\e2e\1-getting-started\visualTesting.cy.js)
cypress\screenshots (cypress\snapshots\base\cypress\e2e\visualTesting.cy.js)
now base screenshots are captured

update configuration to perform visual testing earlier given as "base"
visualRegressionType: "regression"

execute
it will capture a new screenshot place it in the "screenshots" folder and compare it with the screenshot in the "snapshots/base" of that spec file

update base screenshot manually to validate failed scenario

execute
the test will fail and a screenshot is placed below with the differences found
cypress\snapshots\diff\cypress\e2e\visualTesting.cy.js
