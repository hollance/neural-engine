# Is my model using the ANE?

Even though you can use `MLModelConfiguration` to tell Core ML what your preferences are for using the CPU / GPU / ANE, there is no API to ask at runtime on which hardware it is currently running the model. 

Core ML may also split your model into multiple sections and run each using a different processor. So it could be using both the ANE *and* the CPU or GPU during the same inference pass.

## H11ANEServicesThread

While your app is running on the device, press the Pause button in the debugger. If there's a thread with the name **H11ANEServicesThread**, then Core ML is using the Neural Engine for at least some portion of your model.

## Try `computeUnits`

Change `MLModelConfiguration`'s `computeUnits` option from `.all` to `.cpuAndGPU` and `.cpuOnly`. 

If the performance of your model with `.all` isn't much faster than with the other options, Core ML may only be using the ANE for a portion of the model — or not at all.

## Breakpoints

One way to figure out which processor Core ML is running the model on, is to set a **symbolic breakpoint** and drop into the debugger.

Want to know if your model is being run on the ANE? Set a breakpoint on `-[_ANEModel program]` (Important: spell it exactly like that, with the dash in front.) If this breakpoint gets hit, Core ML is using the ANE.

However... Core ML may decide to run a portion of your model on the ANE and the rest on the GPU or the CPU. Just because your app hits `-[_ANEModel program]` doesn't mean the *entire* model runs on the ANE. To make sure, you need to set several other breakpoints.

Core ML uses three different "engines" that are implemented in the private Espresso framework:

- ANE — `Espresso::ANERuntimeEngine`
- GPU — `Espresso::MPSEngine` and `Espresso::MetalLowmemEngine`
- CPU — `Espresso::BNNSEngine`

It can switch between these engines when running your model. By looking at which engine name appears in the debugger's stack trace, you can see which engine / processor is currently being used.

To find out if the model (also) runs on the GPU or CPU, you can use the following symbolic breakpoints:

- `Espresso::MPSEngine::context::__launch_kernel`
- `Espresso::BNNSEngine::convolution_kernel::__launch`
- `Espresso::elementwise_kernel_cpu::__launch`

### Which symbols to look for?

The symbols mentioned above may change between iOS versions. To find other possible symbols that you can use for breakpoints, run your app on a device or the simulator and break into the debugger. Type the following at the debugger prompt:

```nohighlight
(lldb) image list Espresso
```

This prints the path to the private Espresso framework, something like this (it will be different on your machine):

```nohighlight
/Users/matthijs/Library/Developer/Xcode/iOS DeviceSupport/13.3 (17C54) arm64e/Symbols/System/Library/PrivateFrameworks/Espresso.framework/Espresso
```

Next, do the following:

```nohighlight
(lldb) image dump symtab 'put-the-path-here'
```

This dumps the entire symbol table from the Espresso framework. You should be able to find some interesting symbols in there. :-)

If all else fails, use one of the following breakpoints and manually step through the code with the debugger:

- `Espresso::layer::__launch`
- `Espresso::net::__forward`

If you end up in a function such as `Espresso::elementwise_kernel_cpu::__launch`, it's a pretty good hint that you're now running on the CPU.

## Instruments Time Profiler

If you're not sure which breakpoints to set, or you want to get some insights into how fast the different parts of your model are, run your app with the **Time Profiler** instrument.

I recommend making a new, empty app. Call your Core ML model 100 times or so in a loop. 

Run the app in Instruments with the Time Profiler template and open up the Call Tree. 

> **Tip:** Option-click on an item to expand everything below it. That will save you a bunch of clicking.

Find the symbol `-[MLNeuralNetworkEngine predictionFromFeatures:...]`. Right-click it, choose **Focus on subtree**.

Now you'll see all the functions that are being called during the execution of the model, and how much time they relatively take up. The names of these functions will give good clues as to where the model is being executed, and you can use them as breakpoints as well.

When using the ANE, there is also a call to `-[_ANEClient evaluateWithModel...]`. This appears to measure the time it takes to run the model on the ANE.
