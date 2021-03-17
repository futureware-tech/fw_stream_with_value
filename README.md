# fw_stream_with_value

## About

The package provides the implementation of StreamWithValue that wraps a
Stream and keeps the latest value that was received from it.

**StreamWithLatestValue** - implementation that wraps a Stream and keeps the latest value that was received from it. The value **will not be** tracked if there are no listeners on updates.

**PushStreamWithValue** - StreamWithValue implementation that creates a Stream from subsequent calls to add. This way, value is always set to the latest value that has been added, regardless of whether the updates are listened to (in contrast to StreamWithLatestValue).

## How to use

1. Add `fw_stream_with_value` to your `pubspec.yaml`:

```yaml
dependencies:
  fw_stream_with_value: ^0.1.0
```

2. Create StreamWithLatestValue

```dart
StreamController<int> _yourStreamController = StreamController<int>();
StreamWithLatestValue<int>  _streamWithValue =
        StreamWithLatestValue<int>(_yourStreamController.stream, initialValue: 0);

```

3. You can add new value to the stream using StreamController.

```dart
_yourStreamController.add(5);
```

4. To get updates on the UI you can use `StreamBuilderWithValue` or `DataStreamWithValueBuilder` widgets:

```dart
 StreamBuilderWithValue<int>(
    streamWithValue: _streamWithValue,
    builder: (BuildContext context, AsyncSnapshot snapshot) {
      return (snapshot.hasData)
        ? Text(
            '${snapshot.data ?? 0}',
            style: Theme.of(context).textTheme.headline4,
          )
        : CircularProgressIndicator();
    },
 )
```

For more examples, please have a look at the [example project](https://github.com/futureware-tech/fw_stream_with_value/blob/ae6320b5ce736dd799431c8b5041f6b4b71ce854/example/lib/main.dart).
