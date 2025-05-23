# Flutter PayPal Payment Plus Package

The **Flutter PayPal Payment Plus Package** offers a seamless and straightforward integration of PayPal Checkout into your Flutter mobile applications. Whether you're developing for sandbox testing or live production, this package enables a smooth and customizable checkout experience.

---

## 📦 Features

- ✅ **Seamless PayPal Integration**: Simplified integration for PayPal payments within Flutter apps.
- 🧪 **Sandbox Mode Support**: Easily toggle between sandbox and production environments.
- 💳 **Customizable Transactions**: Define full transaction details including items, amounts, and descriptions.
- 🔄 **Payment Callbacks**: Respond to success, error, or cancellation using intuitive callback handlers.

---

## 🚀 Installation

To get started, follow these steps:

### 1. Add the dependency:

In your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_paypal_payment_plus: ^1.0.1
```

### 2. Fetch the package:

```bash
flutter pub get
```

---

## 🛠️ Usage

### 1. Import the package

```dart
import 'package:flutter_paypal_payment_plus/flutter_paypal_payment_plus.dart';
```

### 2. Use `PaypalCheckoutView` to initiate a payment:

Below is a complete example:

```dart
import 'dart:developer';
import 'package:flutter/material.dart';
import 'package:flutter_paypal_payment_plus/flutter_paypal_payment_plus.dart';

void main() {
  runApp(const PaypalPaymentDemo());
}

class PaypalPaymentDemo extends StatelessWidget {
  const PaypalPaymentDemo({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'PaypalPaymentDemo',
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        body: Center(
          child: TextButton(
            child: const Text('Pay with PayPal'),
            onPressed: () {
              Navigator.of(context).push(
                MaterialPageRoute(
                  builder: (BuildContext context) => PaypalCheckoutView(
                    sandboxMode: true,
                    clientId: "YOUR_CLIENT_ID",
                    secretKey: "YOUR_SECRET_KEY",
                    returnURL: "YOUR_RETURN_URL",
                    cancelURL: "YOUR_CANCEL_URL",
                    transactions: const TransactionOption(
                      payPalAmount: PayPalAmount(
                        total: "100",
                        currency: "USD",
                        details: PaymentDetails(
                          subtotal: '100',
                          shipping: "0",
                          shippingDiscount: 0,
                        ),
                      ),
                      description: "The payment transaction description.",
                      itemList: ItemList(
                        items: [
                          Item(
                            name: "Apple",
                            quantity: 1,
                            price: "50",
                            currency: "USD",
                          ),
                          Item(
                            name: "Pineapple",
                            quantity: 5,
                            price: "10",
                            currency: "USD",
                          ),
                        ],
                      ),
                    ),
                    note: "Contact us for any questions on your order.",
                    onSuccess: (PaymentSuccessModel model) async {
                      log("onSuccess: ${model.toJson()}");
                      Navigator.pop(context);
                    },
                    onError: (error) {
                      log("onError: $error");
                      Navigator.pop(context);
                    },
                    onCancel: () {
                      print('Cancelled');
                      Navigator.pop(context);
                    },
                  ),
                ),
              );
            },
          ),
        ),
      ),
    );
  }
}
```

---

## 📘 Notes

- To obtain `clientId` and `secretKey`, register your app at [PayPal Developer Dashboard](https://developer.paypal.com/).
- This package is built on top of the WebView-based implementation of PayPal's Smart Payment Buttons.

---

## 📄 License

This package is open-source and available under the [MIT License](LICENSE).

---

## 🤝 Contributions

Contributions, suggestions, and pull requests are welcome!  
Feel free to [open an issue](https://github.com/YaseenHussein/flutter_paypal_payment_plus/issues) if you find bugs or want new features.

---
