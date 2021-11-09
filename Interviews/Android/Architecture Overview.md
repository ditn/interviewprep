# Architecture Overview

Android is made up of several layers:

### Applications
This is where your app lives, and is the top layer in the software stack.

### Application Framework
This layer provides high-level services to applications in the form of Java classes. This includes:

- **Activity Manager**, which controls application lifecycle and Activity stacks
- **Content Providers**, which allow applications to publish and share data with other applications
- **Resource Manager**, providing access to resources such as Strings, colors, layouts etc

### Binder IPC
The [Binder Inter-Process Communication](https://www.androiddesignpatterns.com/2013/07/binders-window-tokens.html) mechanism allows the Application Framework  to cross process boundaries (Android runs all apps with process isolation) and call into the Android system services code. This enables high-level code to interact with the System Server and other remote service components. At the application framework level, this communication is hidden from the developer and things "just work".

`Intents`, `ContentProviders` and `Messengers` are built ontop of Binder, as they enable communication across processes. When a process sends a message to another process, the kernel allocates space in the destination process's memory and copies the message data directly from the sending process. It then queues a message which tells the receiver where the message data is.

Each `Binder` object has a unique reference in memory and this is used for security as it can act as an identifier token - noone is able to create another `Binder` with the same identifier. For instance, calling `PowerManagerService` to acquire a `WakeLock` requires a token - releasing that `WakeLock` requires the same token. This way, one application or process cannot pretend to be another and interfere.

A good example of this is in the `View` class, where `getWindowToken()` is called extensively. This is a `Binder` token, and is used to ensure that malicious applications aren't allowed to draw ontop of other applications.

### Android Runtime
This is part of the third layer along with Android libraries. ART uses AOT compilation to translate DEX bytecode down to native instructions in Executable & Linkable Format (ELF)

### Android Libraries 
Encompasses Java-based libraries available to Android apps. This includes packages such as:
- android.app
- android.content
- android.database
- android.os
- android.net
- android.text
- android.view
- android.widget
- android.webkit

These by and large are Java wrappers over C++ - not a tonne of logic here.

### HAL
The Hardware Abstraction Layer sits ontop of the kernel, and is responsible for:

- Camera
- Audio
- Graphics
- And more

It defines a standard interface for manufacturers to implement which allows Android to be agnostic about lower-level driver implementations.

### Linux Kernel and Libraries
Onotop of the kernal there's a set of libraries in C++ such as WebKit, SQLite, SSL etc. The kernel provides abstraction over device hardware and contains drivers, networking, memory management etc.