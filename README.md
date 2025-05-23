
# Flutter PayPal Payment Plus Package

The **Flutter PayPal Payment Plus Package** provides an easy-to-integrate solution for enabling PayPal payments in your Flutter mobile application. This package allows for a seamless checkout experience with both sandbox and production environments.

## Features

- **Seamless PayPal Integration**: Easily integrate PayPal payments into your Flutter app.
- **Sandbox Mode Support**: Test payments in a safe sandbox environment before going live.
- **Customizable Transactions**: Define custom transaction details for each payment.
- **Payment Outcome Callbacks**: Handle success, error, and cancellation events for payments.

## Installation

To install the Flutter PayPal Payment Package, follow these steps

1. Add the package to your project's dependencies in the `pubspec.yaml` file:
   ```yaml
   dependencies:
     flutter_paypal_payment_plus: ^1.0.1
    ``` 
2. Run the following command to fetch the package:

    ``` 
    flutter pub get
    ``` 

## Usage
1. Import the package into your Dart file:

    ``` 
    import 'package:flutter_paypal_payment_plus/flutter_paypal_payment_plus.dart';
    ```
2. Navigate to the PayPal checkout view with the desired configuration:
```dart
/// Entry point of the application.
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

            /// When pressed, navigates to the [PaypalCheckoutView] screen to initiate a PayPal payment.
            onPressed: () {
              Navigator.of(context).push(
                MaterialPageRoute(
                  builder: (BuildContext context) => PaypalCheckoutView(
                    /// Indicates whether the PayPal sandbox (test) environment should be used.
                    sandboxMode: true,

                    /// Your PayPal REST API Client ID.
                    clientId: "YOUR_CLIENT_ID",

                    /// Your PayPal REST API Secret Key.
                    secretKey: "YOUR_SECRET_KEY",

                    /// The URL to redirect to upon successful payment completion.
                    returnURL: "YOUR_RETURN_URL",

                    /// The URL to redirect to if the user cancels the payment.
                    cancelURL: "YOUR_CANCEL_URL",

                    /// Transaction details including the list of items and total payment amount.
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

                    /// Optional note or message shown to the user about the payment.
                    note: "Contact us for any questions on your order.",

                    /// Callback triggered when the payment completes successfully.
                    /// Logs the result and navigates back to the previous screen.
                    onSuccess: (PaymentSuccessModel model) async {
                      log("onSuccess: ${model.toJson()}");
                      Navigator.pop(context);
                    },

                    /// Callback triggered when an error occurs during the payment process.
                    /// Logs the error and navigates back to the previous screen.
                    onError: (error) {
                      log("onError: $error");
                      Navigator.pop(context);
                    },

                    /// Callback triggered when the user cancels the PayPal payment.
                    /// Prints a log and returns to the previous screen.
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
