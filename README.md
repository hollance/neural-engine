# The Neural Engine — what do we know about it?

Most new iPhones and iPads have a **Neural Engine**, a special processor that makes machine learning models really fast, but not much is publicly known about how this processor actually works.

The Apple Neural Engine (or ANE) is a type of **NPU**, which stands for Neural Processing Unit. It's like a GPU, but instead of accelerating graphics an NPU accelerates neural network operations such as convolutions and matrix multiplies. 

The ANE isn't the only NPU out there — many companies besides Apple are developing their own AI accelerator chips. Besides the Neural Engine, the most famous NPU is [Google's TPU](https://en.wikipedia.org/wiki/Tensor_processing_unit) (or Tensor Processing Unit).

## Why this document?

I provide [ML consulting services for iOS](https://machinethink.net/hire) and often get email from people who are confused why their model doesn't appear to be running on the Neural Engine, or **why it is so slow** when the ANE is supposed to be way faster than the GPU...

It turns out that **not every Core ML model can make full use of the ANE**. The reason why can be complicated, hence this document tries to answer the most common questions. 

The ANE is great for making ML models run really fast on iPhones and iPads. A model that is optimized for the ANE will seriously outperform the CPU and GPU. But the ANE also has limitations. Unfortunately **Apple isn't giving third-party developers any guidance** on how to optimize their models to take advantage of the ANE. It's mostly a process of trial-and-error to figure out what works and what doesn't.

> **Note:** Everything here was obtained by experimentation. I do not work at Apple and never have, so I am not privy to any implementation details of this chip. Some of this information is probably wrong. It's definitely incomplete. If you know something that isn't explained here, or if you find information that is wrong or missing, please [file an issue](https://github.com/hollance/neural-engine/issues) or [make a pull request](https://github.com/hollance/neural-engine/pulls). Thanks!

If you want to learn more about Core ML in general, I've also written the [Core ML Survival Guide](https://leanpub.com/coreml-survival-guide), an e-book full of tips & tricks about Core ML. Also check out [my blog about ML on mobile](http://machinethink.net/blog).

I was originally planning to make this a blog post but decided to put it on GitHub to make it a community resource and so that other people could contribute to it too. Please do!

## Table of contents

- [Which devices have an ANE?](docs/supported-devices.md)
- [Why should I care about the ANE?](docs/why-care.md)
- [How do I make my model run on the ANE?](docs/running-on-ane.md)
- [How do I prevent my model from running on the ANE?](docs/prevent-running-on-ane.md)
- [Is my model using the ANE?](docs/is-model-using-ane.md)
- [Can I program the ANE directly?](docs/programming-ane.md)
- [Isn't the ANE the same as the GPU?](docs/ane-vs-gpu.md)
- [Is the ANE 16-bit?](docs/16-bit.md)
- [Which Core ML layers are not supported by the ANE?](docs/unsupported-layers.md)
- [How to replace unsupported layers](docs/model-surgery.md)
- [How does the ANE work internally?](docs/internals.md)
- [Other weird issues](docs/other.md)
