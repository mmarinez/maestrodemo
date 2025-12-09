---
description: Add screenshot commands to a Maestro test flow
---

Add screenshot capture commands to a Maestro test flow following these steps:

1. Ask the user which test flow file to modify
2. Read the test flow file
3. Read the screenshot conventions from `.claude/maestro-testing.md`
4. Analyze the test flow and identify key points where screenshots should be captured:
   - After app launch
   - After major navigation
   - Before/after critical interactions
   - At assertion points
5. Add `takeScreenshot` commands with descriptive names following the naming convention:
   - Format: `{step_number}_{action_description}.png`
   - Examples: `01_app_launched.png`, `02_login_screen.png`
6. Show the user a diff of the changes
7. Ask for confirmation before saving