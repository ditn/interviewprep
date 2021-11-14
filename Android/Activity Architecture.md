# Activity Architecture

When an application starts for the first time, the `AcitivtyManagerService` creates a special kind of window token (see [[Architecture Overview#Binder IPC]]) called an application window token. This uniquely identifies the application's top-level container window.

The `ActivityManager` gives this token to both the application and the `WindowManager`. Each time the application wants to add a new screen, it must send this token to the `WindowManager` again.

This ensures that it's impossible for one application to draw over another. It also makes it easier for the `ActivityManager` to request to close all of a token's windows, as the `WindowManager` will be able to correctly identify all of the affected windows.

