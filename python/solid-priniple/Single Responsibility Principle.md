# S - Single Responsibility Principle (SRP)

## Definition

A class should have only one reason to change, meaning it should do only one job or have only one responsibility.

## Simple Terms

> Don't make one class do everything. Each class should focus on one task only.

## Why SRP?

When a class has multiple responsibilities:

* It becomes difficult to maintain.
* Changes in one functionality may impact another.
* Testing becomes harder.
* Code becomes tightly coupled.

A class should have only one reason to change.

---

# ❌ Bad Example (Violates SRP)

In the example below, the `User` class is responsible for:

1. Managing user data.
2. Sending emails.
3. Saving data to the database.

This means the class has multiple reasons to change.

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def get_user_data(self):
        print(f"The name is {self.name} and email is {self.email}")

    def send_email(self):
        print(f"Sending welcome mail to {self.email}")

    def save_to_database(self):
        print(f"Saving {self.name} user data to DB")


user1 = User("Mohan", "mohan@gmail.com")

user1.get_user_data()
user1.send_email()
user1.save_to_database()
```

## Problems

* If email logic changes, modify `User`.
* If database logic changes, modify `User`.
* If user information changes, modify `User`.

The `User` class has multiple responsibilities and violates SRP.

---

# ✅ Good Example (Follows SRP)

Separate each responsibility into its own class.

## user.py

```python
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def get_user_info(self):
        print(f"Name: {self.name}")
        print(f"Email: {self.email}")
```

## emailService.py

```python
class EmailService:
    def send_email(self, user):
        print(f"Sending welcome email to {user.email}")
```

## userRepository.py

```python
class UserRepository:
    def save_to_database(self, user):
        print(f"Saving {user.name} user data to DB")
```

## main.py

```python
from user import User
from emailService import EmailService
from userRepository import UserRepository

user1 = User("mohan", "mohankoli1990@gmail.com")

user1.get_user_info()

email_service = EmailService()
email_service.send_email(user1)

user_repository = UserRepository()
user_repository.save_to_database(user1)
```

## Responsibilities

| Class          | Responsibility          |
| -------------- | ----------------------- |
| User           | Store user-related data |
| EmailService   | Send emails             |
| UserRepository | Database operations     |

---

# Interview Answer

**What is the Single Responsibility Principle?**

The Single Responsibility Principle states that a class should have only one reason to change. A class should perform only one responsibility.

For example, a `User` class should only manage user data. Email functionality should be moved to an `EmailService`, and database operations should be handled by a `UserRepository`. This improves maintainability, readability, scalability, and testability.

