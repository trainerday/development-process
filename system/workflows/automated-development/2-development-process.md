---
title: development-process
type: note
permalink: claude-code-os/system/workflows/automated-development/development-process
---

# Development Process

IMPORTANT: Review the current express JS structure of this project so you follow the same   pattern when creating new pages  

## Development Process
# Development Process (For Claude Code)

## Implementation Phase Instructions

### Step 1: Code Structure Analysis
**IMPORTANT**: Review the current project structure to follow the same patterns when creating new features.

1. **Analyze existing codebase**:
   - Framework patterns (Express.js, React, etc.)
   - File organization and naming conventions
   - CSS/styling approach used
   - JavaScript patterns and modules
   - Routing structure

2. **Follow established patterns**:
   - Use same file structure for new features
   - Match existing CSS class naming
   - Follow same variable naming conventions
   - Use consistent error handling patterns

### Step 2: Implementation Requirements

**Code Quality Standards**:
- Follow existing project's coding style
- Maintain consistent indentation and formatting
- Use meaningful variable and function names
- Add comments for complex logic
- Ensure responsive design compatibility

**Implementation Checklist**:
- [ ] Review approved specification thoroughly
- [ ] Analyze existing similar features in codebase
- [ ] Create new files following project structure
- [ ] Implement core functionality
- [ ] Add proper error handling
- [ ] Ensure mobile responsiveness
- [ ] Test basic functionality manually
- [ ] Update any necessary documentation

### Step 3: Visual Standards Compliance

**Required Elements** (see visual-standards-template.md):
- TrainerDay logo placement
- Poppins font family usage
- Consistent form element heights
- Proper spacing and alignment
- Professional appearance

**Form Element Requirements**:
- All input boxes same height
- All dropdown/select boxes same height as inputs
- Consistent label alignment
- Proper grid layout and spacing

### Step 4: Pre-Testing Validation

Before moving to testing phase:
- [ ] Code compiles without errors
- [ ] No console errors in browser
- [ ] Basic functionality works as specified
- [ ] Visual appearance matches standards
- [ ] Responsive design functions on mobile

### Step 5: Update Task Status

When implementation is complete:
```markdown
## [Task Name]
- [x] Spec generation COMPLETED
- [x] Implementation COMPLETED
- [ ] **Local testing approval PENDING** ← Current step
```

### Integration Notes

**API Integration**: Follow existing API patterns in the project
**Database**: Use existing database connection and query patterns  
**Routing**: Add new routes following established URL structure
**CSS**: Extend existing stylesheets rather than creating new ones