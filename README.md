# Project overview
This project is based on this paper:
Zhang, G., Zhou, M., Zhen, S. et al. A large-scale MEG and EEG dataset for object recognition in naturalistic scenes. Sci Data 12, 857 (2025). https://doi.org/10.1038/s41597-025-05174-7

Only the epoched EEG data will be used. OpenNeuro Accession Number: ds005811.
It can be found on: https://openneuro.org/datasets/ds005811/versions/1.0.9

Individuals watch 4000 images of natural objects and their stimulus response (animate vs inanimate) is collected.
Jupyter notebook contains analysis and figures.

# Research question
Do individuals exhibit different neural activation patterns (N170 component) to different classes of objects?

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
4. Noise reduction. The Zapline algorithm was used to reduce power line noise (50 Hz) in EEG. Average of all EEG channels was used to re-reference the EEG data.
5. ICA artifact rejection. Each run of EEG data was first filtered within the 1–100 Hz range to reduce the impact of low-frequency drifts and high-frequency noise on the ICA decomposition. The data was then decomposed into different independent components using ICA algorithm, and the artifacts components were identified by combining the automatic artifact selection algorithms (MNE-ICALabel for EEG) and manual inspection. Finally, these artifact components were removed on the 0.1–100 Hz time series through regression.
6. Epoching. We divided the time window of each trial from −100ms to 800 ms relative to stimulus onset to fully capture the neural response induced by the stimulus. Baseline correction was performed using the time window from 100 ms before onset of the images. Then, all trials for each participant were concatenated to create the participant’s epoch data.

# Current workflow
1.  Plot evoked objects and topomaps
2.  Plot global field power
3.  Average across channels with ROIs
4.  Compare between animate and inanimate conditions
5.  Compute grand average across subjects
6.  Extract mean amplitudes

# References
Eimer, M. (2012). The Face-Sensitive N170 Component of the Event-Related Brain Potential. In A. J. Calder, G. Rhodes, M. H. Johnson, & J. V. Haxby (Eds.), Oxford Handbook of Face Perception. Oxford University Press. https://doi.org/10.1093/oxfordhb/9780199559053.013.0017

Gao, C., Conte, S., Richards, J. E., Xie, W., & Hanayik, T. (2019). The neural sources of N170: Understanding timing of activation in face-selective areas. Psychophysiology, 56(6), e13336. https://doi.org/10.1111/psyp.13336

Larson, E., Gramfort, A., Engemann, D. A., Leppakangas, J., Brodbeck, C., Jas, M., Brooks, T. L., Sassenhagen, J., McCloy, D., Luessi, M., King, J.-R., Höchenberger, R., Brunner, C., Goj, R., Favelier, G., van Vliet, M., Wronkiewicz, M., Appelhoff, S., Rockhill, A., … user27182. (2026). MNE-Python (v1.12.1). Zenodo. https://doi.org/10.5281/zenodo.19666955

Rossion, B., & Jacques, C. (2011). The N170: Understanding the Time Course of Face Perception in the Human Brain. In E. S. Kappenman & S. J. Luck (Eds.), The Oxford Handbook of Event-Related Potential Components. Oxford University Press. https://doi.org/10.1093/oxfordhb/9780195374148.013.0064

Wang, Y., Huang, H., Yang, H., Xu, J., Mo, S., Lai, H., Wu, T., & Zhang, J. (2019). Influence of EEG References on N170 Component in Human Facial Recognition. Frontiers in Neuroscience, 13, 705. https://doi.org/10.3389/fnins.2019.00705

Zhang, G., Zhou, M., Zhen, S. et al. A large-scale MEG and EEG dataset for object recognition in naturalistic scenes. Sci Data 12, 857 (2025). https://doi.org/10.1038/s41597-025-05174-7
