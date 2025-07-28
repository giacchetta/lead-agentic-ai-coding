# GitHub Action Specification: [ACTION_NAME]

## 1. Action Goal
*Define the primary goal of this GitHub Action in a single, clear statement. What specific task will it automate?*

**Example:** "This action will scan a repository's `package.json` file, identify dependencies with known security vulnerabilities using the `npm audit` command, and fail the workflow if vulnerabilities of a specified severity are found."

## 2. Key Technologies & Libraries
*Specify the core Node.js libraries the action will use.*
- **GitHub Toolkit:** `@actions/core`, `@actions/github`
- **HTTP Client (if needed):** `axios`, `node-fetch`
- **Other:** `fs`, `child_process`

## 3. Action Inputs
*Define the inputs for the `action.yml` file.*

| Input Name      | Description                                     | Required | Default |
|:----------------|:------------------------------------------------|:---------|:--------|
| `github-token`  | The GITHUB_TOKEN secret for API calls.          | Yes      | N/A     |
| `fail-severity` | The minimum vulnerability level to fail on.     | No       | `high`  |
|                 | (Options: `low`, `moderate`, `high`, `critical`) |          |         |

## 4. Action Outputs
*Define the outputs for the `action.yml` file.*

| Output Name     | Description                                       |
|:----------------|:--------------------------------------------------|
| `vuln-count`    | The total number of vulnerabilities found.        |
| `summary-json`  | A JSON string summarizing the audit findings.     |

## 5. Core Logic (`src/main.ts`)
*Implement the following logic flow step-by-step inside an async `run()` function.*

1.  **Get Inputs:**
    -   Retrieve `github-token` and `fail-severity` using `core.getInput()`.
    -   Instantiate the octokit client using the `github-token`.
2.  **Input Validation:**
    -   Check if `fail-severity` is one of the valid options. If not, `core.setFailed()` with an error message and exit.
3.  **Execute Scan:**
    -   Use `child_process.exec` to run the command `npm audit --json`. This command outputs a JSON object.
    -   Handle potential errors during command execution (e.g., if it's not a Node.js project).
4.  **Process Results:**
    -   Parse the JSON output from the `npm audit` command.
    -   Count the total number of vulnerabilities found.
    -   Determine if any vulnerabilities meet or exceed the `fail-severity` threshold.
5.  **Set Outputs & Conclusion:**
    -   Set the `vuln-count` output using `core.setOutput()`.
    -   Set the `summary-json` output with the parsed audit data.
    -   If the `fail-severity` threshold was met, call `core.setFailed()` with a summary message.
    -   If the threshold was not met, log a success message using `core.info()`.
6.  **Error Handling:**
    -   The entire `run()` function must be wrapped in a `try/catch` block. If any error occurs, call `core.setFailed(error.message)`.

## 6. Generate `action.yml`
*Based on the name, description, inputs, and outputs defined above, generate the complete `action.yml` file.*

-   `name`: `[ACTION_NAME]`
-   `description`: `[From Section 1]`
-   `inputs`: `[From Section 3]`
-   `outputs`: `[From Section 4]`
-   `runs`:
    -   `using`: `node20`
    -   `main`: `dist/index.js`

## 7. Final AI Self-Correction Checklist
*Before providing the final code, answer these questions about your generated output:*

- [ ] Does the `action.yml` file perfectly match the inputs and outputs defined in sections 3 and 4?
- [ ] Is every step from the "Core Logic" section (Section 5) implemented in `src/main.ts`?
- [ ] Is all code wrapped in a `try/catch` block to handle unexpected errors?
- [ ] Are all external libraries (`@actions/core`, etc.) properly imported?
- [ ] Are the outputs set using `core.setOutput()` exactly as named in Section 4?