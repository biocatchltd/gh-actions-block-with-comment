# block-with-comment
a github action to add a comment if a test fails, blocking a PR, or remove it if it succeeds.

## Example
An example workflow that uses this action to check for new tags and release a new version if it is new:
```yaml
name: test pr
on:
  pull_request:
    types: [opened, reopened, edited, synchronize]
    branches:
      - main

jobs:
    do-test:
        name: check that the pr's name begins with "test"
        runs-on: ubuntu-latest

        steps:
            - name: checkout
              uses: actions/checkout@v2

            - name: block with comment
              uses: biocatchltd/gh-actions-block-with-comment@v1
              with:
                  comment: "This PR's name must begin with 'test'"
                  test: ${{ startsWith(github.event.pull_request.title, 'test') }}
```

## inputs
* `test`: The test to perform, eill only pass if the test is `'true'`
* `fail_message`: The message to post if the test fails
* `comment_tag`: The tag to use to identify the comment

## Note
this action will fail if the test is not `'true'`, and no further steps will be executed.