# Example 1: Hello World

The simplest way to interact with Claude Code.

## Interactive Mode

Start Claude Code:
```bash
claude
```

Then type:
```
Help me create a simple "Hello World" program in Python
```

Claude will:
1. Create a hello_world.py file
2. Add the Python code
3. Explain how to run it

## Command Mode

Run directly from terminal:
```bash
claude "Create a hello world script in JavaScript"
```

## Expected Output

Claude will create a file like:

```javascript
// hello.js
console.log("Hello, World!");
```

And explain:
- How to run it: `node hello.js`
- What the code does
- Possible variations