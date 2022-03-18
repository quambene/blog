<!-- markdownlint-disable MD001 -->

# Flutter

- [Stateless widget](#stateless-widgets)
- [Stateful widget](#stateful-widgets)

### Stateless widget

``` dart
class MyWidget extends StatelessWidget {
  const MyWidget({ Key? key }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      // ...
    );
  }
}
```

### Stateful widget

``` dart
class MyWidget extends StatefulWidget {
  const MyWidget({ Key? key }) : super(key: key);

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  Widget build(BuildContext context) {
    return Container(
      // ...
    );
  }
}
```
