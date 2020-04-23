# Which Core ML layers are not supported by the ANE?

The main reason why Core ML will not run a model on the ANE is because the model contains certain layer types.

It is possible that Core ML runs the first part of your model on the ANE, and then switches to GPU (or CPU) to run the rest of the model. In theory it could make several of these switches, but every switch between devices involves overhead.

If your model is `S → U → S → U → S → U` where S is a supported layer and U an unsupported layer, Core ML will probably do `ANE → GPU` just once instead of `ANE → GPU → ANE → GPU → etc`. (Although `ANE → CPU → ANE → CPU → etc` does seem to happen...)

However, Core ML is mostly a black box. We have no insight into how Core ML makes the decision to run which part of the model on which processor. The only way to find out is to [set some breakpoints](is-model-using-ane.md) and try it out.

**Tip:** If your model has just one or two layers that are unsupported by the ANE, it's smart to [edit the mlmodel file](https://leanpub.com/coreml-survival-guide) and replace those layers with an alternative that *does* work on the ANE. Running the entire model on the ANE will make your model much faster and more energy efficient.

## Problematic layers

This list is by no means exhaustive, but the following layer types are known to not work on the ANE:

- RNN layers such as LSTM or GRU
- gather
- dilated convolutions
- broadcastable and "ND" layers
- custom layers

> **Note:** Some of these are guesses. It's hard to tell what Core ML is *really* up to half the time.

## Broadcastable layers

Core ML 3 [added a number of new layers](https://machinethink.net/blog/new-in-coreml3/) that support broadcasting, such as:

- `AddBroadcastableLayer`
- `DivideBroadcastableLayer`
- `MultiplyBroadcastableLayer`
- `SubtractBroadcastableLayer`
- and a number of others...

There are also new layers that have "ND" in their name, signifying that they can run on tensors of any rank:

- `ConcatNDLayer`
- `SplitNDLayer`
- and so on...

These layers will not run on the ANE. When it encounters such a "broadcastable" or "ND" layer type, Core ML will fall back to the CPU or GPU.

The good news is: Most of the time you don't actually need these new layer types! They are mostly useful for when your tensors don't have the usual `(batch, channels, height, width)` shape.

You can often replace these broadcastable layers with older layer types from Core ML 2. These still allow a limited amount of broadcasting. And they mostly work fine on the ANE.

The problem is that the TensorFlow and ONNX converters have a tendency to prefer these new broadcastable layers, when you use the argument `minimum_ios_deployment_target='13'`.

When that happens, and your model does not [run on the ANE](is-model-using-ane.md), you can perform some [model surgery](https://leanpub.com/coreml-survival-guide) and replace these layers with the older versions:

- `AddBroadcastableLayer` → `AddLayer`
- `MultiplyBroadcastableLayer` → `MultiplyLayer` or `ScaleLayer` or a linear `Activation` layer
- `ConcatND` → `Concat`
- and so on...

There may not always be a compatible old-style layer available — for example, there is no `SubtractLayer` that can replace `SubtractBroadcastableLayer` — so you may need to be clever and introduce extra layers as a workaround (e.g. negate the contents of the tensor using a linear activation layer with alpha = -1, followed by `AddLayer`).

## Custom layers

[Custom layers](https://machinethink.net/blog/coreml-custom-layers/) let you add new functionality to Core ML. But there's a downside: you can only provide a CPU and GPU implementation. Because there is no public API to [program the ANE](programming-ane.md), custom layers cannot run on the ANE.

If the custom layer occurs near the end of your model, it might make sense to split up the model into two parts and run them one after the other. The first part can use the ANE, while the second part that has the custom layer in it, will use the CPU or GPU. That's likely to be faster than running the entire thing on the CPU or GPU.

## Layers that do work

- upsampling: Recently I worked with a model where upsampling layers appeared to run just fine on the ANE (Core ML also has a `Espresso::ANERuntimeEngine::upsample_kernel`), so I guess these do work.

- deconvolution

## More?

I haven't yet tried out all possible Core ML layer types on the ANE (it's a lot of work!). If you know of any layers that have problems with the ANE, please [send some feedback](https://github.com/hollance/neural-engine/issues). Thanks!
