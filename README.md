# rafis_inventory

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.


## Assignment 7 
### Steps 
1. Install Flutter using Homebrew
`brew install flutter`

2. Create a flutter project called rafis_inventory by running the following command :
`flutter create rafis_inventory`

3. Add this code to the `main.dart file` : 
```dart
import 'package:flutter/material.dart';
import 'package:rafis_inventory/menu.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Rafis Inventory',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // TRY THIS: Try running your application with "flutter run". You'll see
        // the application has a blue toolbar. Then, without quitting the app,
        // try changing the seedColor in the colorScheme below to Colors.green
        // and then invoke "hot reload" (save your changes or press the "hot
        // reload" button in a Flutter-supported IDE, or press "r" if you used
        // the command line to start the app).
        //
        // Notice that the counter didn't reset back to zero; the application
        // state is not lost during the reload. To reset the state, use hot
        // restart instead.
        //
        // This works for code too, not just values: Most code changes can be
        // tested with just a hot reload.
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
        useMaterial3: true,
      ),
      home: MyHomePage(),
    );
  }
}
```

4. In the `lib` directory, create a `menu.dart` file

5. In the menu.dart file, copy this code
```dart
import 'package:flutter/material.dart';

class Items {
  final String name;
  final IconData icon;
  final Color color;

  Items(this.name, this.icon, this.color);
}

class MyHomePage extends StatelessWidget {
  MyHomePage({Key? key}) : super(key: key);

  final List<Items> items = [
    Items("View Items", Icons.checklist, Colors.indigo.shade400),
    Items("Add Item", Icons.add_shopping_cart, Colors.blue.shade400),
    Items("Logout", Icons.logout, Colors.red.shade400),
  ];

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Rafi\'s Inventory',
        ),
      ),
      body: SingleChildScrollView(
        // Scrolling wrapper widget
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding for the page
          child: Column(
            // Widget to display children vertically
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Text widget to display text with center alignment and appropriate style
                child: Text(
                  'My inventory', // Text indicating the shop name
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container for our cards.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((Items item) {
                  // Iteration for each item
                  return ItemCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

class ItemCard extends StatelessWidget {
  final Items item;

  const ItemCard(this.item, {Key? key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        // Responsive touch area
        onTap: () {
          // Show a SnackBar when clicked
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("You pressed the ${item.name} button!")));
        },
        child: Container(
          // Container to hold Icon and Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

6. The previous step already included the Snackbar


### Stateless vs Stateful in Flutter
If a widget can change when a user interacts with it, it's stateful. Meanwhile, a stateless widget
never changes. The examples of stateless widgets are `Icon`, `IconButton`, and `Text`.

One can also say that a stateful widget is dynamic. A notable example would be it changing appearance
in response to interactions by user or when the widget receives data

Source : [Click here to access the flutter docs](https://docs.flutter.dev/ui/interactivity#stateful-and-stateless-widgets)

### Widgets in my app
In `main.dart`:

1. `MaterialApp`: This is the root widget that configures your app. It provides a basic structure for your app, including the title and theme.

2. `MyApp`: This is your custom widget that extends StatelessWidget and represents the root of your app. It doesn't change its appearance once it's built.


In `menu.dart`:

1. `Scaffold:` This widget creates the basic layout of your app with an app bar and content area.

2. `AppBar`: It's the top app bar that displays the title of your app.

3. `SingleChildScrollView`: This widget allows content to be scrollable, ensuring that all content fits on the screen, even if it's too long.

4. `Column`: It's used to arrange widgets vertically, making it easy to stack items on top of each other.

5. `GridView.count`: This widget creates a grid layout with a specified number of columns. It's used to display a grid of items.

6. `ItemCard`: This is your custom widget that represents each item in the grid. It's built using a colored container with an icon and a label.

These widgets are building blocks that help you create the structure and appearance of your Flutter app. They work together to display your app's content and functionality in an organized manner.




