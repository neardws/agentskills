---
name: code-review
description: Multi-agent code review system for comprehensive code quality analysis. Covers security vulnerabilities, performance issues, code style, architecture, and accessibility. Use when reviewing PRs, analyzing code quality, or conducting security audits.
---

# Code Review Skill

A comprehensive code review system using multiple specialized analysis perspectives.

## Review Agents

| Agent | Focus Area |
|-------|------------|
| **Security Agent** | Vulnerabilities, injection flaws, auth issues, data exposure |
| **Performance Agent** | Bottlenecks, memory leaks, algorithmic complexity, caching |
| **Style Agent** | Naming conventions, formatting, code organization, comments |
| **Architecture Agent** | Design patterns, SOLID principles, coupling, cohesion |
| **Accessibility Agent** | WCAG compliance, screen reader support, keyboard navigation |

## Review Process

### 1. Initial Scan
- Identify changed files and their types
- Determine relevant review agents based on file types
- Check for obvious issues (syntax errors, merge conflicts)

### 2. Deep Analysis

#### Security Review
```
Check for:
- SQL/NoSQL injection vulnerabilities
- XSS (Cross-Site Scripting) risks
- Hardcoded secrets or credentials
- Insecure dependencies
- Authentication/authorization flaws
- Input validation issues
- Sensitive data exposure
```

#### Performance Review
```
Check for:
- N+1 query problems
- Unnecessary re-renders (React)
- Memory leaks
- Blocking operations in async code
- Missing indexes in database queries
- Inefficient algorithms (O(n²) when O(n) possible)
- Large bundle sizes
```

#### Style Review
```
Check for:
- Consistent naming (camelCase, snake_case, PascalCase)
- Function/method length (< 50 lines recommended)
- File organization and imports
- Comment quality and necessity
- Dead code and unused variables
- Magic numbers/strings
```

#### Architecture Review
```
Check for:
- Single Responsibility Principle violations
- Circular dependencies
- Tight coupling between modules
- Missing abstractions
- God classes/functions
- Proper error handling patterns
- Test coverage for critical paths
```

### 3. Report Generation

```markdown
# Code Review Report

## Summary
- **Files Reviewed:** X
- **Issues Found:** Y (Critical: A, Warning: B, Info: C)
- **Quality Score:** Z/100

## Critical Issues 🔴
[Must fix before merge]

## Warnings 🟡
[Should fix, but not blocking]

## Suggestions 🟢
[Nice to have improvements]

## Positive Highlights ✨
[Well-written code worth noting]
```

## Quality Gates

Automated checks that must pass:
- [ ] No critical security vulnerabilities
- [ ] No hardcoded secrets
- [ ] All tests pass
- [ ] Code coverage meets threshold
- [ ] No circular dependencies
- [ ] Linter passes with no errors

## Usage Examples

### Full Review
```
Review this PR for all quality aspects
```

### Security-Focused
```
Perform a security audit on these changes
```

### Performance Analysis
```
Analyze performance implications of this code
```

### Architecture Review
```
Review the architectural decisions in this module
```

## Best Practices for Reviewers

1. **Be Constructive** - Suggest improvements, not just problems
2. **Explain Why** - Don't just say "wrong", explain the reasoning
3. **Prioritize** - Focus on critical issues first
4. **Be Specific** - Point to exact lines and suggest fixes
5. **Acknowledge Good Code** - Positive feedback matters

## Integration with CI/CD

Can be integrated with GitHub Actions:
```yaml
- name: Code Review
  run: |
    # Fetch PR changes
    gh pr diff $PR_NUMBER > changes.diff
    # Run automated review
    # Post comments on PR
```
