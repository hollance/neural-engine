# Use os_log to look at warning / error messages

It's possible that Core ML prints an error message such as "[coreml] Error computing NN outputs -1" or "Error plan build: -1" to the console. Unfortunately, such messages aren't very helpful in diagnosing what's causing the error.

To get more useful messages, run your app in **Instruments using the os_log instrument**. Core ML will print more information here.

This is also useful for figuring out if all the layers in your model are supported on the ANE. If not, Core ML will likely print a message about it.

You can also download the logs from your device and examine them. For example, to download the last 1 day (`1d`) worth of logs:

```nohighlight
$ sudo log collect --device --last 1d
```

This creates a folder `system_logs.logarchive`. You can double-click this to open it in the Console app and then search for `coreml` or `espresso`.

Using the command-line:

```nohighlight
$ log show --archive system_logs.logarchive --predicate '(subsystem IN {"com.apple.espresso","com.apple.coreml"}) && (category IN {"espresso","coreml"})' --info --debug --last 1d
```

The logs will show `<private>` for the names of the model and its layers, but you can work around this by [installing a device profile](https://superuser.com/questions/1532031/how-to-show-private-data-in-macos-unified-log) on your Mac.

If you're running Core ML on the Mac, you can use `log stream` to view the log messages related to Core ML in realtime:

```nohighlight
$ log stream --predicate '(subsystem IN {"com.apple.espresso","com.apple.coreml"}) && (category IN {"espresso","coreml"})' --info --debug
```
