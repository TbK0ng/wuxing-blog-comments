---
description: Display a personalized greeting message
argument-hint: [name]
---

# /hello

## Purpose
Display a personalized greeting to the user. If no name is provided, defaults to "World".

## Contract
**Inputs:**
- `$1` — NAME (optional, string) - The name to greet

**Outputs:** A friendly greeting message

## Instructions
1. Check if a name parameter is provided
2. If no name, use "World" as default
3. Format and return a greeting message
4. Optionally include the current time for extra friendliness

## Examples
- `/hello` → "Hello, World! 👋"
- `/hello Alice` → "Hello, Alice! 👋"
- `/hello 大熊掌门` → "你好，大熊掌门！👋"