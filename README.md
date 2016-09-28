# cartogram
[![Build Status](https://travis-ci.org/sjewo/cartogram.svg?branch=master)](https://travis-ci.org/sjewo/cartogram)
[![CRAN Downloads](http://cranlogs.r-pkg.org/badges/cartogram)](https://cran.r-project.org/package=cartogram)

## Create Cartograms with R

Construct a continuous area cartogram by a rubber sheet distortion algorithm (Dougenik et al. 1985) or non-contiguous Area Cartograms (Olson 1976) in R.

## Changes
* [0.0.2] Non-contiguous Area Cartogram
* [0.0.2] Prepare data with missing or extreme values before cartogram calculation for faster convergence
* [0.0.1] Intial Release

## Example Continuous Area Cartogram 
```
library(cartogram)
library(tmap)
library(maptools)

data(wrld_simpl)

afr <- wrld_simpl[wrld_simpl$REGION==2,]
afr <- spTransform(afr, CRS("+init=epsg:3395"))

# construct cartogram
afrc <- cartogram(afr, "POP2005", itermax=5)

# plot it
tm_shape(afrc) + tm_fill("POP2005", style="jenks") + 
  tm_borders() + tm_layout(frame=F)
```

![Cartogram](http://www.methoden.ruhr-uni-bochum.de/files/cartogram.jpg)

## Example Non-contiguous Area Cartogram
Many thanks to @rCarto and @neocarto for contributing the code!

```
library(cartogram)
library(tmap)
library(maptools)

data(wrld_simpl)

afr <- wrld_simpl[wrld_simpl$REGION==2,]
afr <- spTransform(afr, CRS("+init=epsg:3395"))

# construct cartogram
afrnc <- nc_cartogram(afr, "POP2005")

# plot it
tm_shape(afr) + tm_borders() + 
  tm_shape(afrnc) + tm_fill("POP2005", style="jenks") + 
  tm_borders() + tm_layout(frame=F)
```
![Cartogram Olson](http://www.methoden.ruhr-uni-bochum.de/files/cartogram_nc.png)


## References
* Dougenik, Chrisman, Niemeyer (1985): An Algorithm To Construct Continuous Area Cartograms. In: Professional Geographer, 37(1), 75-81.
* Olson, J. M. (1976), Noncontiguous Area Cartograms. The Professional Geographer, 28: 371–380. doi:10.1111/j.0033-0124.1976.00371.x


