# Example 4: Writing Tests

Use Claude Code to generate comprehensive test suites.

## Sample Function to Test

```javascript
// calculator.js
class Calculator {
    add(a, b) {
        return a + b;
    }

    subtract(a, b) {
        return a - b;
    }

    multiply(a, b) {
        return a * b;
    }

    divide(a, b) {
        if (b === 0) {
            throw new Error("Division by zero");
        }
        return a / b;
    }
}

module.exports = Calculator;
```

## Requesting Tests

```bash
claude "Write comprehensive Jest tests for this Calculator class"
```

## Generated Test Suite

Claude will create:

```javascript
// calculator.test.js
const Calculator = require('./calculator');

describe('Calculator', () => {
    let calc;

    beforeEach(() => {
        calc = new Calculator();
    });

    describe('add', () => {
        test('adds two positive numbers', () => {
            expect(calc.add(2, 3)).toBe(5);
        });

        test('adds negative numbers', () => {
            expect(calc.add(-2, -3)).toBe(-5);
        });

        test('adds zero', () => {
            expect(calc.add(5, 0)).toBe(5);
        });
    });

    describe('subtract', () => {
        test('subtracts two positive numbers', () => {
            expect(calc.subtract(5, 3)).toBe(2);
        });

        test('subtracts resulting in negative', () => {
            expect(calc.subtract(3, 5)).toBe(-2);
        });
    });

    describe('multiply', () => {
        test('multiplies two positive numbers', () => {
            expect(calc.multiply(3, 4)).toBe(12);
        });

        test('multiplies by zero', () => {
            expect(calc.multiply(5, 0)).toBe(0);
        });

        test('multiplies negative numbers', () => {
            expect(calc.multiply(-2, -3)).toBe(6);
        });
    });

    describe('divide', () => {
        test('divides two numbers', () => {
            expect(calc.divide(10, 2)).toBe(5);
        });

        test('throws error on division by zero', () => {
            expect(() => calc.divide(5, 0)).toThrow('Division by zero');
        });

        test('handles decimal results', () => {
            expect(calc.divide(5, 2)).toBe(2.5);
        });
    });
});
```

## Test Coverage

Ask Claude to check coverage:

```bash
claude "Add edge cases and improve test coverage for the Calculator class"
```

## Different Testing Frameworks

Claude Code supports various testing frameworks:

- **Python**: pytest, unittest
- **JavaScript**: Jest, Mocha, Vitest
- **Java**: JUnit
- **Go**: testing package
- **Rust**: built-in testing

Just specify your preferred framework in your request!