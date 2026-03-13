# Documentation Standards Specialist - Reference Documentation

This directory contains reference materials and procedures for documentation standards and code review workflow implementation.

## Core Domains

### File Formatting Standards

EditorConfig configuration for consistent formatting:

```ini
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

Key requirements:
- Use spaces for indentation (2 spaces)
- Unix-style line endings (LF)
- UTF-8 character encoding
- No trailing whitespace
- Files must end with a newline

### Frontmatter Metadata Standards

Required fields for documentation articles:
1. `title` - Article title
2. `description` - Brief description
3. `authors` - List of author identifiers
4. `tags` - Content categorization

Required field order:
1. title
2. description
3. baseline
4. cover
5. authors
6. contributors
7. editors
8. keywords
9. related
10. tags

Example frontmatter:
```yaml
---
title: "Article Title"
description: "Brief description of the article content"
authors:
  - author-username
contributors:
  - contributor-username
editors:
  - editor-username
keywords:
  - keyword1
  - keyword2
related:
  - path/to/related-article
tags:
  - tag1
  - tag2
---
```

### Content Types and Tags

Content type classifications:
- `doka` - Reference material (methods, properties, specifications)
- `article` - Extended educational content
- `placeholder` - Draft or stub content pending completion

Section-specific tags:
- css, html, js - Technology-specific content
- a11y - Accessibility content
- tools - Development tools and platform documentation
- recipe - How-to guides and tutorials

## PR Review Workflow

### Workflow Sequence

```
[Create PR] --> [Automated Checks] --> [Label Assignment] --> [Review Checklist] --> [Preview Deploy] --> [Human Review] --> [Merge]
```

### Automated PR Checks

1. **Formatting Check** - EditorConfig linting on changed files
2. **Frontmatter Validation** - Required fields, field order, cross-references
3. **Link Checker** - Internal and external link validation

### Preview Deployment

- Build documentation with PR changes
- Deploy to preview environment
- Post comment with preview URL and changed materials list
- URL format: `https://content-{PR_NUMBER}.dev.{domain}`

### Review Checklists

For new reference documentation:
- Title is clear and descriptive
- Description explains the concept
- Code examples are accurate and tested
- Related articles are linked
- Author information is complete
- Accessibility considerations addressed

For new articles:
- Learning objectives are clear
- Content flows logically
- Examples support the narrative
- Summary/conclusion present
- Appropriate for target audience
- Technical accuracy verified

## Quality Automation

### Frontmatter Validation

Validation checks:
- Required field existence
- Field order compliance
- Related article path validation
- Author/contributor profile existence

Auto-fix capability:
- Reorder frontmatter fields on merge
- Commit corrections with bot attribution

### Link Checking

Scheduled weekly comprehensive validation:
- Buffer size: 8192
- Max connections: 10
- Timeout: 20 seconds
- Excluded: localhost, 127.0.0.1, codepen.io URLs

### Spell Checking

Command: `npx yaspeller --only-errors --file-extensions ".md,.html" *`

Dictionary patterns:
- Simple word: `"kubernetes"`
- Word with variations: `"container(s|)"`
- Word with multiple endings: `"API(s|'s)"`

Inline exclusions:
```markdown
Technical term here <!-- yaspeller ignore -->

<!-- yaspeller ignore:start -->
Text to exclude from spell checking
<!-- yaspeller ignore:end -->
```

## Code Ownership

### CODEOWNERS Configuration

```
# Section Owners
css @css-reviewer1 @css-reviewer2
html @html-reviewer1 @html-reviewer2
js @js-reviewer1 @js-reviewer2
tools @tools-reviewer
a11y @accessibility-reviewer

# Demo Owners
**/demos @demo-specialist

# Infrastructure
.github @devops-lead
```

### Label-Based Assignment

Labels applied based on changed files:
- File path patterns trigger specific labels
- Labels trigger reviewer assignment
- Content type detection from frontmatter tags

## Issue Management

### Issue Templates

**Error Report:**
- Article link (required)
- Error description with screenshots
- Sources with correct information

**New Content Request:**
- Topic description
- Justification for documentation
- Contribution intent checkbox

**Q&A Entry:**
- Question text
- Answer intent checkbox

## Content Contribution

### Contribution Workflow

1. Fork repository
2. Create content using templates
3. Add supporting materials (images, demos, practice examples)
4. Submit pull request with descriptive title

### Article Templates

Reference documentation structure:
- Summary
- Syntax
- Parameters table
- Return value
- Examples (basic and advanced)
- Browser support
- See also links

