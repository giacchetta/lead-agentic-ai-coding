# GitHub Action Template: [ACTION_NAME]

This template provides guidance for creating a GitHub Action using TypeScript based on the [actions/typescript-action](https://github.com/actions/typescript-action) repository.

## 1. Action Purpose

*Describe the purpose of this GitHub Action - what problem it solves and what automation it provides.*

**Example:** "This action automates the process of analyzing JavaScript dependencies for security vulnerabilities and licensing issues. It runs on pull requests and provides inline comments for identified problems."

## 2. Action Inputs

*List the inputs that the action will accept. Use the format below for each input.*

| Input Name | Required | Default | Description |
|:-----------|:---------|:--------|:------------|
| `token` | Yes | N/A | GitHub token used for authentication |
| `directory` | No | `.` | The directory containing the files to analyze |
| `fail-on-error` | No | `true` | Whether to fail the workflow if issues are found |

## 3. Action Outputs

*List the outputs that the action will produce. Use the format below for each output.*

| Output Name | Description |
|:------------|:------------|
| `issue-count` | The number of issues found |
| `summary-report` | A Markdown-formatted summary of the analysis |

## 4. Core Implementation

*Describe the core functionality that needs to be implemented in the `src/` directory.*

The action should perform the following tasks:
1. Parse and validate input parameters
2. Set up the necessary environment
3. Execute the core functionality (e.g., running a scan, processing files)
4. Format and output the results
5. Set appropriate exit status based on findings and configuration

## 5. Implementation Details

### File Structure

```
├── action.yml               # Action metadata file
├── package.json             # Node.js package configuration
├── tsconfig.json            # TypeScript configuration
├── jest.config.js           # Test configuration
├── .github/workflows/       # CI workflows for testing the action
│   └── test.yml
├── src/                     # Source code
│   ├── main.ts              # Entry point
│   ├── utils/               # Utility functions
│   └── types/               # TypeScript type definitions
└── __tests__/               # Test files
    └── main.test.ts
```

### Key Files to Implement

1. **action.yml**
   - Define the action name, description, inputs, outputs, and entry point.
   - Reference the compiled JavaScript file in the `dist` directory.

2. **src/main.ts**
   - Main entry point for the action.
   - Get input parameters using `core.getInput()`.
   - Implement error handling with try/catch blocks.
   - Set outputs using `core.setOutput()`.
   - Set failure status when needed using `core.setFailed()`.

3. **src/utils/**
   - Implement helper functions for the core functionality.
   - Keep functions small, focused, and testable.

4. **__tests__/**
   - Implement unit tests for all functionality.
   - Mock external services and GitHub API calls.

## 6. Development Workflow

1. **Setup Development Environment**
   ```bash
   # Clone the repository (if starting from actions/typescript-action)
   git clone https://github.com/actions/typescript-action.git my-action
   cd my-action
   
   # Install dependencies
   npm install
   ```

2. **Implement the Action**
   - Update `action.yml` with your action's metadata
   - Implement the functionality in `src/main.ts` and supporting files
   - Add tests in `__tests__/`

3. **Test Locally**
   ```bash
   # Run tests
   npm test
   
   # Build the action
   npm run build
   
   # Package for distribution
   npm run package
   ```

4. **Test in a Workflow**
   - Create a test workflow in `.github/workflows/test.yml`
   - Reference your action with `uses: ./`
   - Test with different input combinations

5. **Release Process**
   - Create a release branch: `git checkout -b releases/v1`
   - Build and commit the compiled code: `npm run all`
   - Push to GitHub: `git push -u origin releases/v1`
   - Create a tag: `git tag -a v1 -m "First major release"`
   - Push the tag: `git push origin v1`

## 7. Action Versioning

Follow semantic versioning for releases:
- `v1.0.0` - First stable release
- `v1.0.1` - Bug fixes
- `v1.1.0` - New features (backward compatible)
- `v2.0.0` - Breaking changes

Create and maintain major version tags (e.g., `v1`, `v2`) that point to the latest version within that major version.

## 8. Best Practices

- **Security**: Never hardcode tokens or credentials.
- **Error Handling**: Properly handle all errors and provide meaningful messages.
- **Logging**: Use `core.debug()`, `core.info()`, `core.warning()`, and `core.error()` appropriately.
- **Input Validation**: Always validate input parameters before using them.
- **Idempotency**: Ensure the action can be run multiple times with the same result.
- **Minimal Dependencies**: Keep external dependencies to a minimum.
- **Documentation**: Document all inputs, outputs, and usage examples in the README.

## 9. Example Usage

```yaml
name: Example Workflow

on:
  pull_request:
    branches: [ main ]

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Run Your Action
        id: your-action
        uses: owner/action-name@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          directory: './src'
          
      - name: Print Output
        run: echo "Found ${{ steps.your-action.outputs.issue-count }} issues"
```

## 10. Implementation Checklist

- [ ] Updated `action.yml` with correct metadata
- [ ] Implemented core functionality in `src/main.ts`
- [ ] Added utility functions as needed
- [ ] Written tests for all code paths
- [ ] Tested the action locally
- [ ] Verified the action works in a workflow
- [ ] Created proper release versioning
- [ ] Updated documentation with examples
