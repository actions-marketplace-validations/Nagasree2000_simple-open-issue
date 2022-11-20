# Create a JavaScript Action

<p align="center">
  <a href="https://github.com/actions/javascript-action/actions"><img alt="javscript-action status" src="https://github.com/actions/javascript-action/workflows/units-test/badge.svg"></a>
</p>

Use this template to bootstrap the creation of a JavaScript action.:for creating a issue

This template includes tests, linting, a validation workflow, publishing, and versioning guidance.



## Create an action from this template

U can use this template for creation of new issue in your github repositories and also for creation of relevant java script files.

## Code in Main

Install the dependencies

```bash
npm install
```

Run the tests :heavy_check_mark:

```bash
$ npm test

 PASS  ./index.test.js
  ✓ throws invalid number (3ms)
  ✓ wait 500 ms (504ms)
  ✓ test runs (95ms)
...
```

## Change action.yml

The action.yml defines the inputs and output for your action.

Update the action.yml with 

`token: which is used for authentication purpose
`
`title: which is used as a title for your issue creation
`
`body: which is used as a body for your issue creation
`
`assignees: Are the persons you want to assign to your issue
`

See the [documentation](https://help.github.com/en/articles/metadata-syntax-for-github-actions)

## Change the Code

Most toolkit and CI/CD operations involve async operations so the action is run in an async function.

```javascript
const core = require("@actions/core");
const github = require("@actions/github");
const { Octokit } = require("@octokit/rest");
...

async function run() {
  try {
      ...
  }
  catch (error) {
    core.setFailed(error.message);
  }
}

run()
```

See the [toolkit documentation](https://github.com/actions/toolkit/blob/master/README.md#packages) for the various packages.

## Package for distribution

GitHub Actions will run the entry point from the action.yml. Packaging assembles the code into one file that can be checked in to Git, enabling fast and reliable execution and preventing the need to check in node_modules.

Actions are run from GitHub repos.  Packaging the action will create a packaged action in the dist folder.

Run prepare

```bash
npm run prepare
```

Since the packaged index.js is run from the dist folder.

```bash
git add dist
```

## Create a release branch

Users shouldn't consume the action from master since that would be latest code and actions can break compatibility between major versions.

Checkin to the v1 release branch

```bash
git checkout -b v1
git commit -a -m "v1 release"
```

```bash
git push origin v1
```

Note: We recommend using the `--license` option for ncc, which will create a license file for all of the production node modules used in your project.

Your action is now published! :rocket:

See the [versioning documentation](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)

## Usage

You can now consume the action by referencing the v1 branch

```yaml
uses: Nagasree2000/Open-Issue@v1
with:
  token: {{ secrets.GITHUB_TOKEN }}
  title: Issue creation
  body: Body of issue
  assignees: |
    Nagasree2000
    Nagasree1976
```

## Output
```yaml
uses: Nagasree2000/actions/simple-issue@v1
outputs:
  issue: # id of output
    description: "The issue description"
```



See the [actions tab](https://github.com/actions/javascript-action/actions) for runs of this action! :rocket:
