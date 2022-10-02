### Notes on Book Code Base

#### Matlab dependency issues:
- Many files require the CVX toolbox, so I have prepended these a commented link to the download page
- CH01_SEC09_Tensor uses the parafac() function, which is not defined anywhere. As best I can tell it comes from this toolbox, so I've included a link to that: https://www.mathworks.com/matlabcentral/fileexchange/1088-the-n-way-toolbox

#### Files not translated into Python:
- CH02_SEC04_2_SpectrogramBeethoven: Seems like the existing packages for importing an MP3 into Python are a little sketchy. Could pretty easily implement this if we provided a .wav music file instead, but I have skipped it for now .
- CH06_SEC01_1_NN: SKLearn does not have an obvious analogue to Matlab's patternnet(). The network would probably have to be built manually in Torch.
- CH06_SEC06_1_NNLorenz: There doesn't seem to be any obvious translation of Matlab's feedforwardnet() into Keras (specifically, its use of Levenberg-Marquardt backpropagation).
- CH08_SEC07_3_LQG_Simulink: Uses Simulink and C wrappers; translation into Python might be kind of an ordeal
- CH09_SEC02_2_BalancedTruncation: The system used here is unstable (eigenvalues with real part > 0). Matlab's control toolbox seems to have built-in methods to deal with this (e.g. hsvd() returns the stable singular values and gives 'Inf' for the unstable ones). The Python control module lacks these safeguards. I tried to work around it, but the impulse response plots that come out at the end are still unstable. Also, the hsvd() function in the Python module has not yet been implemented for discrete systems, so that would need to be written from scratch
- CH09_z_extra_BT_ERA_OKID: Same system as the BalancedTruncation file, so same issues.
- CH10_SEC02_GA_PID: I played around some with the most widely-used genetic programming toolbox for python (DEAP). I'm sure it's capable of reproducing this, but it will be a fairly nontrivial process to translate (there isn't any function as straightforward as Matlab's ga())
- CH10_SEC03_Krstic_ex1p3: Uses Simulink

#### Files where there may be some outstanding translation issues:
- CH04_SEC07_2_RegressAIC_BIC: The python module I used for these ARMA processes gives different results for AIC and BIC than the Matlab code. There is probably something subtly different going on under the hood of these functions, but it's not clear to me what it is

#### Matlab issues that made their way into print:
- CH06_SEC04_1_StochasticGradientDescent: The stochastic gradient descen loop uses two index variables which are called ind1,ind2 in one line and i1,i2 in another. This error appears in the printed code in the book and is reflected in Fig. 6.11 (although the visual difference is fairly subtle and subject to stochastic variation anyway)

#### Matlab “production” files
