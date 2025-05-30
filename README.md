# Secure Workflow Configuration Fix

## Vulnerability Description
Found a workflow that triggers on `pull_request_target` without scoping the default GITHUB_TOKEN. The workflow `insecure.yml` in .github/workflows uses `pull_request_target` and lacks a `permissions:` block, leaving the token at its default (write) privileges.

## Severity
High

## Fix
The fix adds explicit permissions to the workflow file to limit the token scope to only what is necessary. This follows the principle of least privilege and helps prevent potential security issues.

### Changes Made
- Added a `permissions:` block to limit token scope
- Set `contents: read` as the default permission
- Added comments explaining how to add only necessary permissions

## Why This Matters
Workflows that trigger on `pull_request_target` run with repository write permissions by default. This can be dangerous because the workflow runs in the context of the base repository but can be triggered by a fork, potentially allowing malicious code execution with write access to your repository.
