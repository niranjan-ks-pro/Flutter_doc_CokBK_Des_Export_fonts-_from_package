# export_fonts_from_a_package

A new Flutter project. Not working:

Error : " Resolving dependencies...
The current Dart SDK version is 3.0.5.

Because export_fonts_from_a_package depends on awesome_package any which doesn't support null safety, version solving failed.

The lower bound of "sdk: '>=2.0.0-dev.68.0 <3.0.0'" must be 2.12.0 or higher to enable null safety.
For details, see https://dart.dev/null-safety "

Export fonts from a package
===========================

1.  [Cookbook](https://docs.flutter.dev/cookbook)
2.  [Design](https://docs.flutter.dev/cookbook/design)
3.  [Export fonts from a package](https://docs.flutter.dev/cookbook/design/package-fonts)

Rather than declaring a font as part of an app, you can declare a font as part of a separate package. This is a convenient way to share the same font across several different projects, or for coders publishing their packages to [pub.dev](https://pub.dev/). This recipe uses the following steps:

1.  Add a font to a package.
2.  Add the package and font to the app.
3.  Use the font.

info Note: Check out the [google_fonts](https://pub.dev/packages/google_fonts) package for direct access to almost 1000 open-sourced font families.

[](https://docs.flutter.dev/cookbook/design/package-fonts#1-add-a-font-to-a-package)1\. Add a font to a package
---------------------------------------------------------------------------------------------------------------

To export a font from a package, you need to import the font files into the `lib` folder of the package project. You can place font files directly in the `lib` folder or in a subdirectory, such as `lib/fonts`.

In this example, assume you've got a Flutter library called `awesome_package` with fonts living in a `lib/fonts` folder.

content_copy

```
awesome_package/
  lib/
    awesome_package.dart
    fonts/
      Raleway-Regular.ttf
      Raleway-Italic.ttf

```

[](https://docs.flutter.dev/cookbook/design/package-fonts#2-add-the-package-and-fonts-to-the-app)2\. Add the package and fonts to the app
-----------------------------------------------------------------------------------------------------------------------------------------

Now you can use the fonts in the package by updating the `pubspec.yaml` in the *app's* root directory.

### [](https://docs.flutter.dev/cookbook/design/package-fonts#add-the-package-to-the-app)Add the package to the app

To add the `awesome_package` package as a dependency, run `flutter pub add`:

content_copy

```
$ flutter pub add awesome_package

```

### [](https://docs.flutter.dev/cookbook/design/package-fonts#declare-the-font-assets)Declare the font assets

Now that you've imported the package, tell Flutter where to find the fonts from the `awesome_package`.

To declare package fonts, prefix the path to the font with `packages/awesome_package`. This tells Flutter to look in the `lib` folder of the package for the font.

content_copy

```
flutter:
  fonts:
    - family: Raleway
      fonts:
        - asset: packages/awesome_package/fonts/Raleway-Regular.ttf
        - asset: packages/awesome_package/fonts/Raleway-Italic.ttf
          style: italic

```

[](https://docs.flutter.dev/cookbook/design/package-fonts#3-use-the-font)3\. Use the font
-----------------------------------------------------------------------------------------

Use a [`TextStyle`](https://api.flutter.dev/flutter/painting/TextStyle-class.html) to change the appearance of text. To use package fonts, declare which font you'd like to use and which package the font belongs to.

content_copy

```
child: Text(
  'Using the Raleway font from the awesome_package',
  style: TextStyle(
    fontFamily: 'Raleway',
  ),
),
```

[](https://docs.flutter.dev/cookbook/design/package-fonts#complete-example)Complete example
-------------------------------------------------------------------------------------------

### [](https://docs.flutter.dev/cookbook/design/package-fonts#fonts)Fonts

The Raleway and RobotoMono fonts were downloaded from [Google Fonts](https://fonts.google.com/).

### [](https://docs.flutter.dev/cookbook/design/package-fonts#pubspecyaml)`pubspec.yaml`

content_copy

```
name: package_fonts
description: An example of how to use package fonts with Flutter

dependencies:
  awesome_package:
  flutter:
    sdk: flutter

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  fonts:
    - family: Raleway
      fonts:
        - asset: packages/awesome_package/fonts/Raleway-Regular.ttf
        - asset: packages/awesome_package/fonts/Raleway-Italic.ttf
          style: italic
  uses-material-design: true

```

### [](https://docs.flutter.dev/cookbook/design/package-fonts#maindart)`main.dart`

content_copy

```
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      title: 'Package Fonts',
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  const MyHomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // The AppBar uses the app-default font.
      appBar: AppBar(title: const Text('Package Fonts')),
      body: const Center(
        // This Text widget uses the Raleway font.
        child: Text(
          'Using the Raleway font from the awesome_package',
          style: TextStyle(
            fontFamily: 'Raleway',
          ),
        ),
      ),
    );
  }
}
```
