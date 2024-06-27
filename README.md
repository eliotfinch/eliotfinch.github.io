# Page title

### Below is a test of some markdown with equations

Below we plot the real and imaginary parts. As an aside, we can work out the analytic form of these distributions by calculating the integral

\[ p_N(n) = \int_{-\infty}^\infty \int_{-\infty}^\infty \mathrm{d}A ~ \mathrm{d}\phi ~ p_A(A) ~ p_\phi(\phi) ~ \delta(g(A,\phi) - n) \]

where

$$p_A(A) = \frac{1}{\sqrt{2\pi \sigma^2}} \exp\left[-\frac{1}{2}\left( \frac{A}{\sigma} \right)^2\right], \quad \sigma = \sqrt{\frac{1}{2}S_n(f)T}$$

and

$$ p_\phi(\phi) = \frac{1}{2\pi} \quad \mathrm{for} \quad 0 < \phi < 2\pi, \quad 0\ \ \mathrm{otherwise.} $$

The function $g$ is the combination of $A$ and $\phi$ for which we want to know the probability distribution. For example, for the real part of $\tilde{n}(f)$ we have

$$ g(A,\phi) = \mathrm{Re}[Ae^{i\phi}] = A\cos{\phi} $$

The integral becomes

$$ p_N(n_r) = \int_{-\infty}^\infty \int_0^{2\pi} \mathrm{d}A ~ \mathrm{d}\phi ~ \frac{1}{\sqrt{2\pi \sigma^2}} \exp\left[-\frac{1}{2}\left( \frac{A}{\sigma} \right)^2\right] ~ \frac{1}{2\pi} ~ \delta(A\cos{\phi} - n_r) $$

To evaluate this, lets use the delta function to collapse the integral over $A$. To do this we must isolate the $A$ inside the dirac delta in the following way:

$$ \delta(A\cos{\phi} - n_r) = \frac{1}{|\cos{\phi}|} \delta \left(A - \frac{n_r}{\cos{\phi}} \right) $$

and the integral becomes

\begin{align} 
p_N(n_r) &= \frac{1}{2\pi\sqrt{2\pi \sigma^2}} \int_0^{2\pi} ~ \mathrm{d}\phi ~ \frac{1}{|\cos{\phi}|} ~ \exp\left[-\frac{1}{2}\left( \frac{n_r}{\sigma \cos{\phi}} \right)^2\right] \\
         &= \frac{1}{\pi\sqrt{2\pi \sigma^2}} \exp\left[ -\frac{1}{4} \left( \frac{n_r}{\sigma} \right)^2 \right] K_0\left[ \frac{1}{4} \left( \frac{n_r}{\sigma} \right)^2 \right]
\end{align}

where $K_0$ is the $n=0$ modified Bessel function of the second kind.

Does code scroll ona  mobile?

```python
# We could repeat the entire process multiple times and extract the single
# bin of interest, or to speed things up we can work in terms of a single
# frequency bin from the start. 

repeats = 1000000

# Create two arrays of normal samples - these now represent repeated instances
# of the noise in a single frequency bin
noise_prime_real = np.random.normal(size=repeats)
noise_prime_imag = np.random.normal(size=repeats)
noise_prime = (noise_prime_real + 1j*noise_prime_imag)/np.sqrt(2)

# Scale to get the frequency-domain noise instances in the chosen frequency
# bin
instances = np.sqrt(1/2)*np.sqrt(T)*asd_f*noise_prime

# The recovered mean of the squared magnitudes
print('Recovered mean squared magnitude =',np.mean(abs(instances)**2))
```
