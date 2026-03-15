# Playwright BDD Test Project

This project contains an end-to-end UI automation suite built with Playwright and Cucumber.
It validates multiple flows from The Internet test application using feature files, step definitions, and page objects.

## Framework Overview

This is a BDD-first automation framework where each business flow is represented as a feature file and executed through reusable page objects.

Core design goals:

- Readable scenarios for non-technical and technical users
- Reusable step definitions and page methods
- Data-driven coverage using centralized test data
- Clean and separate reporting outputs for full and tagged runs

## Tech Stack

- Playwright for browser automation
- Cucumber for BDD-style scenarios
- JavaScript for step definitions, page objects, and test data

## Project Structure

- `features/`stores `.feature` files grouped by business area
- `features/step-definitions/` stores Cucumber step implementations
- `pages/` stores page object classes for each page under test
- `pageObjects/` stores page object management helpers
- `test-data/` stores reusable datasets for tagged suites
- `reports/` stores generated JSON and HTML Cucumber reports
- `playwright-report/` stores the Playwright HTML report output
- `tests/` is configured as Playwright's `testDir` and currently holds project documentation

## How The Framework Works

Execution flow:

1. Cucumber reads scenarios from `features/*.feature`.
2. Matching step definitions execute from `features/step-definitions/*.steps.js`.
3. Step definitions call page object methods in `pages/`.
4. Browser/context lifecycle is managed from `features/step-definitions/hooks.js`.
5. Reports are generated in `reports/` as JSON and HTML.

### Hooks And Browser Lifecycle
- `Before` hook launches Chromium and creates a fresh browser context/page per scenario.
- `After` hook disposes API contexts and closes browser resources.
- Default timeout is configured centrally in hooks (`90s`) to reduce flaky timeout behavior.

### Page Object Model Pattern
- Each page class encapsulates selectors and actions for one app page.
- Step definitions stay concise by delegating UI logic to page objects.
- `pageObjects/POManager.js` acts as a helper layer to organize page object access.

### Data-Driven Approach
- Reusable data is placed in `test-data/*.data.js`.
- Tagged suites consume dedicated datasets to keep steps clean and maintainable.

## Tagging Strategy
The framework supports targeted execution by tags for faster feedback and suite partitioning:
- `@smoke` for critical path checks
- `@regression` for broad functional coverage
- Feature-group tags such as `@advanced-links`, `@auth-dynamic-links`, `@interaction-links`, `@browser-ui-links`, and `@secure-dom-links`

### Prerequisites
- Node.js installed
- npm installed

## Installation

### Run the following command from the project root:
npm install

## Run Tests
Run the default BDD suite:
npm run test

### Run all suites and generate all reports:
npm run test:all:reports

### Run tagged suites individually:
npm run test:bdd:smoke
npm run test:bdd:regression
npm run test:bdd:advanced
npm run test:bdd:auth-dynamic
npm run test:bdd:interaction
npm run test:bdd:browser-ui
npm run test:bdd:secure-dom


## Reports

Generated reports are available here after execution:

- `reports/cucumber-report.html`
- `reports/cucumber-smoke-report.html`
- `reports/cucumber-regression-report.html`
- `reports/cucumber-advanced-report.html`
- `reports/cucumber-auth-dynamic-report.html`
- `reports/cucumber-interaction-report.html`
- `reports/cucumber-browser-ui-report.html`
- `reports/cucumber-secure-dom-report.html`

Report usage guidance:

- HTML reports are best for manual review and sharing outcomes.
- JSON reports are useful for CI integration or post-processing.
- If a run is interrupted, regenerate reports to avoid partial JSON files.

## Local Debugging Tips

- Run one tagged suite at a time when troubleshooting failures.
- Use headed mode (`HEADLESS=false`) for UI step validation.
- Keep selectors and waits inside page objects to avoid duplicated timing logic.
- Re-run failed scenarios quickly with relevant tag commands.

## CI And Scalability Notes

- Current config targets Chromium for consistency and speed.
- The Playwright config already includes a project structure that can be extended to Firefox/WebKit when needed.
- Report files are separated by suite type, making it easier to publish artifacts per pipeline stage.

## Notes

- The project is currently configured to run in Chromium.
- Playwright config points to `./tests` as the native Playwright test directory.
- The active automated coverage in this repository is driven mainly through Cucumber feature files in `features/`.

# Project Structure

