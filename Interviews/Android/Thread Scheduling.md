# Thread Scheduling

## Nice Values

Nice Values in Android are a measure of a thread's priority. Threads with a _higher_ nice value are _lower_ priority - they are being _nice_ to other threads.

The two most important priorities are `default` and `background`. The UI thread is given `default` priority.

In theory this would be enough but in practise this system is somewhat lacking - 20 background threads with one thread driving the UI would end up impacting the performance of the UI considerably, resulting in lag.

## Cgroups
To fix this issue, Android adopts foreground vs background scheduling from Linux using `cgroups` (control groups).

Threads with `background` priority are moved into a background `cgroup`, where they are limited to a small percentage of available CPU horsepower _if_ threads in other groups are busy. This lets background threads make _some_ progress without starving the UI, for instance.

Android also moves all threads belonging to applications that aren't currently in the foreground to the background - ergo, the currently focused application will always have priority.