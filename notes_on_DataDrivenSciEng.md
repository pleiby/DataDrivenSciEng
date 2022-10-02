Notes on Data Driven Science and Engineering
=================================================

- Author: Paul Leiby
- File: notes_on_DataDrivenSciEng.md

- [ ] Complete Course & Book for Brunton & Kutz Data Driven Science & Engineering"
	- see pdf book [Brunton&Kutz2017 Data Driven Science & Engineering](http://databookuw.com/databook.pdf) (partial Chapters?) 
		- local file "Brunton&Kutz2017 Data Driven Science & Engineering - databook.pdf"
	- see videoseries YouTube playlist [Data Driven Science and Engineering](https://www.youtube.com/playlist?list=PLMrJAkhIeNNRpsRhXTMt8uJdIGz9-X_1-)
		- [ ] Particularly lectures 41:61 on FT and FFT
		- [ ] See [DatabookUW website (with chapters, code, and videos)](http://databookuw.com/)
		- Book Website: http://databookuw.com 
		- Book PDF: http://databookuw.com/databook.pdf
- [ ] SVD for data/dimensionality reduction
	- As a "data-driven generalization of the Fourier Transform" (partic FFT)
		- FFT is expansion based on sines and cosines
		- (compare also expansions based on Bessel Fns, Spherical fns, or other systems of fns as "mathematical modes" for "basis mode" for coordinate transformations)
		- Uses for SVD
			- Solve for x in Ax = b for non-square A
				- E.g. linear regression Xb = y for data X and y
			- SVD for PCA
				- based on correlation in data, distill high-dim data to key features
		- SVD is based on simple and interpretable computation


## Chapter 1 Notes

### Video Lectures 1 & 2

$X = U \Sigma V^T$

- Each of the matrix has separate, intuitive interpretation
- Properties of U, $\Sigma, and V
    - X is n x m (m observations of an nx1 column vector of data, which could be a flattened array)
    - U is n x n (square)
		- same column length as data X, so they can be reshaped into original obs (faces, images, or whatever)
        - columns of U are "left singular vectors," ordered by importance in data
			- kind of "eigenobservations"
        - form a basis for the data
    - $\Sigma$ is "diagonal," and n x m (diagonal in upper m x m block, else 0 below and off diagonal)
        - elements are non-negative and heirachically ordered: $\sigma_1 \ge \sigma_2 \ge ... >= \sigma_m$
		- the central matrix $\Simga$ is the matrix of "singular values", associated with the (importance of the) singular vectors in U and V
    - V is m x m (square)
        - columns of V are "right singular vectors," ordered by importance in data 
        - if the original observations X are sequential in time, the columns of V^T give "eigen time-series" info
    - U and V are unitary (columns are orthonormal, i.e. orthogonal and unit length), transpose is its inverse
        - $U U^T = U^T U = I$
        - $V V^T = V^T V = I$
	- Elements of U and V (and Sigma) are heirarchically organized
	- V represents time evolution or mixture info for left-singular vectors:
		- kth column of V^T is the mixture of the left-singular vectors u_i in U that is needed to reproduced the kth observation of X
- invoke SVD by simple commands in Matlab or Python
	[U, S, V] = svd(X)
- SVD is 
	- guaranteed to exist
	- unique

### Video 3. Singular Value Decomposition - Matrix Approximation
- Note that since original data X (n x m) has m observations, so at most m linearly independent observations, even though U (n x n) has n columns of "left singular vectors", at most the first m are meaningful for representing X.
	- U has more parameters/elements than X does!
- "rank r SVD approximation of X":
	- Compresses n x m data matrix X (for typically large n, smaller m) into 
		- n x r matrix $\hat X$
		- r diagonal elements in $\hat \Sigma$
		- r x r matrix $\hat V^T$
		
- Eckard-Young Theorem
	- provable that k-truncated SVD $\tilde X$ is best rank-k approximation of X
	- "best" means it minimizes Frobenius norm of difference between $X$ and $\hat X$
		- $\tilde X = argmin_{\tilde X} ||X - {\tilde X}||_F$
- **Bottom line for SVD Matrix Approximation**
	- **You can approximate any matrix X by a lower rank matrix $\tilde X$ given by a trunkated SVD**
	- Algebraically:
		- $X_{n x m} = U_{n x n} \Sigma_{n x m} V^T_{m x m}$
			- Also $X_{n x m} = U_{n x m} \Sigma_{m x m} V^T_{m x m}$ (can drop U cols after m, $\Sigma$ rows below m, which are zero) for the economy SVD, while retaining full info of X
		- $\tilde X_{n x k} = \tilde U_{n x k} \tilde \Sigma_{k x k} \tilde V^T_{k x m}$
			- drop U cols after k, $\Sigma$ rows & cols past k, and $V^T$ rows below k, wihch are lower information (lower "energy") singular vectors and values, since SVD matrixes are heirachically ordered.