# Claude Configuration for Maestro Testing

This directory contains project-specific conventions and preferences for Claude Code to follow when working with Maestro mobile automation tests.

## Directory Structure

```
.claude/
├── README.md                 # This file
├── maestro-testing.md        # Testing conventions and best practices
├── report-template.md        # HTML report structure and styling
└── commands/                 # Custom slash commands
    ├── run-ios-tests.md      # Run iOS tests with report generation
    └── add-screenshots.md    # Add screenshots to test flows
```

## Configuration Files

### maestro-testing.md
Defines testing standards including:
- Device selection preferences
- Screenshot capture strategy
- Test organization and naming conventions
- Element selection best practices
- Error handling guidelines

### report-template.md
Defines HTML report requirements:
- Report structure and sections
- Styling guidelines (colors, typography, layout)
- Screenshot embedding method
- Responsive design rules
- Description templates

## Custom Slash Commands

### /run-ios-tests
Executes the complete iOS test suite:
- Starts device if needed
- Runs all test flows with screenshots
- Generates HTML report
- Follows all conventions from config files

Usage:
```
/run-ios-tests
```

### /add-screenshots
Adds screenshot commands to a test flow:
- Analyzes test flow structure
- Suggests screenshot locations
- Follows naming conventions
- Previews changes before applying

Usage:
```
/add-screenshots
```

## How It Works

When you work with Claude Code on this project:

1. **Automatic Reading**: Claude reads these configuration files to understand your preferences
2. **Convention Following**: All testing and reporting follows the defined standards
3. **Consistency**: Every test run and report generation uses the same structure
4. **Customization**: You can edit these files to change how Claude works

## Customizing

### To Change Testing Conventions
Edit `.claude/maestro-testing.md` to update:
- Screenshot naming patterns
- Device preferences
- Test organization rules

### To Change Report Style
Edit `.claude/report-template.md` to update:
- Colors and branding
- Report sections
- Screenshot descriptions
- Layout preferences

### To Add Custom Commands
Create new `.md` files in `.claude/commands/`:
1. Add YAML frontmatter with description
2. Write step-by-step instructions
3. Reference other config files as needed

## Benefits

- **Consistency**: Same report format every time
- **Efficiency**: No need to repeat preferences
- **Customization**: Easy to modify standards
- **Team Alignment**: Share conventions across team
- **Documentation**: Self-documenting project standards

## Examples

### Request a Test Run
```
"Run the iOS tests and generate a report"
```
Claude will automatically:
- Read conventions from maestro-testing.md
- Run tests with screenshots
- Generate report following report-template.md
- Use configured colors and styling

### Modify a Test Flow
```
"Add screenshots to loginTests.yml"
```
Claude will:
- Read screenshot conventions
- Add appropriately named screenshots
- Follow the defined placement rules

## Maintenance

**Review these files when:**
- Starting a new test suite
- Onboarding new team members
- Changing project requirements
- Updating branding/styling

**Best Practice**: Keep these files in version control so the entire team shares the same conventions.

---
*Created: December 8, 2025*