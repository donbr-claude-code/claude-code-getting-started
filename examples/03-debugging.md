# Example 3: Debugging with Claude Code

Learn how to use Claude Code to debug issues in your code.

## Sample Buggy Code

Create a file `buggy_code.js`:

```javascript
function getUserAge(users, userId) {
    const user = users.find(u => u.id = userId);
    return user.age;
}

const users = [
    { id: 1, name: "Alice", age: 30 },
    { id: 2, name: "Bob", age: 25 }
];

console.log(getUserAge(users, 2)); // Should print 25
```

## Finding the Bug

```bash
claude "Help me debug this JavaScript code - it's not returning the correct user"
```

## Claude's Analysis

Claude will identify:
1. Assignment operator (=) instead of comparison (===)
2. Missing null check for user not found
3. Potential type coercion issues

## Fixed Version

```javascript
function getUserAge(users, userId) {
    const user = users.find(u => u.id === userId);

    if (!user) {
        throw new Error(`User with id ${userId} not found`);
    }

    return user.age;
}

const users = [
    { id: 1, name: "Alice", age: 30 },
    { id: 2, name: "Bob", age: 25 }
];

try {
    console.log(getUserAge(users, 2)); // Prints: 25
    console.log(getUserAge(users, 3)); // Throws error
} catch (error) {
    console.error(error.message);
}
```

## Common Debugging Requests

1. **TypeScript errors:**
   ```bash
   claude "Fix this TypeScript compilation error"
   ```

2. **Runtime errors:**
   ```bash
   claude "Why is this function returning undefined?"
   ```

3. **Logic errors:**
   ```bash
   claude "This sorting algorithm isn't working correctly"
   ```

## Tips

- Include error messages in your request
- Provide context about expected vs actual behavior
- Share relevant code snippets
- Mention the programming language and version