# How do I make my model run on the ANE?

Core ML will try to run your model on the ANE whenever possible, but you can't *force* Core ML to use the ANE. 

When creating an instance of your Core ML model, you can pass in an `MLModelConfiguration` object:

```swift
let config = MLModelConfiguration()
config.computeUnits = .all

let model = try MyModel(configuration: config)
```

To allow the model to run on the ANE, use `computeUnits = .all`.

Note that this does not *guarantee* the model will run on the ANE, it just tells Core ML that you prefer to use the ANE if available.

If possible, Core ML will run the entire model on the ANE. However, it will switch to another processor when it encounters an unsupported layer. Even if Core ML could theoretically run the second part of the model on the GPU, it might actually decide to use the CPU. You can't assume anything here. (Note that the CPU can actually be faster than the GPU on many neural network operations, so it's not necessarily a bad thing.)
