# Other weird issues

Stuff I or others have seen (anecdotal evidence):

- Using an mlmodel file that stores its weights as 16-bit floats appears to be slower than a model than uses 32-bit floats. On the GPU this makes no difference, as it always converts the weights to 16-bit floats anyway, but the Neural Engine seems to struggle with this. (I am not 100% sure what is going on here.)

- The A12 and later processors have a "smart compute system" that determines whether tasks should be run on the CPU, GPU, or ANE. So even if the model can run on the ANE without problems, Core ML may still decide to run it elsewhere, depending on what the system is doing. From [Twitter](https://twitter.com/eugenebokhan/status/1251423554861752320?s=20): "What we’ve also found out is that if NPU supports all the layers of the model and the GPU is resting, with a high probability CoreML will run it on GPU. But if GPU is heavy loaded with work - you can expect the model to be run on NPU."

- Even if all the layers in your model are compatible with the ANE, Core ML may still decide to run your model on the GPU. If you believe this is happening, split your model into two parts and see what happens to the first part. Does that run on the ANE now? I've seen it happen that, once the model becomes larger than a certain size, Core ML may decide that the GPU is more appropriate, even if the model could completely run on the ANE.

## Macbook Air vs Macbook Pro M1Max

Performance on densenet 121 is faster on Macbook Air than M1Max Macbook Pro. The difference is 4-5% with Monterey 12.3.1 and 13.3.1. Earlier version of Monterey and XCode had errors using ANE. The error was "H11ANEDevice::H11ANEDeviceOpen IOServiceOpen failed result= 0xe00002e2"
