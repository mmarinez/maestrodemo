# Maestro Cloud Setup for GitHub Actions

This document explains how to set up Maestro Cloud testing in GitHub Actions.

## Prerequisites

1. **Maestro Cloud Account**: Sign up at [console.mobile.dev](https://console.mobile.dev)
2. **API Key**: Get your API key from the Maestro Cloud console

## Setup Steps

### 1. Get Your Maestro Cloud Credentials

#### API Key:
1. Go to [console.mobile.dev](https://console.mobile.dev)
2. Sign in or create an account
3. Navigate to **Settings** → **API Keys**
4. Create a new API key or copy your existing key

#### Project ID:
1. In Maestro Cloud console, go to **Projects**
2. Select or create your project
3. Copy the **Project ID** (format: `proj_xxxxxxxxxxxxx`)
   - Found in project settings or URL

### 2. Add Credentials to GitHub Secrets

1. Go to your GitHub repository
2. Navigate to **Settings** → **Secrets and variables** → **Actions**
3. Add **two** repository secrets:

   **Secret 1:**
   - Click **New repository secret**
   - Name: `MAESTRO_CLOUD_API_KEY`
   - Value: Paste your Maestro Cloud API key
   - Click **Add secret**

   **Secret 2:**
   - Click **New repository secret**
   - Name: `MAESTRO_CLOUD_PROJECT_ID`
   - Value: Paste your Project ID (e.g., `proj_01example0example1example2`)
   - Click **Add secret**

### 3. Workflow Configuration

The workflow is already configured in `.github/workflows/maestro-tests.yml`:

```yaml
- name: Run Maestro Cloud Tests for iOS
  uses: mobile-dev-inc/action-maestro-cloud@v1
  with:
    api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
    project-id: ${{ secrets.MAESTRO_CLOUD_PROJECT_ID }}
    app-file: Wikipedia.app
    workspace: .maestro
    include-tags: ios
```

## How It Works

### When Tests Run:
1. GitHub Actions triggers on push/PR to main or develop branches
2. Workflow checks out your code
3. Sets up Java 17 (required for Maestro)
4. **Maestro Cloud Action**:
   - Uploads `Wikipedia.app` to Maestro Cloud
   - Uploads test flows from `.maestro/` directory
   - Runs tests on real iOS devices in the cloud
   - Captures screenshots and videos automatically
   - Returns pass/fail results

### Benefits of Maestro Cloud:
- ✅ **No simulator management** - runs on real devices
- ✅ **Faster execution** - optimized cloud infrastructure
- ✅ **Automatic screenshots** - captured for every test step
- ✅ **Video recordings** - full test execution videos
- ✅ **Parallel execution** - run multiple tests simultaneously
- ✅ **Real device testing** - more accurate than simulators
- ✅ **Cost effective** - no need for macOS runners

## Viewing Results

### In GitHub:
- Check the Actions tab for test status
- View logs in the workflow run

### In Maestro Cloud Console:
- Go to [console.mobile.dev](https://console.mobile.dev)
- View detailed test reports
- See screenshots and videos
- Analyze test failures
- Download artifacts

## Configuration Options

You can customize the workflow by uncommenting and modifying these parameters:

```yaml
with:
  api-key: ${{ secrets.MAESTRO_CLOUD_API_KEY }}
  app-file: Wikipedia.app
  workspace: .maestro
  include-tags: ios

  # Optional:
  device-locale: en_US        # Set device locale
  ios-version: 18             # Specify iOS version
  name: Wikipedia iOS Tests   # Custom test run name
  async: false                # Wait for results (default)
  env: |                      # Environment variables
    USERNAME=test_user
    PASSWORD=test_pass
```

## Troubleshooting

### "API Key not found" Error
- Verify the secret is named exactly: `MAESTRO_CLOUD_API_KEY`
- Check that the secret is set in the correct repository
- Ensure the API key is still valid in Maestro Cloud console

### "App file not found" Error
- Verify `Wikipedia.app` exists in your repository
- Check the path is correct relative to repository root
- Ensure the app is committed to the repository

### Tests Not Running
- Check that test flows have the `ios` tag
- Verify test flows are in `.maestro/` directory
- Review Maestro Cloud console for detailed error messages

## Local Testing vs Cloud Testing

### Local (using Maestro CLI):
```bash
maestro test .maestro/ios/
```
- Runs on your local simulator
- Screenshots saved to `screenshots/` directory
- Instant feedback during development

### Cloud (GitHub Actions):
```bash
# Automatically triggered on push/PR
```
- Runs on real devices in the cloud
- Screenshots available in Maestro Cloud console
- CI/CD integration for automated testing

## Cost Considerations

- Check [Maestro Cloud pricing](https://www.mobile.dev/pricing) for your usage
- Free tier available for small projects
- Pay-as-you-go for larger test suites

## Next Steps

1. ✅ Add `MAESTRO_CLOUD_API_KEY` to GitHub secrets
2. ✅ Add `MAESTRO_CLOUD_PROJECT_ID` to GitHub secrets
3. ✅ Push code to trigger workflow
4. ✅ Check GitHub Actions for results
5. ✅ View detailed reports in Maestro Cloud console

---
*Last updated: December 8, 2025*