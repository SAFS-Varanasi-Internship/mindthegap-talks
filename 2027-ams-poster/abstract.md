<!-- Event: AMS 107th Annual Meeting, Denver, CO. Poster, Wednesday, January 13, 2027.
     Program page: https://ams.confex.com/ams/107ANNUAL/meetingapp.cgi/Paper/497283
     The same abstract is used for the eScience talk (../2027-escience/abstract.md). -->

# Scalable Deep Learning for Satellite Ocean-Color Gap Filling: From Cloud-Hosted Training Data to Model Deployment to Gap-Filled Outputs

Elizabeth Eli Holmes<sup>1,2</sup>, Troy Russo<sup>3</sup>, Kaira Nair<sup>4</sup>

<sup>1</sup> NOAA, Seattle, WA, USA  
<sup>2</sup> School of Fisheries and Aquatic Sciences, University of Washington, Seattle, WA, USA  
<sup>3</sup> Departments of Statistics and Mathematics, University of Washington, Seattle, WA, USA  
<sup>4</sup> Applied and Computational Mathematical Sciences, University of Washington, Seattle, WA, USA

## Abstract

The increasing availability of satellite data products in cloud-accessible formats creates new opportunities for applying deep learning directly to large environmental datasets. However, practical use of these methods remains limited by the difficulty of training models on datasets larger than local memory, efficiently accessing remotely hosted data, preserving preprocessing information, and applying trained models back to selected portions or the full observational record. We are developing an open-source workflow that addresses these challenges for gap-filling cloud-obstructed ocean-color observations and derived products such as chlorophyll-a estimates.

The workflow uses an autoencoder-based approach in which synthetic clouds are applied to observed data to create training examples from the same dataset that will ultimately be gap filled. Because the original values beneath the synthetic masks remain known, the model can learn to reconstruct cloud-obstructed pixels without requiring a separate gap-free training dataset. The workflow operates directly on cloud-hosted Zarr and Icechunk datasets, including virtual datasets constructed with tools such as VirtualiZarr. Training samples are generated lazily using xarray, Dask, and Xbatcher, enabling patch-based model training without first downloading or materializing the full dataset.

We use a convolutional U-Net because reconstruction of missing ocean-color observations depends not only on conditions at individual pixels, but also on spatial context and coherent structures in the surrounding field. The model can therefore learn regional characteristics, including seasonal variability, coastline information, and recurring small- to medium-scale spatial patterns, rather than relying on a model tuned to global conditions. Initial applications show that the model can reproduce small- to medium-scale spatial features and seasonal patterns, while also highlighting the challenge of recovering broader spatial structure. Following training, the model is saved as a reusable bundle containing the network, weights, and metadata required to reproduce model inputs and preprocessing. The model can then be applied to individual dates, user-defined subsets, or an entire satellite record.

This presentation will describe: (1) training deep-learning models directly from cloud-hosted, larger-than-memory satellite datasets; (2) the use of synthetic masking for regional gap-filling model development; (3) packaging and deployment of trained models for selected dates or complete records; and (4) evaluation of multiscale approaches for improving the spatial fidelity of reconstructed ocean-color fields.
