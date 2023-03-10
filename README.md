<a name="top-anchor"/>

| [SCXML Wiki](https://alexzhornyak.github.io/SCXML-tutorial/) | [Forum](https://github.com/alexzhornyak/ScxmlEditor-Tutorial/discussions) |
|---|---|

# Qt SCXML Monitor
This project is a set of header-only files that help you to monitor your SCXML state machine written in Qt. Monitor events could be watched in [ScxmlEditor](https://github.com/alexzhornyak/ScxmlEditor-Tutorial) with pause-resume and breakpoints options.

## Qt [SCXML](https://alexzhornyak.github.io/SCXML-tutorial/) Debug Via SVG
It was an old dream to monitor state machine workflow without any external dependencies in Qt and finally it comes true. </b>
We prepared some native SCXML SVG monitors:
- [scxmlsvgview.h](scxmlsvgview.h) - for widgets (based on QGraphicsView)
    - see how to use it in [Dining Philosophers Example](https://github.com/alexzhornyak/SCXML-tutorial/tree/master/Examples/Qt/DiningPhilosophers)
- [scxmlsvgqmlitem.h](scxmlsvgqmlitem.h) - for QML (based on QQuickPaintedItem)
    - see how to use it in [Stopwatch Example](https://github.com/alexzhornyak/SCXML-tutorial/tree/master/Examples/Qt/StopWatch)

![StopWatchDemo](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/StopWatch_SvgMonitor.gif)

Since ScxmlEditor 2.2.1 you can export SCXML to SVG, include only monitor headers in your app and create monitor instances any time. 
> **NOTICE:** While state machine pointer is not set, the monitor **does nothing** and can be left in **Release**.

## Qt [SCXML](https://alexzhornyak.github.io/SCXML-tutorial/) External Debugging Monitor
Native QtCreator's scxml designer does not allow user to debug [SCXML statecharts](https://alexzhornyak.github.io/SCXML-tutorial/) and observe statemachine work flow, so we offer to use [ScxmlEditor]([../README.md](https://github.com/alexzhornyak/ScxmlEditor-Tutorial)) as an instrument for debugging complex SCXML state charts

### Description
We implemented Qt SCXML monitor in a single header [ScxmlExternMonitor2.h](scxmlexternmonitor2.h) as **UDPScxmlExternMonitor**. It has public a property **`QScxmlStateMachine *scxmlStateMachine`**. While **scxmlStateMachine** is not assigned it does nothing and you may leave it even in a release versions of your applications. When you need to observe statemachine work flow, just assign a valid **QScxmlStateMachine pointer** to the property, and monitor will start send UDP debug packages to the ScxmlEditor. And you will be able to observe when state is entered and when is exited, etc.

![example_debug](https://raw.githubusercontent.com/alexzhornyak/SCXML-tutorial/master/Images/StopWatchScxml.gif)

### 1. Usage in QML
#### 1.1. Option 1. From inherited state machine object
![opt1](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/ExternMonitor_QML1.png)

#### 1.2. Option 2. From QML object
##### Monitor registration
![opt2](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/ExternMonitor_QML2.png)
##### Usage in QML
![opt2_2](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/ExternMonitor_QML2_2.png)

### 2. Usage in C++ Qt Widgets
![cppOpt](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/ExternMonitor_CPP.png)

### 3. Import active states configuration
There is an option to export and import active states configuration. It may be useful when you are unable to use a remote debugger. You can export active states configuration to file and open it later with ScxmlEditor **`Import states configuration`** menu option.
#### Let's take a look at a simple example. 
Suppose that your deployed application does not work properly on the remote device.
- You can implement calling??[**`IScxmlExternMonitor`** method **`QStringList dumpAllActiveStates()`**](scxmlexternmonitor2.h) into your application. And it will save active states configuration by demand.
![ImportStatesConfiguration_MenuDump](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/ImportStatesConfiguration_MenuDump.png)

- Later you can transfer dump file to your working place

- Open the corresponding project with ScxmlEditor

- Call menu **`Import states configuration`**
![ImportStatesConfiguration](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/ImportStatesConfiguration.png)

- Select dump file in dialog
![ImportStatesConfiguration_Dialog](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/ImportStatesConfiguration_Dialog.png)

- Analyze active states
![ImportStatesConfiguration_Highlight](https://raw.githubusercontent.com/alexzhornyak/ScxmlEditor-Tutorial/master/Images/ImportStatesConfiguration_Highlight.png)

| [TOP](#top-anchor) | [SCXML Wiki](https://alexzhornyak.github.io/SCXML-tutorial/) | [Forum](https://github.com/alexzhornyak/ScxmlEditor-Tutorial/discussions) |
|---|---|---|
