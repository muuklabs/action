# Muuktest integration with Github Action

This action connects to ***MuukTest*** executor for Playwright using your *key.pub*. Use this action to run E2E by tag propertyy and value on. More details about workflow see [GitHub Actions](https://docs.github.com/en/actions).


## How to use

Add the Muuk action *muuklabs/action@v1.0.3* with required input parameters as part of your yaml configuration on your CI/CD pipeline or create a new yaml configuration as suggested below:

```
on: [pull_request]

jobs:
  muuktest-e2e-tests:
    runs-on: ubuntu-latest
    name: Execute MuukTest E2E.
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Retrieve and execute MuukTest E2E
        uses: muuklabs/action@v1.0.2
        with:
          muuk-key: ${{ secrets.MUUKTEST_TOKEN }}
          tag-property: ${{ vars.TAG_PROPERTY }}
          tag-value: ${{ vars.TAG_VALUE }}
          base-url: (Optional)
```

**Inputs**
```
muuk-key: Key value taken from key.pub file. Download this from Account tab in MuukTest Portal.
tag-property: [tag/hashtag] Choose for either a single test 'tag' or a set of tests by 'hashtag'.
tag-value: Value for property '#cicd'
base-url: (Optional) URL to execute the E2E tests against. If not provided, tests are executed on their on base URL defined for each test on MuukTest portal. Set any public or local environment available for this CICD script.
```

You could either set inputs by using variables as shown in 'How to use' section or set literals (or combination of both) as shown in the example:

***Example*** 
```
        muuk-key: 'pbyhz1qmmar69yxnbaa72---'
        tag-property: 'hashtag'
        tag-value: '#cicd'
        base-url: 'https://mycicd-public-local-domain'
```
