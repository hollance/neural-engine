# How to replace unsupported layers

Here is a simple script that lets you replace `addBroadcastable` layers with plain old `add` layers. 

The broadcastable version was introduced in Core ML 3 and is more powerful, but [does not always work](unsupported-layers.md) on the ANE. In most situations, the old `add` layer performs the equivalent operation (it also supports broadcasting to some extent) and is compatible with the ANE. 

```python
import coremltools

model = coremltools.models.MLModel("YourModel.mlmodel")
spec = model._spec
nn = spec.neuralNetwork

# NOTE: If your model is a classifier, use the following:
# nn = spec.neuralNetworkClassifier

for layer in nn.layers:
    if layer.WhichOneof("layer") == "addBroadcastable":
        layer.add.MergeFromString(b"")

new_model = coremltools.models.MLModel(spec)
new_model.save("YourNewModel.mlmodel")
```

You may need to make other changes to your model as well. To learn how to edit mlmodel files, check out my e-book [Core ML Survival Guide](https://leanpub.com/coreml-survival-guide).
