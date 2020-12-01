# Is the ANE 16-bit?

It appears so. 

When you run a Core ML model on the CPU, it uses float32 for all its calculations and for storing the intermediate tensors. (As of iOS 14 and macOS 11, Core ML can also use float16 on the CPU.)

On the GPU it uses float16 for the weights and the intermediate tensors, but float32 for the calculations. You can turn this off with the option `allowLowPrecisionAccumulationOnGPU` from `MLModelConfiguration`, in which case the GPU also uses float16 for the calculations. This is a bit faster but you may lose precision.

The ANE appears to use float16 for everything. This means that if your model has activations that are relatively large (`> 1e2`) or relatively small (`< 1e-4`), you will lose precision. Or worse, the model may not actually work correctly at all — i.e. very small numbers become 0.

## Multiprecision

Apple claims that the ANE in the A12 Bionic has "multiprecision" support. This is also known as variable precision.

TODO: Look into what this actually means.

## Quantized operations

Core ML has support for quantizing weights using 8-bit or smaller integers. However, it appears this is just for storing the weights in the mlmodel file. In theory, an NPU can perform operations such as convolution directly with quantized weights, but there is no evidence to suggest the ANE currently does this.

As of iOS 14 and macOS 11, Core ML does support 8-bit operations but only for the matrix multiplication layers, not for convolution layers or other operations. It's unknown whether such 8-bit operations are actually performed on the ANE or only on the CPU.
