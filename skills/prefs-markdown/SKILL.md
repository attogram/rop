---
name: prefs-markdown
description: >
  Use this skill as a style guide for generating Markdown content.
  It provides rules for formatting, line length, and content.
---

# Markdown Preferences Skill v1.1

Adopt these preferences when generating content in Markdown format.

## Philosophy
- Minimize Token Usage
- Optimize for human readability
- No Fluff

## Scope
- Adhere to these rules when creating, modifying, or auditing Markdown files.

## Lists
- Items start at the beginning of the line with `- `
- 2 spaces per indent level for nested items

## Markdown Headers
- All headers must have a blank line above them, except top-level `#`
- If a header has content, content must begin on the line directly after
  the header, no blank line in between
- Example:
```markdown
# Foo

## Bar

### Baz
{content}

## Qux
{content}
```

## Line Length
- Markdown files MUST NOT exceed 80 characters per line.
  - Exception for URLs and other elements that cannot be reasonably
    broken.

## Hyperlinking
- When linking, use hyperlinked relatively.
  - Example: [`docs/Foo.md`](../../docs/Foo.md)
- Directories MUST NOT use a trailing slash in the URL.
  - Example: [`docs`](../../docs)
- Validate the path before adding any link.
  - You MUST run an empirical check (`ls`, `find`, etc.) to verify existence.

## No Fluff
- Content must be strictly high-signal. Do NOT use:
  - Emojis
  - Decorative spacers (`---`)
  - Conversational fillers
  - Excessive **bolding** or *italics* without a clear purpose for emphasis.
