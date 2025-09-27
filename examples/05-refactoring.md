# Example 5: Code Refactoring

Learn how to use Claude Code to refactor and improve existing code.

## Original Code

```python
# user_manager.py
def get_user_data(user_id):
    import sqlite3
    conn = sqlite3.connect('database.db')
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM users WHERE id = " + str(user_id))
    result = cursor.fetchone()
    conn.close()

    if result:
        return {
            'id': result[0],
            'name': result[1],
            'email': result[2],
            'age': result[3]
        }
    return None

def update_user_email(user_id, new_email):
    import sqlite3
    conn = sqlite3.connect('database.db')
    cursor = conn.cursor()
    cursor.execute("UPDATE users SET email = '" + new_email + "' WHERE id = " + str(user_id))
    conn.commit()
    conn.close()

def delete_user(user_id):
    import sqlite3
    conn = sqlite3.connect('database.db')
    cursor = conn.cursor()
    cursor.execute("DELETE FROM users WHERE id = " + str(user_id))
    conn.commit()
    conn.close()
```

## Refactoring Request

```bash
claude "Refactor this Python code to follow best practices, improve security, and reduce duplication"
```

## Refactored Version

Claude will provide:

```python
# user_manager.py
import sqlite3
from typing import Optional, Dict, Any
from contextlib import contextmanager
from dataclasses import dataclass

@dataclass
class User:
    id: int
    name: str
    email: str
    age: int

class UserManager:
    def __init__(self, db_path: str = 'database.db'):
        self.db_path = db_path

    @contextmanager
    def get_connection(self):
        """Context manager for database connections."""
        conn = sqlite3.connect(self.db_path)
        conn.row_factory = sqlite3.Row
        try:
            yield conn
        finally:
            conn.close()

    def get_user(self, user_id: int) -> Optional[User]:
        """Fetch a user by ID.

        Args:
            user_id: The user's ID

        Returns:
            User object if found, None otherwise
        """
        with self.get_connection() as conn:
            cursor = conn.cursor()
            cursor.execute(
                "SELECT id, name, email, age FROM users WHERE id = ?",
                (user_id,)
            )
            row = cursor.fetchone()

            if row:
                return User(**dict(row))
            return None

    def update_user_email(self, user_id: int, new_email: str) -> bool:
        """Update a user's email address.

        Args:
            user_id: The user's ID
            new_email: The new email address

        Returns:
            True if update was successful, False otherwise
        """
        with self.get_connection() as conn:
            cursor = conn.cursor()
            cursor.execute(
                "UPDATE users SET email = ? WHERE id = ?",
                (new_email, user_id)
            )
            conn.commit()
            return cursor.rowcount > 0

    def delete_user(self, user_id: int) -> bool:
        """Delete a user from the database.

        Args:
            user_id: The user's ID

        Returns:
            True if deletion was successful, False otherwise
        """
        with self.get_connection() as conn:
            cursor = conn.cursor()
            cursor.execute(
                "DELETE FROM users WHERE id = ?",
                (user_id,)
            )
            conn.commit()
            return cursor.rowcount > 0

# Usage example
if __name__ == "__main__":
    manager = UserManager()

    # Get user
    user = manager.get_user(1)
    if user:
        print(f"User: {user.name}, Email: {user.email}")

    # Update email
    if manager.update_user_email(1, "newemail@example.com"):
        print("Email updated successfully")

    # Delete user
    if manager.delete_user(2):
        print("User deleted successfully")
```

## Key Improvements

1. **Security**: SQL injection prevention with parameterized queries
2. **DRY Principle**: Eliminated code duplication
3. **Type Safety**: Added type hints
4. **Resource Management**: Context manager for connections
5. **Structure**: Class-based organization
6. **Error Handling**: Better return values and error states
7. **Documentation**: Added docstrings

## Common Refactoring Patterns

- Extract methods/functions
- Replace magic numbers with constants
- Simplify complex conditionals
- Remove dead code
- Improve naming conventions
- Add proper error handling