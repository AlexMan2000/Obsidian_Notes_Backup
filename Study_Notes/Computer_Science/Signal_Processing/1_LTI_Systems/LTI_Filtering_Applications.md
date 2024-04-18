# Edge Detection
## Definition
> [!def]
> The canonical definition of the 1D Edge Detector is: $$y[n]=x[n]-x[n-1]$$ so the inpulse response of this system is $$h[n]=\delta[n]-\delta[n-1]$$. Given this, now if we have an arbitrary input signal $x[n]$, we could derive the output $y[n]$ by convolution $$(x*h)[n]$$
> 
> This filter, applied to the signal, can extract out the sharp increase or decrease in the magnitude of the signal.



## Applications on PCS
### Piecewise Constant Signal
> [!def]
> Suppose we have the following input signal:
> ![](LTI_Filtering_Applications.assets/image-20240417163837057.png)
> Each $n$ correspond to a unique $k$ such that $\delta[n-k]=1$ where $n=k$.
```python
n = np.arange(0, 21)
h = np.array([1, -1])
x = np.array([0,0,0,0,0,1,1,1,1,1,3,3,3,3,2,2,2,2,2,0,0])
y = np.convolve(x, h, "same") # filtered version of x

# Plot results
plt.figure(figsize=(16, 8))

plt.subplot(2, 1, 1)
plt.stem(n, x)
plt.ylim([0, 3.5])
plt.title("Piecewise Constant Signal $x[n]$")

plt.subplot(2, 1, 2)
plt.stem(n, y)
plt.ylim([-2.5, 2.5])
plt.title("1D Edge Detector Output for $x[n]$")

plt.show()
```
> [!code] Output
> ![](LTI_Filtering_Applications.assets/image-20240417164138115.png)
> We can see that if we apply the 1D Edge detector filter to the piecewise continuous signal, the output would show the discontinuity point with its direction.
> - We see that the original signal changes 4 times, from 0 -> 1, 1 -> 3, 3-> 2, and finally 2 -> 0. Then the edge detector extracts 4 sharp change in the original signal and output 4 non-zero value.



### Sparse Signals
> [!def]
> One of the hottest areas of signal processing in the past ~15 years has been the study of sparse (mostly zero) signals, including both acquisition and representation, known as *compressed sensing*. 
> - A key part of compressed sensing algorithms is applying some *sparsifying transform* to signals that retain all the signal's information (i.e., the original signal could be completely recovered from the transformed one) but result in a new signal that is **mostly zero**.
> 
> Suppose you're interested in developing compressed sensing algorithms for piecewise constant signals, and are in need of a way to sparsify them. How would you do so by only using the first signal value, $x(0)$, and using an LTI filter of your choice as the sparsifying transform? Explain both what LTI filter you would use, and how to recover the original signal from the filtered one. You can ignore noise that would be present for real world signals — assume the signal truly is piecewise-constant like the ones above. Also, you may assume $x(n) = 0$ for $n < 0$, since this is basically what we're doing in the digital setup.
> -  We could define a difference equation where $x[n]=y[n]+x[n-1]$ where $x[n]$ is the original signal and $y[n]$ is the compressed signal(sparse).
> - $x[0]=y[0]$



### Moving Difference 
> [!example] Ramp Signal
> ![](LTI_Filtering_Applications.assets/image-20240417165629846.png)
```python
# TODO your code here
n = np.arange(51)
h = np.array([1, -1])
x = np.array([(n[i]**2) for i in range(len(n))]) # x = n^2
y = np.convolve(x, h, mode="valid")

# Plot results
plt.figure(figsize=(16, 8))

plt.subplot(2, 1, 1)
plt.stem(x)
plt.title("Piecewise Constant Signal $x[n]$")

plt.subplot(2, 1, 2)
plt.stem(y)
plt.title("1D Edge Detector Output for $x[n]$")

plt.show()
```
> [!code] Output
> ![](LTI_Filtering_Applications.assets/image-20240417171409781.png)
> **Q:** A ramp signal linearly increases. You should see in your plot that a 1D edge detector, or moving difference, outputs a constant signal when given a ramp as its input. What real function ($f(t) = ?$) does the ramp remind you of? What is that function's derivative (what's $f'(t)$)? How does the derivative for it match up against the edge detector's output?
> **A:** $f(t)=t, f'(t)=1$

> [!example] Quadratic Signal
> ![](LTI_Filtering_Applications.assets/image-20240417171453910.png)
```python
# TODO your code here
n = np.arange(51)
h = np.array([1, -1])
x = np.array([(n[i]**2) for i in range(len(n))]) # x = n^2
y = np.convolve(x, h, mode="valid")

# Plot results
plt.figure(figsize=(16, 8))

plt.subplot(2, 1, 1)
plt.stem(x)
plt.title("Piecewise Constant Signal $x[n]$")

plt.subplot(2, 1, 2)
plt.stem(y)
plt.title("1D Edge Detector Output for $x[n]$")

plt.show()
```
> [!code] Output
> ![](LTI_Filtering_Applications.assets/image-20240417171516258.png)
> **Q:** Same question as before. You should see in your plot that a 1D edge detector, or moving difference, outputs a ramp signal when given a quadratic as its input. What real function ($f(t)=?$) does the quadratic remind you of? What is that function's derivative (what's $f'(t)$)? How does the derivative for it match up against the edge detector's output?
> **A:**  $f(t)=t^2$ and $f'(t)=2t$.





## Applications on Noisy Signals
> [!bug] Caveats
> When applied on gaussian noise signals, we notice that the edge detector filter neither amplifies nor supresses the original signal, which doesn't give us much information about the original signal.
> 
> So a good practice before applying edge detector is to denoise the signal first.
> ![](LTI_Filtering_Applications.assets/image-20240417171953142.png)




# Data Smoothing
## SMA
> [!def]
> 





