# spin
Simulations of spin systems with QuTiP, mainly for my research.

# Requirements

* `numpy` obviously, it's scientific computing in python after all! ([conda-forge](https://anaconda.org/conda-forge/numpy))
* `qutip` the main package for these simulations ([conda-forge](https://anaconda.org/conda-forge/qutip))
* `matplotlib` for plotting results ([conda-forge](https://anaconda.org/conda-forge/matplotlib)). Versions below 3.3.0 are preffered for proper aspect ratios on the Bloch sphere plots (it was written with 3.0.3 which worked well, see installation section below).
* `mayavi` for plotting 3D Bloch sphere animations ([conda-forge](https://anaconda.org/conda-forge/mayavi))
* `ffmpeg` for animations ([conda-forge](https://anaconda.org/conda-forge/ffmpeg))

# Recommended Installation

Installing the packages above should run fine but there is an issue with versions of `matplotlib` over 3.3, where Bloch-sphere plots have the wrong aspect ratio due to changes in `Axes3d`; it makes your sphere look like a football, and it's not super trivial to fix (if you find a good hack let me know!). It works just fine to downgrade to `matplotlib` version 3.0.3, though you'll have to run a previous version of `python` as well (I'm running 3.7.9). 

If you use the Anaconda distribution, follow the steps below to set up a new environment (called spin) for this repository which should work to get all the right versions.

1. To start, create a new environment `spin` with the right version of `matplotlib`. This will also install `python` and `numpy` as dependencies. `% conda create -n spin matplotlib=3.0.3`
2. Activate the new environment with `% conda activate spin`
3. We're going to have to *pin* the `matplotlib` version to 3.0.3. We'll create a file called *pinned* in our new environment's *conda-meta* directory, and add a line saying that for this environment the version of `matplotlib` is not to be changed. This should handle it such that even if we update or install new packages, `conda` will make sure it doesn't change `matplotlib`. We can create the file and add the line via (your path may vary): `% echo "matplotlib==3.0.3" >> ~/anaconda3/envs/spin/conda-meta/pinned`
4. Next we'll install the other packages we need. Even though we already have `numpy` we'll add it here just to be sure. `% conda install -c conda-forge numpy qutip jupyter mayavi`
5. Next lets list our packages in this environment and check that the `matplotlib` version is 3.0.3, `% conda list`

And with that, the Bloch sphere animations using `matplotlib` will look good. Note that this only affects the plots made with the `qutip.Bloch()` class, and not `qutip.Bloch3d()` class which does not use `matplotlib`.
