# 💻 Полезные сниппеты кода

## Flutter Widgets

### Красивый Gradient Container
```dart
Container(
  decoration: BoxDecoration(
    gradient: LinearGradient(
      colors: [Colors.blue.shade400, Colors.purple.shade600],
      begin: Alignment.topLeft,
      end: Alignment.bottomRight,
    ),
    borderRadius: BorderRadius.circular(20),
    boxShadow: [
      BoxShadow(
        color: Colors.black.withOpacity(0.1),
        blurRadius: 10,
        offset: Offset(0, 5),
      ),
    ],
  ),
  child: Center(
    child: Text(
      'Hello World!',
      style: TextStyle(
        color: Colors.white,
        fontSize: 24,
        fontWeight: FontWeight.bold,
      ),
    ),
  ),
)
```

### Анимированная кнопка
```dart
class AnimatedButton extends StatefulWidget {
  @override
  _AnimatedButtonState createState() => _AnimatedButtonState();
}

class _AnimatedButtonState extends State<AnimatedButton>
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _animation;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: Duration(milliseconds: 200),
      vsync: this,
    );
    _animation = Tween<double>(begin: 1.0, end: 0.95).animate(_controller);
  }

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTapDown: (_) => _controller.forward(),
      onTapUp: (_) => _controller.reverse(),
      onTapCancel: () => _controller.reverse(),
      child: ScaleTransition(
        scale: _animation,
        child: Container(
          padding: EdgeInsets.symmetric(horizontal: 20, vertical: 12),
          decoration: BoxDecoration(
            color: Colors.blue,
            borderRadius: BorderRadius.circular(10),
          ),
          child: Text('Нажми меня!', style: TextStyle(color: Colors.white)),
        ),
      ),
    );
  }
}
```

## Dart Tips & Tricks

### Extension Methods
```dart
extension StringExtensions on String {
  String get capitalize => this[0].toUpperCase() + substring(1);

  bool get isEmail => RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(this);
}

// Использование
void main() {
  print('hello world'.capitalize); // Hello world
  print('test@email.com'.isEmail); // true
}
```

### Null Safety
```dart
// Старый способ
String? getUserName(User? user) {
  return user?.name;
}

// Новый способ с null safety
String? getUserName(User? user) => user?.name;

// Или с оператором ??
String getUserName(User? user) => user?.name ?? 'Unknown';
```

## GitHub Actions

### Автоматическое тестирование Flutter
```yaml
name: Flutter CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - uses: subosito/flutter-action@v2
      with:
        flutter-version: '3.10.0'
    - run: flutter pub get
    - run: flutter test
    - run: flutter build apk --release
```

## Полезные команды

```bash
# Быстрое создание Flutter проекта
flutter create my_app --platforms=android,ios --org=com.example

# Анализ кода
flutter analyze

# Форматирование кода
dart format .

# Создание APK
flutter build apk --release --split-per-abi

# Создание iOS архива
flutter build ios --release
```
