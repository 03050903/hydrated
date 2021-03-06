# Hydrated

Hydrated provides a BehaviorSubject that automatically persists to Flutter's local storage. An async `hydrate()` method rehydrates on command!

## Easy to consume

All values are persisted with `shared_preferences` and restored with `hydrate()` at next app launch.

```dart
final count$ = HydratedSubject<int>("count", seedValue: 0); // persist
await count$.hydrate(); // hydrate

count$.add(42); // this value will be available on next app launch
```

## Ready for BLoC

```dart
class _Bloc {
  /// persist
  final count$ = HydratedSubject<int>("count", seedValue: 0);

  _Bloc() {
    /// hydrate
    this.count$.hydrate();
  }

  // ...
}
```

## Supports types and classes

We support all `shared_preferences` types.

- `int`
- `double`
- `bool`
- `String`
- `List<String>`

```dart
final count$ = HydratedSubject<int>("count");
```

We also support serialized classes with `hydrate` and `persist` arguments.

```dart
final user$ = HydratedSubject<User>(
  "user",
  hydrate: (String s) => User.fromJSON(s),
  persist: (User user) => user.toJSON(),
);
```

## Reliable

Hydrated is mock tested with all supported types and is dogfooded by its creator.

<img alt="demo of Hydrated tests completing successfully" src="https://raw.githubusercontent.com/lukepighetti/hydrated/master/docs/tests.gif" width="600">

## Demo

<img alt="demo of Hydrated BehaviorSubject between app restarts" src="https://raw.githubusercontent.com/lukepighetti/hydrated/master/docs/hydrated.gif" width="400">
