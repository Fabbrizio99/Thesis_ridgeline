---
Title: "Tracking Forest Recovery After Vaia: A Fuzzy Logic Approach with Ridgeline plots"
Author: "Mattia Fabris"
Date: "2026-01-05"
Output: html_document
---

## Introduction
The classic analysis of land cover is based on Boolean logic, in which a pixel categorically belongs to a class (e.g., 1 for “Forest”, 0 for “Non-Forest”). 
However, natural ecosystems, especially after severe disturbances such as Storm Vaia in 2018 (HERE I MAY ADD), present ecological gradients and blurred transitions.

Using fuzzy logic in this model, each pixel is not a discrete class, but an ‘empirical model of reality’ with a degree of membership (𝜇) continuous between 0 and 1.

- Value 1.0: Represents the "Ideal Forest" (full photosynthetic biomass); 
- Value 0.0: Represents the total absence of forest characteristics (bare soil, rock, or urban surfaces);  
- Intermediate Values (0.2 - 0.7): Describe the typical heterogeneity of post-disturbance environments, characterised by fallen tree trunks, pioneer herbaceous vegetation and shrubs.

The main objective of this analysis is to monitor the trajectory of forest recovery over time. 
In this context, the identification of specific types of non-forest land cover, such as the distinction between bare soil or fallen dry logs, is secondary to the main objective. 
Instead, the focus is entirely on quantifying how close each pixel is to returning to a functional forest state. 
By using a continuous scale from 0 (non-forest) to 1 (full forest), we ensure that the resulting temporal visualisations, such as Ridgeline Plots, remain immediately intuitive: a shift to the right of the curve clearly signals forest regrowth. 
Conversely, attempting to plot three or four distinct classes simultaneously would complicate interpretation.

## Ridgeline Plots

Ridgeline graphs are partially overlapping line graphs that create the impression of a mountain range. They can be very useful for visualising changes in distributions over time or space.

For this reason, I decided to use this representation for the study of images. Specifically, the study uses satellite images obtained from Copernicus to analyse vegetation continuity.

The analysis was performed using the NDVI index, which indicates the health of vegetation. The images were taken over several years in the same area, which was hit by a storm in 2018 that knocked down many trees. In the specific case below, I will discuss the Val di Fiemme.

```{r, eval=F}
install.packages("ggridges")
install.packages("ggplot2")
install.packages("gtable", type = "source")
library(ggridges)
library(ggplot2)
library(gtable)
```
<img src="2017 Val di Fiemme.jpg" width="100%" />
<img src="2019 Val di Fiemme.jpg" width="100%" />
The geom geom_density_ridges calculates density estimates from the provided data and then plots those, using the ridgeline visualization. The height aesthetic does not need to be specified in this case.

```{r, eval=F}
ridge1b <- ggplot(df_all_zona1b, aes(x = value, y = year, fill = year)) +
  geom_density_ridges(alpha = 0.7, scale = 1) +
  theme_minimal()
```

<img src="Rplotndwi.png" width="100%" />
