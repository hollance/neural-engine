# Why should I care about the ANE?

It's **much faster** than the CPU or GPU! And it's **more energy efficient**. 

For example, when running a model on real-time video, the ANE will not make the phone as hot and drains the battery much less quickly. Users will appreciate that.

Running your models on the ANE will leave the GPU free for doing graphics tasks, and leave the CPU free for running the rest of your app.

Consider this: Many [modern neural network architectures](https://machinethink.net/blog/mobile-architectures/) actually run faster on the CPU than on the GPU (when using Core ML). That's because iPhones have really fast CPUs! Plus, there is always a certain amount of overhead in scheduling tasks to run on the GPU, which may undo any speed gains.

Given these facts, should you run your neural network on the CPU instead of on the GPU? Well, probably no — you'll need the CPU for handling UI events, doing network requests, and so on... it's already busy enough. Better to hand off that work to a parallel processor such as the GPU — or even better, the ANE.

**Not all models can run on the ANE** because not all types of layers are supported. But if you have a model that *can* run on the ANE, you should prefer that over the GPU or CPU on devices that have one.

What if you have a model that cannot run on the ANE for some reason? It might be possible to tweak the model to make it compatible with the ANE anyway. See the other pages in this repo for tips to help with that.
