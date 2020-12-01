# How do I prevent my model from running on the ANE?

Instantiate your model as follows:

```swift
let config = MLModelConfiguration()
config.computeUnits = .cpuAndGPU

let model = try MyModel(configuration: config)
```

This tells Core ML it can only use the CPU or the GPU, but not the ANE.

You can also use `computeUnits = .cpuOnly` if you don't want to use the GPU but always force the model to run on the CPU.

Why would you need to prevent Core ML from using the ANE? Perhaps you're trying to run multiple models at the same time and you want one of them to use the ANE while the others use the GPU and CPU. But most of the time I need to use this feature it is because of bugs in Core ML — some models give strange errors when you try to run them on the ANE but run fine on the GPU or CPU.
