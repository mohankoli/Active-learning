# S - Single Responsibility Principle (SRP)

## Definition
A class should have only one reason to change, meaning it should do only one job or have only one responsibility.

## Simple Terms
> Don't make one class do everything. Each class should focus on one task only.

## Example
A `User` class should only handle user-related data, while database operations should be handled by a separate `UserRepository` class.
