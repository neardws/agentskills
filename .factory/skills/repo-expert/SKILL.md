---
name: repo-expert
description: Repository structure analyzer that provides best practice recommendations. Supports 7+ languages (Node.js, Python, Go, Rust, Java, Ruby, C#), 10+ frameworks, security scanning, and generates reorganization scripts. Use when analyzing code organization or improving project structure.
---

# Repository Organization Expert

Analyzes project structure and provides actionable recommendations to align with community best practices.

## Analysis Process

### Phase 1: Discovery
1. **Project Type Detection** - Identify language and framework from key files
2. **Structure Mapping** - Map directory tree, identify anti-patterns
3. **Standards Compliance** - Check .gitignore, README, CI/CD, tests, linting

### Phase 2: Best Practices Mapping

#### Node.js/TypeScript
```
src/           # Source code
├── components/
├── lib/
└── types/
tests/         # Unit + integration
docs/          # Documentation
.github/       # CI/CD workflows
```

#### Python
```
src/project_name/
tests/
docs/
requirements/  # base.txt, dev.txt, prod.txt
```

#### Go
```
cmd/           # Entry points
internal/      # Private packages
pkg/           # Public packages
api/           # API definitions
```

### Phase 3: Generate Recommendations

Priority levels:
- **🔥 Critical** - Security issues, missing .gitignore, exposed secrets
- **⚡ Important** - Structure improvements, missing tests, CI/CD
- **💡 Enhancement** - Code quality tools, documentation

### Phase 4: Output

1. `REPO_ANALYSIS.md` - Comprehensive report with score (1-10)
2. `reorganize.sh` - Implementation script
3. `repo-templates/` - Configuration templates
4. Mermaid diagram - Before/after visualization

## Supported Project Types

**Languages:** Node.js, Python, Go, Rust, Java, Ruby, C#/.NET

**Frameworks:** Next.js, Vite, Django, Flask, Rails, Angular, Spring Boot

**Categories:** Web apps, APIs, CLI tools, libraries, monorepos

## Usage

```
Analyze this repository structure and provide recommendations
```

```
Focus on security issues in this repository organization
```

```
Analyze this Next.js project for best practices compliance
```

## Special Handling

- **Monorepos** - Detects lerna.json, nx.json, rush.json
- **Large repos** - Limits analysis to 3 directory levels
- **Security** - Checks for exposed secrets, validates .gitignore
