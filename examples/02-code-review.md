# Example 2: Code Review

Learn how to use Claude Code for code reviews and improvements.

## Reviewing Existing Code

Suppose you have this Python function:

```python
def calculate_total(items):
    total = 0
    for i in range(len(items)):
        total = total + items[i]['price'] * items[i]['quantity']
    return total
```

## Using Claude for Review

```bash
claude "Review this Python function and suggest improvements:
def calculate_total(items):
    total = 0
    for i in range(len(items)):
        total = total + items[i]['price'] * items[i]['quantity']
    return total"
```

## Expected Suggestions

Claude might suggest:
1. Using more Pythonic iteration
2. Adding type hints
3. Adding error handling
4. Using list comprehension or sum()

## Improved Version

```python
from typing import List, Dict

def calculate_total(items: List[Dict[str, float]]) -> float:
    """Calculate total price for a list of items.

    Args:
        items: List of dictionaries with 'price' and 'quantity' keys

    Returns:
        Total price as a float

    Raises:
        KeyError: If item is missing required keys
        TypeError: If values are not numeric
    """
    if not items:
        return 0.0

    return sum(item['price'] * item['quantity'] for item in items)
```

## Try It Yourself

1. Create a file with your own code
2. Ask Claude to review it
3. Apply the suggestions
4. Compare the before and after