# Project overview
This project is based on this paper:
Zhang, G., Zhou, M., Zhen, S. et al. A large-scale MEG and EEG dataset for object recognition in naturalistic scenes. Sci Data 12, 857 (2025). https://doi.org/10.1038/s41597-025-05174-7

Only the epoched EEG data will be used. It can be found on OpenNeuro. OpenNeuro Accession Number: ds005811.
Individuals watch 4000 images of natural objects and their stimulus response (animate vs inanimate) is collected.
Jupyter notebook contains analysis and figures.

# Research question
Do individuals exhibit different neural activation patterns to different classes of objects?

# Methods
| |Natural Object Dataset|
|---|---|
|Stimulus type|60 images x 1000 object categories = 60,000 images|
|Stimulus paradigm|Each trial lasted 1500 ms, with stimulus presented for 800 ms, followed by variable fixation period of 700 ± 200 ms|
|Participants|19 (8 females, mean age ± SD, 21.26 ± 2.00 years)|
| |9 completed 4 EEG sessions, each consisting of eight runs and 4000 unique images|
| |10 completed 2 EEG sessions, each consisting of eight runs and 2000 unique images|
|Data type|EEG data|
|Hardware|64-channel Neuroscan system|
|Sampling rate|500 Hz|
|Image size|600 x 600 pixels|

# Data preprocessing (conducted by authors)
1.  BIDS conversion. The raw EEG data were first converted to Brain-Imaging-Data-Structure (BIDS) format. During this process, we manually checked the data integrity and wrote participant information, experiment time, and other details into the BIDS structure.
2.  Downsample. EEG data were downsampled to 250 Hz to reduce the computational burden of downstream analysis.
3. Bad sensor fixing. We used established automatic bad channel detection algorithms to detect bad channels in each run of EEG. 1.34 bad channels (SD = 2.32) on average were detected per EEG data run. The bad channels were then corrected using interpolation algorithms (spherical splines interpolation for EEG).
4. Noise reduction. The Zapline algorithm was used to reduce power line noise (50 Hz) in EEG. Average of all EEG channels was used to re-referencing the EEG data.
5. ICA artifact rejection. Each run of EEG data was first filtered within the 1–100 Hz range to reduce the impact of low-frequency drifts and high-frequency noise on the ICA decomposition. The data was then decomposed into different independent components using ICA algorithm, and the artifacts components were identified by combining the automatic artifact selection algorithms (MNE-ICALabel for EEG) and manual inspection. Finally, these artifact components were removed on the 0.1–100 Hz time series through regression.
6. Epoching. We divided the time window of each trial from −100ms to 800 ms relative to stimulus onset to fully capture the neural response induced by the stimulus. Baseline correction was performed using the time window from 100 ms before onset of the images. Then, all trials for each participant were concatenated to create the participant’s epoch data.

# Current workflow
1.  Plot evoked objects and topomaps
2.  Plot global field power
3.  Average natural object classes across channels with ROIs
4.  Compare between classes
5.  Compute grand average across subjects
6.  Extract latency and amplitude
7.  Calculate PSD
8.  Time-frequency analysis

# References
Zhang, G., Zhou, M., Zhen, S. et al. A large-scale MEG and EEG dataset for object recognition in naturalistic scenes. Sci Data 12, 857 (2025). https://doi.org/10.1038/s41597-025-05174-7
