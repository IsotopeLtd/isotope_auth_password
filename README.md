# Isotope Password Auth Service

Extends the Isotope `AuthServiceAdapter` and provides a `PasswordAuthService` for email/password credentialed  authentication using the `FirebaseAuth` backend service provider.

## Installation

Add the following dependencies to your `pubspec.yaml`:

```dart
dependences:
  isotope_auth:
    git: git://github.com/isotopeltd/isotope_auth.git
  isotope_auth_password:
    git: git://github.com/isotopeltd/isotope_auth_password.git
```

## Implementation

In your project, import the package:

```dart
import 'package:isotope_auth_password/isotope_auth_password';
```

Then instantiate a new `PasswordAuthService` object:

```dart
// authService constant is used in later examples:
const PasswordAuthService authService = new PasswordAuthService();
```

If you are using the `Isotope` framework, you'll likely be register the `PasswordAuthService` as a lazy singleton object using `registrar` service locator:

```dart
import 'package:isotope/registrar.dart';

void setup() {
  Registrar.instance.registerLazySingleton<PasswordAuthService>(PasswordAuthService());
}
```

See the [registrar documentation](https://github.com/IsotopeLtd/isotope/tree/master/lib/src/registrar) for information about registering, fetching, resetting and unregistering lazy singletons.

### Create identity

Creates a `FirebaseUser` in `FirebaseAuth` and returns an `IsotopeIdentity` object containing the mapped properties.

Method signature:

```dart
Future<IsotopeIdentity> createIdentity(Map<String, dynamic> credentials)
```

This method expects the following keys passed as a `credentials` map:

- String `email`: the email address for the identity
- String `password`: the password for the identity

The method will return an `IsotopeIdentity` object.

Example:

```dart
IsotopeIdentity identity = await authService.createIdentity({
  email: 'someone@example.com', 
  password: 'aBcD*1234!'
});
```

### Sign in

Signs in to Firebase Auth.

Method signature:

```dart
Future<IsotopeIdentity> signIn(Map<String, dynamic> credentials)
```

This method expects the following keys passed as a `credentials` map:

- String `email`: the email address for the identity
- String `password`: the password for the identity

The method will return an `IsotopeIdentity` object.

Example:

```dart
IsotopeIdentity identity = await authService.signIn({
  email: 'someone@example.com', 
  password: 'aBcD*1234!'
});
```

### Sign out

Signs out of Firebase Auth.

Method signature:

```dart
Future<void> signOut()
```

Example:

```dart
await authService.signOut();
```

### Reset password

Sends a password reset link to the specified email address.

Method signature:

```dart
Future<void> sendPasswordReset(String email)
```

Example:

```dart
await authService.sendPasswordReset();
```

### Current identity

Returns an `IsotopeIdentity` object if the user is authenticated or `null` when not authenticated.

Method signature:

```dart
Future<IsotopeIdentity> currentIdentity()
```

Example:

```dart
IsotopeIdentity identity = authService.currentIdentity();
```

## License

This library is available as open source under the terms of the MIT License.

## Copyright

Copyright © 2020 Jurgen Jocubeit
