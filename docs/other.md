# Other weird issues

Stuff I have seen but can't confirm whether it's really true or not:

- Using an mlmodel file that stores its weights as 16-bit floats appears to be slower than a model than uses 32-bit floats. On the GPU this makes no difference, as it always converts the weights to 16-bit floats anyway, but the Neural Engine seems to struggle with this. (I am not 100% sure what is going on here.)
