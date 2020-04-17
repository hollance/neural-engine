# How do I prevent my model from running on the ANE?

Instantiate your model as follows:

```swift
let config = MLModelConfiguration()
config.computeUnits = .cpuAndGPU

let model = try MyModel(configuration: config)
```

This tells Core ML it can only use the CPU or the GPU, but not the ANE.

You can also use `computeUnits = .cpuOnly` if you don't want to use the GPU but always force the model to run on the CPU.
