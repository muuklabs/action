# MuukTest E2E Integration for GitHub Actions

Integrate MuukTest's E2E testing capabilities into your GitHub Actions workflows. This action automatically downloads your test scripts and configuration files from the MuukTest portal, sets up Playwright with all required dependencies, and executes your E2E tests.

## Features

- 🔐 Secure authentication with MuukTest portal using your API key
- 🎯 Execute tests by tag or hashtag for flexible test selection
- 🌐 Override base URL for testing different environments
- ⚡ Configurable parallel workers for optimal test execution
- 📊 Automatic test result reporting to MuukTest portal
- 🔧 Zero-configuration Playwright setup with all dependencies

## Prerequisites

- A MuukTest account with test scripts configured
- API key (`key.pub`) downloaded from your MuukTest portal Account tab
- Tests tagged appropriately for CI/CD execution

## Usage

Add the MuukTest action to your GitHub Actions workflow:

```yaml
name: E2E Tests

on: [pull_request, push]

jobs:
  muuktest-e2e:
    runs-on: ubuntu-latest
    name: Run MuukTest E2E Tests
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
        
      - name: Execute MuukTest E2E tests
        uses: muuklabs/action@v1
        with:
          muuk-key: ${{ secrets.MUUKTEST_KEY }}
          tag-property: ${{ vars.TAG_PROPERTY }}
          tag-value: ${{ vars.TAG_VALUE }}
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `muuk-key` | ✅ Yes | - | Your MuukTest API key from `key.pub` file. Download from the Account tab in MuukTest Portal. **Store this as a secret!** |
| `tag-property` | ✅ Yes | - | Test selection mode: `tag` (single test) or `hashtag` (multiple tests by hashtag) |
| `tag-value` | ✅ Yes | - | The tag or hashtag value to filter tests (e.g., `mytest` or `#cicd`) |
| `base-url` | ❌ No | - | Override the base URL for test execution. If not provided, tests use their configured base URL from MuukTest portal |
| `workers` | ❌ No | `3` | Number of parallel workers for Playwright test execution |

## Examples

### Basic Usage with Secrets and Variables

```yaml
- name: Run E2E tests
  uses: muuklabs/action@v1
  with:
    muuk-key: ${{ secrets.MUUKTEST_KEY }}
    tag-property: ${{ vars.TAG_PROPERTY }}
    tag-value: ${{ vars.TAG_VALUE }}
```

### Run Tests Against Staging Environment

```yaml
- name: Run E2E tests on staging
  uses: muuklabs/action@v1
  with:
    muuk-key: ${{ secrets.MUUKTEST_KEY }}
    tag-property: 'hashtag'
    tag-value: '#smoke'
    base-url: 'https://staging.example.com'
```

### Run Tests with Custom Worker Count

```yaml
- name: Run E2E tests with 5 parallel workers
  uses: muuklabs/action@v1
  with:
    muuk-key: ${{ secrets.MUUKTEST_KEY }}
    tag-property: 'hashtag'
    tag-value: '#regression'
    workers: '5'
```

### Complete Example with All Parameters

```yaml
- name: Run E2E tests with all options
  uses: muuklabs/action@v1
  with:
    muuk-key: ${{ secrets.MUUKTEST_KEY }}
    tag-property: 'hashtag'
    tag-value: '#cicd'
    base-url: 'https://qa.example.com'
    workers: '4'
```

## Setting Up Secrets and Variables

### Required Secret

In your GitHub repository, go to **Settings → Secrets and variables → Actions** and create:

- `MUUKTEST_KEY`: Your MuukTest API key content from the `key.pub` file

### Optional Variables

You can also set repository variables for convenience:

- `TAG_PROPERTY`: Default tag property (e.g., `hashtag`)
- `TAG_VALUE`: Default tag value (e.g., `#cicd`)

## How It Works

1. **Authentication**: Connects to MuukTest portal using your API key
2. **Download**: Retrieves test scripts and configuration files
3. **Setup**: Installs Node.js, Playwright, and all required dependencies
4. **Execute**: Runs your E2E tests with the specified parallel workers
5. **Report**: Automatically sends test results back to MuukTest portal

## Support

For more information about MuukTest or to report issues:
- 📖 [MuukTest Documentation](https://www.muuktest.com)
- 🐛 [Report an Issue](https://github.com/muuklabs/action/issues)
- 📧 Contact MuukTest support

## License

See [LICENSE](LICENSE) file for details.
