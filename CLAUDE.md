# Project: Web Development Capstone

## Stack
- HTML5, CSS3
- Node.js (LTS v24.18.0)
- Git for version control

## Conventions
- Use Conventional Commits format for all commit messages (feat:, fix:, docs:, chore:)
- Keep code readable with meaningful variable names
- Follow semantic HTML structure
- Comment complex logic

## Project Structure
- README.md - project overview
- LICENSE - MIT license
- .gitignore - Node.js ignore rules
## Rules Learned From Prompting Exercise

1. Never accept AI-generated form code without checking input `type` attributes explicitly — a vague prompt produced a password field with `type="text"` instead of `type="password"`, which is a silent security issue that doesn't show up just by looking at the rendered page.

2. Always specify validation rules explicitly in the prompt (minimum lengths, required formats, required character types) rather than saying "add validation" — vague validation requests produce empty-string checks only, not real rules.

3. Every form submit handler must call `event.preventDefault()` and be explicitly requested — otherwise generated forms default to a native submit that reloads the page and silently discards all entered data.