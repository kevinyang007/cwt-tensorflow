# Tensorflow CWT
This implements a 1-D Continuous Wavelet Transform (CWT) using a Ricker wavelet in tensorflow. It is very similar to scipy's cwt routine, excpet is slightly limited yet much faster.

It has the advantage of running in parallel on a GPU and is about 8x faster than an old laptop i5 using a GTX 750 TI (~1,400 GFLOPS). This is done by using tensorflow's parallel while_loop function.

One caveat of using this is the accuracy. Currently this api and scipy's cwt both limit the Ricker wavelet samples to 10x the scale size. What this means for both libarires is that they are both much faster at the cost of a very small numerical error.

See test.py for plotting the result and the cwtRicker function type in cwt.py.

## Usage
Run [test.py](https://github.com/nickgeoca/cwt-tensorflow/blob/master/test.py) example. It produces the plot below.
![](https://github.com/nickgeoca/cwt-tensorflow/blob/master/mortletCWT.png)

## TODO
* Add this line of code similar to scipy's [cwt](https://github.com/scipy/scipy/blob/63bcdc4eeafa59553c00e44343dbb38380bd9d45/scipy/signal/wavelets.py#L362): samples = min(10*width, len(wav))
* consier scipy's ability to specify the wavelet scale
```python
# Scipy's cwt can specify the wavelet scales in detail. This api can't do that.
cwt(wav, signal.ricker, [1,1.5,2,2.5,3])
# This api is equivilent to calling scipy's cwt as below.
cwt(wav, signal.ricker, range(1,n))
```
* Maybe add 2d verison