```text
PlaywrightAutomation/
|-- .github/
|-- .vscode/
|-- features/
|   |-- add-remove-elements.feature
|   |-- advanced-links.feature
|   |-- auth-dynamic-links.feature
|   |-- browser-ui-links.feature
|   |-- dom-window-links.feature
|   |-- interaction-links.feature
|   |-- navigation-links.feature
|   |-- secure-dom-links.feature
|   `-- step-definitions/
|       |-- advanced-links.steps.js
|       |-- auth-dynamic-links.steps.js
|       |-- browser-ui-links.steps.js
|       |-- dom-window-links.steps.js
|       |-- hooks.js
|       |-- interaction-links.steps.js
|       |-- navigation-links.steps.js
|       `-- secure-dom-links.steps.js
|-- node_modules/
|-- pageObjects/
|   `-- POManager.js
|-- pages/
|   |-- abTestingPage.js
|   |-- addRemoveElementsPage.js
|   |-- basicAuthPage.js
|   |-- brokenImagesPage.js
|   |-- challengingDomPage.js
|   |-- checkboxesPage.js
|   |-- contextMenuPage.js
|   |-- digestAuthPage.js
|   |-- disappearingElementsPage.js
|   |-- dragAndDropPage.js
|   |-- dropdownPage.js
|   |-- dynamicContentPage.js
|   |-- dynamicControlsPage.js
|   |-- dynamicLoadingPage.js
|   |-- entryAdPage.js
|   |-- exitIntentPage.js
|   |-- featurePage.js
|   |-- fileDownloadPage.js
|   |-- fileUploadPage.js
|   |-- floatingMenuPage.js
|   |-- forgotPasswordPage.js
|   |-- formAuthenticationPage.js
|   |-- framesPage.js
|   |-- geolocationPage.js
|   |-- homePage.js
|   |-- horizontalSliderPage.js
|   |-- hoversPage.js
|   |-- infiniteScrollPage.js
|   |-- inputsPage.js
|   |-- javascriptAlertsPage.js
|   |-- javascriptErrorPage.js
|   |-- jqueryUiMenusPage.js
|   |-- keyPressesPage.js
|   |-- largeDomPage.js
|   |-- multipleWindowsPage.js
|   |-- nestedFramesPage.js
|   |-- notificationMessagesPage.js
|   |-- redirectLinkPage.js
|   |-- secureFileDownloadPage.js
|   |-- shadowDomPage.js
|   |-- shiftingContentPage.js
|   |-- slowResourcesPage.js
|   |-- sortableDataTablesPage.js
|   |-- statusCodesPage.js
|   |-- typosPage.js
|   `-- wysiwygEditorPage.js
|-- playwright-report/
|   `-- index.html
|-- reports/
|   |-- cucumber-advanced-report.html
|   |-- cucumber-advanced-report.json
|   |-- cucumber-auth-dynamic-report.html
|   |-- cucumber-auth-dynamic-report.json
|   |-- cucumber-browser-ui-report.html
|   |-- cucumber-browser-ui-report.json
|   |-- cucumber-dom-window-report.html
|   |-- cucumber-dom-window-report.json
|   |-- cucumber-interaction-report.html
|   |-- cucumber-interaction-report.json
|   |-- cucumber-regression-report.html
|   |-- cucumber-regression-report.json
|   |-- cucumber-report.html
|   |-- cucumber-report.json
|   |-- cucumber-secure-dom-report.html
|   |-- cucumber-secure-dom-report.json
|   |-- cucumber-smoke-report.html
|   `-- cucumber-smoke-report.json
|-- test-data/
|   |-- advancedLinks.data.js
|   |-- authDynamicLinks.data.js
|   |-- browserUiLinks.data.js
|   |-- domWindowLinks.data.js
|   |-- herokuLinks.data.js
|   |-- interactionLinks.data.js
|   |-- navigationLinks.data.js
|   |-- sample-upload.txt
|   `-- secureDomLinks.data.js
|-- test-results/
|-- tests/
|   |-- PROJECT_STRUCTURE.md
|   `-- README.md
|-- .gitignore
|-- package-lock.json
|-- package.json
`-- playwright.config.js
```

## Notes

- `features/` contains the BDD scenarios.
- `features/step-definitions/` contains step implementations and hooks.
- `pages/` contains page object models.
- `test-data/` contains test inputs and reusable data files.
- `reports/` and `playwright-report/` contain generated execution reports.
- `tests/` currently stores project documentation.
