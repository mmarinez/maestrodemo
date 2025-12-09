# Maestro Testing Conventions

This file defines the testing standards and conventions for Maestro mobile automation in this project.

## Test Execution Rules

### Device Selection
- **iOS Testing**: Use iPhone 16 Pro simulator (iOS 18.6) by default
- **Android Testing**: Use any available Android emulator
- Always verify device is running before executing tests
- Device ID: `135E61FE-60B9-4863-909C-EEF459DCDF9B` (iPhone 16 Pro)

### Test Flow Structure
- Always use `clearState` before launching app for consistent test results
- Load element definitions using `runFlow: loadElements.yml` pattern
- Group related tests in separate YAML files under `.maestro/ios/` or `.maestro/android/`

### Screenshot Strategy
**When to capture screenshots:**
- After app launch
- After each major navigation step
- Before and after critical interactions
- At assertion points
- After completing each test flow

**Storage Location:**
All screenshots must be stored in the `screenshots/` directory

**Naming Convention:**
```
screenshots/{step_number}_{action_description}.png

Examples:
- screenshots/01_app_launched.png
- screenshots/02_onboarding_start.png
- screenshots/03_login_success.png
- screenshots/04_home_screen.png
```

**Screenshot Placement in Flows:**
```yaml
- launchApp
- takeScreenshot: "screenshots/01_app_launched.png"
- tapOn: "Login Button"
- takeScreenshot: "screenshots/02_after_login_tap.png"
```

## Test Organization

### Directory Structure
```
.maestro/
├── ios/
│   ├── {feature}Tests.yml    # Main test flows
│   └── loadElements.yml       # Screen element definitions
├── android/
│   └── {feature}Tests.yml
└── screens/
    ├── {screen}.js            # JavaScript element selectors
    └── ...
```

### Test File Naming
- Use descriptive names: `wikipediaTests.yml`, `searchTests.yml`, `loginTests.yml`
- Suffix with `Tests.yml` for test flows
- Use camelCase for flow names

### Tags
Always include appropriate tags in test flows:
```yaml
appId: org.wikimedia.wikipedia
tags:
  - ios
  - passing
  - smoke      # Quick validation tests
  - regression # Full test coverage
  - [feature]  # Feature-specific tag
```

## Best Practices

### Element Selection
- Prefer ID selectors over text when possible
- Use variables from `loadElements.yml` for reusable selectors
- Example: `${output.onboarding.nextButton}` instead of hardcoded text

### Waits and Timing
- Use `extendedWaitUntil` for dynamic content
- Avoid hardcoded delays unless necessary
- Let Maestro's auto-wait handle most timing issues

### Assertions
- Add assertions at key checkpoints
- Use `assertVisible` to verify expected elements
- Use `assertNotVisible` for negative checks

### Test Data
- Store test credentials in environment variables
- Use `env` section in YAML for configuration
```yaml
env:
  TEST_USERNAME: "test_user"
  TEST_PASSWORD: "test_pass"
```

## Reporting Requirements

When running tests:
1. Capture all screenshots during execution
2. Generate comprehensive HTML report
3. Include test metrics (commands executed, pass/fail rate)
4. Embed device information
5. Add descriptive text for each screenshot

## Error Handling

- Mark optional steps with `optional: true`
- Use `when` conditions for platform-specific logic
- Always capture screenshot on failure for debugging

## CI/CD Integration

### GitHub Actions
Tests are automatically run on every push and pull request via GitHub Actions.

**Workflow file:** `.github/workflows/maestro-tests.yml`

**What it does:**
- Boots iOS simulator on macOS runner
- Installs Maestro CLI
- Runs all iOS tests with JUnit output
- Stores screenshots in `screenshots/` directory
- Uploads test results and screenshots as artifacts
- Publishes test results to PR comments

**Manual trigger:**
Go to Actions tab in GitHub → Select "Maestro iOS Tests" → Click "Run workflow"

**Artifacts:**
- `test-results`: JUnit XML report
- `test-screenshots`: All captured screenshots
- `test-report`: HTML report (if generated)

### Running Tests Locally vs CI
- **Local**: Screenshots saved to `screenshots/` directory
- **CI**: Screenshots uploaded as GitHub Actions artifacts
- Both follow the same naming conventions and structure

## Code Review Checklist

Before committing test changes:
- [ ] All screenshots saved to `screenshots/` directory
- [ ] All screenshots have descriptive names
- [ ] Tests run successfully on target device
- [ ] Element selectors are properly defined
- [ ] Tags are accurate and up-to-date
- [ ] No hardcoded waits (use `extendedWaitUntil`)
- [ ] Comments explain complex logic
- [ ] Test data is externalized
- [ ] GitHub Actions workflow runs successfully

---
*Last updated: December 8, 2025*