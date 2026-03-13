## Plan: Add Poutine Security Scanning Workflow

Add a GitHub Actions workflow that uses the boostsecurityio/poutine-action to scan this repository's GitHub Actions workflows for security vulnerabilities.

**Steps**
1. Create new workflow file at `.github/workflows/poutine-scan.yml`
2. Configure workflow to run on push and pull_request to main branch
3. Add job that checks out repository and runs poutine action
4. Configure poutine action to scan for vulnerabilities in CI/CD pipelines
5. Optionally upload SARIF results to GitHub code scanning
6. Set appropriate permissions for the job (contents: read, security-events: write)

**Relevant files**
- `.github/workflows/poutine-scan.yml` — New workflow file to create
- `.github/workflows/testCSV.yml` — Existing workflow for reference
- `action.yml` — Current action metadata (to understand existing inputs/outputs)

**Verification**
1. Verify new workflow file is created with correct syntax
2. Check that workflow runs successfully on push/pull_request
3. Confirm poutine action completes and produces SARIF output
4. Validate that any security findings are properly reported
5. Ensure workflow doesn't interfere with existing testCSV workflow

**Decisions**
- Use tagged version of poutine-action (v1.0.8) rather than @main for stability
- Include SARIF upload step to integrate with GitHub code scanning
- Run on push and pull_request to main branch for continuous security monitoring
- Keep existing Dependabot export action unchanged; add poutine as separate workflow

**Further Considerations**
1. Should we add workflow_dispatch trigger for manual scanning? / Recommended: Yes for flexibility
2. Should we configure poutine to fail on violations? / Recommended: No initially, to avoid breaking existing workflows
3. Should we add schedule trigger for weekly scans? / Recommended: Yes for ongoing monitoring