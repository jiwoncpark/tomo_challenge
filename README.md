# The Idealised Tomography Challenge

In this challenge you are asked to group galaxies into tomographic bins using only the quantities we generate using the metacalibration method.  These quantities are the only ones for which we can compute a shear bias correction associcated with the division.

We provide training and validation sets of data, and once everyone has added methods, we

This test is highly idealised: we have a huge complete training sample, simple noise models, no outliers, and no variation in depth or any other observing conditions.

Galaxy magnitudes are generated by adding noise to the CosmoDC2 data and applying a preliminary selection cut (SNR>10, metacal flag=0, metacal size > PSF size / 2).

All entrants will be on the author list for the upcoming TXPipe-CosmoDC2 paper, which these results will go into.  The winner will additionally receive glory.


## Getting training data

Run `python -m tomo_challenge.data` in this directory to download the full set of challenge data, about 4.5GB.  You can also get the individual files from here if you prefer:  https://portal.nersc.gov/project/lsst/txpipe/tomo_challenge_data/

## Installing dependencies

From the root folder:
```
$ pip install -r requirements.txt
```


## Metric

The current metric is the S/N on the spectra generated with the method:
```
score^2 = sqrt(mu^T . C^{-1} . mu) - baseline
```
where mu is the theory spectrum and C the Gaussian covariance.

We plan to add second metric based on Fisher matrices shortly.


## Entering the contest.

You can enter the contest by pull request.  Add a python file with your method in it.


## Example Method

In `tomo_challenge/random_forest_example.py` you can find an example of using a scikit-learn classified with a simple galaxy split to assign objects.  Run it by doing, e.g.:

```
python -m tomo_challenge.random_forest_example riz 5
```

This will compute the metric and make a plot for the random forest method using between 1 and 5 bins.

You are welcome to adapt any part of that code in your methods.


The example random forest implementation gets the following scores using the spectrum S/N metric.  For griz:

```
# nbin  score
1  0.0
2  28.2
3  35.4
4  37.9
5  39.7
6  40.3
7  40.5
8  41.1
9  41.5
10  41.8
```

and for riz:

```
# nbin  score
1  0.1
2  21.6
3  26.4
4  28.5
5  29.7
6  30.1
7  30.1
8  29.4
9  29.1
10  30.1
```
