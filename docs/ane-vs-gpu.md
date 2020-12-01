# Isn't the ANE the same as the GPU?

The ANE and the GPU are two separate processors. They are located on the same die together with the CPU cores, but they are separate things.

Here is what the A12 Bionic looks like (picture from [anandtech.com and TechInsights](https://www.anandtech.com/show/13393/techinsights-publishes-apple-a12-die-shot-our-take)). As you can see, the ANE (labeled NPU here) and the GPU cores are separate areas on the chip.

![The A12 die](https://images.anandtech.com/doci/13393/A12.jpg)

To program the GPU you need to use **Metal**, Apple's GPU programming language. Besides graphics shaders, Metal also allows you to write compute shaders. 

Both iOS and macOS provide **Metal Performance Shaders** (MPS), a framework that has pre-built shaders for many image processing tasks. MPS also has compute shaders for neural network operations such as convolutions. In fact, when Core ML runs your model on the GPU, it uses MPS under the hood. 

Metal cannot be used to program the ANE, it's exclusively for the GPU. There is currently no public framework for directly programming the ANE.

Core ML uses the following frameworks for the different processors:

- **CPU:** BNNS, or Basic Neural Network Subroutines, a part of Accelerate.framework
- **GPU:** Metal Performance Shaders (MPS)
- **ANE:** private frameworks

Core ML can split up a model so that one part runs on the ANE and another part on the GPU or CPU. It switches between these different frameworks when it does that.

iPhones, iPads, and Apple Silicon Macs have **shared memory**, which means that the CPU, GPU, and ANE all use the same RAM. The advantage of shared memory is that you don't need to upload data from one processor to the other. But that doesn't mean switching between processors has no cost: the data still needs to be converted into a suitable format. For example, on the GPU the data needs to be put into a texture object first.

On Intel-based Macs, the GPU may have its own RAM (often called VRAM).
