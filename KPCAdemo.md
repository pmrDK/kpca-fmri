# 1 - Introduction #
This page provides Matlab code as supplementary material for the article entitled
> Nonlinear analysis of neuroimages with kernel principal component analysis and pre-image estimation `[Rasmussen2012]`.

# 2 - Overview #

On this page we provide the following

  * A version of the Object recognition data set of Haxby et.al. `[Haxby2001]` that has been preprocessed within a simple preprocessing pipeline.
  * A Matlab demo of kernel principal component analysis (KPCA) and pre-image estimation `[Mika1999]`. The impact of denoising is evaluated within the NPAIRS resampling framework `[Strother2002]`.
  * Matlab functions that reproduce the results of the Object recognition data set presented in the above-referenced article `[Rasmussen2012]`.

# 3 - Downloads #

Click [here](http://code.google.com/p/kpca-fmri/downloads/detail?name=haxby_preimage.zip) to download Matlab scripts that were use for preprocessing of the object recognition data set, the preprocessed object recognition data set, and Matlab code with the demonstration.

To run the scripts please ensure that the subdirectories **`matlabfunctions`** and **`haxby_preprocessed`** are in the same directory. I.e. use this organization

**`BASEDIR/matlabcode/`**

**`BASEDIR/haxby_preprocessed/`**

where the directory **`BASEDIR`** contains the scripts **`denoisingdemo.m`** , **`manifoldnavigation.m`** and **`haxbyanalysis.m`**, and the **`haxby_preprocessed`** directory contains the **`haxby0?.mat`** files

## Preprocessing details ##

The dataset was downloaded from http://data.pymvpa.org/datasets/haxby2001/ and preprocessed as follows: i) A whole brain mask was created using the bet tool in FSL. ii) Motion correction using mcflirt in FSL. iii) Voxels corresponding to the mask4\_vt.nii mask were retained. iv) linear de-trending in Matlab. v) Standardization of the voxel’s time series with estimates of mean and standard deviation based on the “rest” blocks.

If you prefer to generate the data files from the original data, please download the data set from http://data.pymvpa.org/datasets/haxby2001/, and use the script **`haxby_preprocess.m`** to preprocess the data set. Note that the FSL and SPM software packages are required.

Note: The original authors of `[Haxby2001]` hold the copyright of this dataset and made it available under the terms of the Creative Commons Attribution-Share Alike 3.0 license: http://creativecommons.org/licenses/by-sa/3.0/

# 4 - Demo of KPCA and pre-image estimation #

Here we provide a demonstration of KPCA and pre-image estimation. The impact of image denoising is evaluated within the NPAIRS resampling framework using the Fisher’s discriminant analysis (FDA) as a multivariate model linking the brain scans to the experimental labels/cognitive states. Specifically the following analysis is performed for each subject: i) A denoised version of the data set is created by means of KPCA and pre-image estimation. ii) To evaluate the the impact of image denosing we perform split-half resampling. In each resampling run the data set was split into two partitions with three runs in each split. We train a FDA model on the first split, and use the trained model to infer the labels of scans in the second split and vice versa, yielding two estimates of the prediction accuracy. In order to evaluate model visualization reproducibility we calculate the Pearson’s correlation coefficients between the first canonical variate of the two models, and also the Pearson’s correlation coefficients between sensitivity maps derived from the two models. iii) The procedure in ii) is repeated 10 times where runs, in each resampling iteration, are randomly assigned to the two partitions.

Download the Object recognition data set and the Matlab code. Edit the script **`denoisingdemo.m`** where the path to the to **`BASEDIR`** defined as in section 3 above should be entered as

```
% Declare path
D.ds = 'BASEDIR';
```

Run the script to produce the analysis result, showing model performance in terms of prediction accuracy and visualization reproducibility as measured within the NPAIRS resampling framework.

Note that we for illustration in this demo use fixed settings for the denoising parameters (KPCA subspace dimensionality and the width of the Gaussian kernel). In section 4 we perform a computationally more expensive analysis with nested split-half resampling in order to obtain unbiased estimates of model performance.

# 4 - Reproduce the results of the Object recognition data set presented in `[Rasmussen2012]` #
## Manifold navigation ##

Use the script **`manifoldnavigation.m`** to produce the results of the manifold navigation. This is quite fast to run. Locate the following line to set the path to the files:
```
D.ds = 'BASEDIR';
```
Run the script.
## Image denoising ##

Use the script **`haxbyanalysis.m`** to produce the results of the denoising analysis. Note that is quite expensive (computationally) to run due to the nested resampling procedure. This is due to the fact that we explore 350 pre-processing parameter combinations in six subjects, and perform 10 resampling iteration – each with 10 nested NPAIRS iterations. The code can easily be split into several analysis if a cluster system is available. Locate the following line to set the path to the files:
```
D.ds = 'BASEDIR';
```
Run the script.
# 5 - References #

`[Haxby2001]` Haxby, J. V., Gobbini, I. M., Furey, M. L., Ishai, A., Schouten, J. L., Pietrini, P., 2001. Distributed and overlapping representations of faces and objects in ventral temporal cortex. Science 293 (5539), 2425–2430.

`[Mika1999]` Mika, S., Scholkopf, B., Smola, A., Muller, K. R., Scholz, M., Ratsch, G., 1999. Kernel PCA and de-noising in feature spaces. In: Advances in Neural Information Processing Systems 11. MIT Press, pp. 536–542.

`[Rasmussen2012]` Rasmussen, P.M., Abrahamsen, T.J., Madsen, K.H., Hansen, L.K., 2012. Nonlinear analysis of neuroimages with kernel principal component analysis and pre-image estimation. Neuroimage, DOI: http://dx.doi.org/10.1016/j.neuroimage.2012.01.096 .

`[Strother2002]` Strother, S. C., Anderson, J., Hansen, L. K., Kjems, U., Kustra, R., Sidtis, J., Frutiger, S., Muley, S., Laconte, S., Rottenberg, D., April 2002. The quantitative evaluation of functional neuroimaging experiments: The NPAIRS data analysis framework. NeuroImage 15 (4), 747–771.