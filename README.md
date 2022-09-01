# How to Use Stacked Architecture to Build a Flutter Counter App


<img src="How to Send Push Notifications to a Specific Device in Android Using Firebase (2).png" />


Flutter is a UI toolkit for building cross-platform applications. You can build Flutter apps using various state management techniques like the Stacked architecture.

This article will explain what Stacked architecture is and will guide you through creating a simple Counter App in Flutter with Stacked.

# Table of Contents
1. Intro to Flutter Widgets
2. Why Do You Need State Management Architectures in Flutter?
3. What is Stacked Architecture?
4. About the Counter App We Will be Building
5. How to Setup Flutter and the Counter
6. Summary


# Intro to Flutter Widgets

In Flutter, you use widgets to create various parts of the app's UI. In Flutter, a widget is a piece or unit of the user interface. A Flutter application is essentially a large tree of widgets. AppBar, Container, Icon, Image, Text, and other widgets are examples.

StatelessWidgets and StatefulWidgets are the two types of widgets in Flutter. In Flutter, StatefulWidgets are used to create widgets with State.
To notify Flutter that a state has changed in your application, use the **setState** function (available only within StatefulWidgets), and Flutter will rebuild the widget tree based on the changed state data.

Flutter's widgets do not change. They are unchangeable. Flutter efficiently paints UIs at 60 frames per second.

Flutter checks the widget tree at each frame paint. If any widgets change, Flutter removes them and replaces them with new widgets with the changed state.



# Why Do You Need State Management Architectures in Flutter?

setState is good. It is the best way to handle UI and state because it encourages declarative programming (which is the best way to code UIs).

However, as your Flutter codebase grows, you will notice that you will always use setState. Your Flutter app will have numerous widgets that rely on large amounts of changing state data. As a result, your code becomes clogged.

State management architectures used across frameworks and libraries aid in separation of concerns, clean code, and scaling. State management is also useful when multiple developers work on the same codebase. Architectures also aid in code testing.

Every widget in Flutter has a build method that returns its widget tree. The build method accepts a BuildContext from which it can access important app data or perform tasks such as navigation or dialogue display.

InheritedWidget is a built-in method for retrieving state from a widget further up the widget tree. It uses the BuildContext to get state from this higher widget.

ChangeNotifier is a Flutter class that does exactly what its name implies. It notifies listeners when its values change. You can extend this class by calling its notifyListeners() method, which you can then use to update the UI as needed. Popular state management options in Flutter use ChangeNotifier. For instance, Provider.


# What is Stacked Architecture?

Stacked is a modern Flutter state management framework that features excellent separation of concerns and dependency injection.

Separation of concerns entails keeping all UI code separate from logic code. This separation is critical for the long-term viability of your Flutter project.

Stacked architecture is functionally composed of only three parts. Services, ViewModels, and Views. Views are on top, closest to the user, ViewModels are beneath that, taking input from the Views, and Services are beneath that, which the ViewModels use to provide functionality. That's all. It comes with some rules that I strongly advise against breaking.

Dane Mackier founded Stacked, which is now maintained by the community. Dane Mackier is a Dart and Flutter GDE (Google Developer Expert). He built Stacked by combining the benefits of other popular state management architectures.

It should be noted that Stacked employs ChangeNotifier.


# About the Counter App We Will be Building

To keep things simple, we'll use Stacked architecture to create a one-screen Counter App.

If there are no values, the app will display a Zero. However, if the user increases the value, it will be displayed.

We'll also have a floating action button (with a plus icon) to add and subtract value.

<p float="left">
  <img src="Screenshot 2022-09-01 at 10.16.44 AM.png" width="500" />
  <img src="Screenshot 2022-09-01 at 10.16.23 AM.png" width="500" /> 
  
</p>

# How to Setup Flutter and the Counter
## 1. Install Flutter

First, you'll need to have Flutter installed and working properly. If you do, you can get to step two. You can also get to step two if you don't want to follow along.

If you don't have Flutter installed, install it by following the steps for your operating system here.

Run the flutter doctor -v command in your terminal. If all the listed options have a good check or green color, then you are good to continue. If any of the results have errors, search the error online and you'll find solutions to the problem.

## Create the Flutter Project

Run the following command to create a new Flutter project:

```
flutter create counter_app 
```

## 3. Add the Packages

We need to add the stacked Flutter package to project. It will provide us with necessary classes (like ViewModels), given that we are building with the Stacked Architecture.

```
flutter pub add stacked
```

## Folder Structure

Make a new folder called ui in the lib folder. Create a new folder within that folder called views, and within that folder, a new folder called counter. Create two new files in the counter folder: counter screen and counter model. The FilledStacks team pointed out to me that having the view and the ViewModel in the same folder makes more sense, so that's what we'll be doing from now on.

<img src="Screenshot 2022-09-01 at 12.20.09 PM.png" width="500" />

The counter_view will have the basic code for associating a view with a ViewModel.

<img src="Screenshot 2022-09-01 at 12.47.00 PM.png" width="500" />

The builder provides the UI that will be "built from" the ViewModel. As you see we're using the .reactive named constructor. This indicates that the builder will be called to rebuild the UI every time notifyListeners is called in the ViewModel. There's also a constructor .nonReactive which will only build the UI once and it won't rebuild when notifyListeners is called in the ViewModel. The ViewModel looks as follows.

<img src="Screenshot 2022-09-01 at 12.50.10 PM.png" width="500" />

We'll add a Floating Action button to the view and call the increment and decrement functions from the onPressed event. Make the following changes to the CounterScreen build function.

If you run the code now and press the floating action button, the text will update as the counter changes. That's the fundamentals of the View to ViewModel relationship, as well as the foundation of this architecture's state management. When you update a property or variable that your widget will use, you call notifyListener, and your UI is rebuilt with the new ViewModel state. The navigation will be set up next.


## Run the Counter App

You should be able to run the above app on a preconfigured device if you are using a Flutter-enabled IDE.

If you are not, no worries; simply execute the following command in the same terminal. Alternatively, ensure that you are in the same project folder in the terminal before running the command:

```
flutter run
```

It should run the Flutter app on an available device or ask you to choose a device and then run the application on it.

You should be able to add and subtract numbers.

 <img src="Screenshot 2022-09-01 at 10.16.44 AM.png" width="500" />
 
 # Summary
 
 State Management architectures are useful for organising Flutter projects. They are optional, but they may become necessary if you are developing a complex application or if multiple people are contributing to the same codebase.

These architectures figure out how to update the UI without using the standard setState calls (). One such architecture is stacked. It updates the UI using notifyListeners().
A key feature of Stacked is carrying out crucial services like navigation without the BuildContext.


