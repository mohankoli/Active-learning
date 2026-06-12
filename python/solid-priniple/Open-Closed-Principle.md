# O - Open Closed Principle (OCP)

## Definition

Software entities (classes, modules, functions) should be:

* **Open for Extension**
* **Closed for Modification**

This means you should be able to add new functionality without changing existing, tested code.

---

## Simple Terms

> Add new features by adding new code, not by modifying existing code.

### Open for Extension

You can add new functionality.

### Closed for Modification

Do not modify existing working code.

---

# ❌ Bad Example (Violates OCP)

In the example below, every time a new payment method is added, we must modify the existing `PaymentProcessing` class.

```python
class PaymentProcessing:
    def pay(self, payment_method: str, amount):
        if payment_method == 'UPI':
            print(f"Payment started using UPI and amount is {amount}")
            print("UPI payment done!!")

        elif payment_method == "CreditCard":
            print(f"Payment started using Credit Card and amount is {amount}")
            print("Credit Card payment done!!")


pay_processor = PaymentProcessing()
pay_processor.pay("CreditCard", 500)
```

## Problem

Today we support:

* UPI
* Credit Card

Tomorrow if we want:

* PayPal
* Net Banking
* Debit Card
* Apple Pay

We must keep modifying the existing class.

```python
elif payment_method == "PayPal":
    ...
```

```python
elif payment_method == "NetBanking":
    ...
```

This violates OCP because existing code changes whenever a new payment method is introduced.

---

# ✅ Good Example (Follows OCP)

## Step 1: Create an Abstract Payment Interface

```python
from abc import ABC, abstractmethod

class PaymentMethod(ABC):

    @abstractmethod
    def pay(self, amount):
        pass
```

---

## Step 2: Create UPI Payment Class

```python
class UPIPayment(PaymentMethod):

    def pay(self, amount):
        print(f"Payment started using UPI and amount is {amount}")
        print("UPI payment done!!")
```

---

## Step 3: Create Credit Card Payment Class

```python
class CreditCardPayment(PaymentMethod):

    def pay(self, amount):
        print(f"Payment started using Credit Card and amount is {amount}")
        print("Credit Card payment done!!")
```

---

## Step 4: Payment Processor

```python
class PaymentProcessor:

    def process_payment(self, payment_method, amount):
        payment_method.pay(amount)
```

---

## Step 5: Client Code

```python
upi = UPIPayment()

processor = PaymentProcessor()
processor.process_payment(upi, 500)
```

### Output

```text
Payment started using UPI and amount is 500
UPI payment done!!
```

---

# Adding PayPal (Without Modifying Existing Code)

Create a new class:

```python
class PayPalPayment(PaymentMethod):

    def pay(self, amount):
        print(f"Payment started using PayPal and amount is {amount}")
        print("PayPal payment done!!")
```

Usage:

```python
paypal = PayPalPayment()

processor = PaymentProcessor()
processor.process_payment(paypal, 1000)
```

### Output

```text
Payment started using PayPal and amount is 1000
PayPal payment done!!
```

Notice:

* No changes in `PaymentProcessor`
* No changes in `UPIPayment`
* No changes in `CreditCardPayment`

We only added a new class.

This follows OCP.

---

# Real-World Example

Think about Amazon payment options.

Initially:

* Credit Card
* UPI

Later Amazon adds:

* PayPal
* EMI
* Gift Card
* Wallet

Amazon should not rewrite the payment processor every time.

Instead, each payment type should implement a common payment interface.

---

# Interview Answer

**What is the Open Closed Principle?**

The Open Closed Principle states that software entities should be open for extension but closed for modification. We should be able to add new functionality without changing existing, tested code.

For example, instead of using multiple `if-else` conditions for payment methods, we create a common `PaymentMethod` interface and implement separate classes such as `UPIPayment`, `CreditCardPayment`, and `PayPalPayment`. When a new payment method is required, we simply add a new class without modifying existing code.