Educational article structure:
- Introduction with learning objectives
- Main content sections
- Summary with key takeaways
- Further reading links

### Style Guidelines

Writing:
- Clear, direct language
- Practical examples
- Avoid unexplained jargon

Code examples:
- Test all code before submitting
- Use meaningful variable names
- Include comments for complex logic

Formatting:
- Hierarchical headings (H2, H3, H4)
- Focused paragraphs
- Lists for related items
- Alt text for images

## Demo Standards

### File Structure

```
article-folder/
  demos/
    demo-name/
      index.html
      images/
      scripts/
  index.md
```

### Demo Embedding

```markdown
<iframe title="Demo Description" src="demos/demo-name/" height="250"></iframe>
```

Requirements:
- Descriptive title attribute
- Minimum height specified
- Relative path to demo folder

## Release Management

### Changelog Generation

Auto-generated from merged PRs based on labels:
- Platform/Tools
- Accessibility
- CSS/HTML/JS Documentation
- Bug Fixes
- Improvements
- Infrastructure
- Other Changes

### Release Process

1. Generate release notes from PR labels
2. Apply semantic versioning
3. Document breaking changes
4. Trigger automated deployment

## Author Attribution

### Profile Structure

Location: `people/{username}/index.md`

Required fields:
- `name` - Display name
- `url` - Personal site or GitHub link

Optional fields:
- `photo` - Avatar image
- `photoAlt` - Accessibility description

### Contribution Statistics

Tracked per contributor:
- Total articles written
- Total practice examples
- Total Q&A answers
- Issues created
- Pull requests submitted
- Most contributed category

## Licensing

**Text Content:** CC BY-NC-SA 4.0
- May be modified and redistributed
- Must maintain attribution
- Non-commercial use only
- Derivative works use same license

**Media Content:** CC BY-NC-ND 4.0
- May be redistributed without modification
- Must maintain attribution
- Non-commercial use only

## GitHub Actions Templates

### PR Quality Check Workflow

```yaml
name: PR Quality Checks
on:
  pull_request:

jobs:
  format-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - name: Get changed files
        id: files
        uses: Ana06/get-changed-files@v2.2.0
      - name: Run EditorConfig Linter
        run: |
          npm install editorconfig-checker --global
          for file in ${{ steps.files.outputs.added_modified }}; do
            editorconfig-checker ${file}
          done

  meta-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - name: Get changed markdown files
        id: files
        uses: Ana06/get-changed-files@v2.2.0
        with:
          filter: '**/index.md'
      - name: Validate Frontmatter
        run: |
          npx yaml-cat --format json --output result.json ${{ steps.files.outputs.added_modified }}
          node .github/scripts/frontmatter.js

  link-check:
    needs: [format-check, meta-check]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Get changed markdown files
        id: files
        uses: Ana06/get-changed-files@v2.2.0
        with:
          filter: '*.md'
          format: 'csv'
      - name: Check Links
        uses: JustinBeckwith/linkinator-action@v1
        with:
          paths: ${{ steps.files.outputs.added_modified }}
          markdown: true
```

### Auto-Label Workflow

```yaml
name: PR Labels
on:
  pull_request_target:

jobs:
  labels:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          ref: ${{ github.event.pull_request.head.sha }}
      - name: Apply Labels
        uses: actions/labeler@v4
        with:
          repo-token: "${{ secrets.GITHUB_TOKEN }}"
          configuration-path: ".github/labeler.yml"
```

## Quick Reference

### Before Submitting PR

- [ ] All formatting follows EditorConfig standards
- [ ] Frontmatter includes required fields
- [ ] Frontmatter fields are in correct order
- [ ] All internal links are valid
- [ ] Images have alt text
- [ ] Demos work correctly
- [ ] Spell check passes
- [ ] Author profile exists

### PR Review Checklist

- [ ] Automated checks pass
- [ ] Content is accurate
- [ ] Code examples work
- [ ] Writing is clear
- [ ] Accessibility considered
- [ ] Preview looks correct

## Common Errors and Solutions

| Error | Cause | Solution |
|-------|-------|----------|
| Missing required field: title | Frontmatter lacks title | Add title field to frontmatter |
| Field X not in correct position | Field order incorrect | Reorder fields per specification |
| Invalid author reference | Author profile doesn't exist | Create profile in people/ directory |
| Related article not found | Invalid related path | Fix path or create referenced article |
| Link check failed | Broken link detected | Fix or remove broken link |
| EditorConfig violation | Formatting inconsistency | Apply EditorConfig rules |
