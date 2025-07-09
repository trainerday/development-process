---
title: Upload Zwift ZWO with decimal values fails
type: note
permalink: product-development/os-projects/td-web/backlogs/upload-zwift-zwo-with-decimal-values-fails
tags:
- '["bug"'
- '"zwift"'
- '"import"'
- '"later"'
- '"backlog"]'
---

# Upload Zwift ZWO with decimal values fails

## Status
- **Priority**: Later
- **Type**: Bug
- **Labels**: Bug, Import
- **Created**: 2025-01-03
- **Updated**: 2025-01-03

## Description
Uploading Zwift ZWO files that contain decimal values fails during the import process.

## Details
- ZWO files with decimal power values cause upload failure
- Zwift workout files (.zwo) use XML format
- Issue specifically occurs when power values have decimals

## Technical Notes
- Review ZWO file parser implementation
- Check decimal value handling in power calculations
- Verify XML parsing for numeric values
- Test with various decimal formats (e.g., 250.5, 250.0, 250.75)
- Consider locale-specific decimal separators

## Acceptance Criteria
- [ ] ZWO files with decimal power values upload successfully
- [ ] Decimal values are correctly parsed and stored
- [ ] No loss of precision in power values
- [ ] Error handling provides clear feedback if issues occur
- [ ] Unit tests cover decimal value scenarios
- [ ] Works with both comma and dot decimal separators

## Resources
- Zwift ZWO file format specification
- Sample ZWO files with decimal values for testing

## Notes
- Common issue with XML number parsing
- May affect other numeric fields beyond power
- Consider backwards compatibility with existing uploads