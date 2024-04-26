# radon_transformation_for_DM
This code analyzes 3D velocity data by creating histograms and applying the Radon transform for feature extraction. It also converts data into astronomical coordinates and generates a Mollweide sky map.
## Setup and Data Loading
First, we import the necessary libraries and mount Google Drive to access the data files stored there. This setup is crucial for loading the velocity data, which we will analyze.

`import numpy as np
from scipy.integrate import tplquad, dblquad
from google.colab import drive
import math

### Mount Google Drive to access the data file
drive.mount('/content/drive')

### Load velocity data from a numpy file stored on Google Drive
vel = np.load('/content/drive/MyDrive/Colab Notebooks/dmvposnp.npy')`

## Constants and Initial Data Preparation
Define constants used throughout the notebook and prepare data for further processing. `AtomicMassS` is the atomic mass in atomic mass units (amu) and `bin_number` defines how finely we bin our data in histograms.
`AtomicMassS = 32.066  # Atomic mass of sulfur
bin_number = 10  # Number of bins for the histogram

# Calculate ranges for each component and create bins
ranges = [(vel[:, i].min(), vel[:, i].max()) for i in range(3)]
bins = [np.linspace(ranges[i][0], ranges[i][1], bin_number) for i in range(3)]
hist, edges = np.histogramdd(vel[:, :3], bins=bins, density=True)

# Calculate bin widths based on the ranges
dx = (ranges[0][1] - ranges[0][0]) / bin_number
dy = (ranges[1][1] - ranges[1][0]) / bin_number
dz = (ranges[2][1] - ranges[2][0]) / bin_number`
