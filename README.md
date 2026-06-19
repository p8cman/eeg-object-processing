# Project overview
This repository is used for a NTU course module - HP7217: APPLIED FUNCTIONAL NEUROSCIENCE. A large-scale EEG dataset in naturalistic scenes was used to study for object recognition. Data preprocessing was done by the authors of the dataset so only the epoched EEG data was used. OpenNeuro Accession Number: ds005811. It can be found on: https://openneuro.org/datasets/ds005811/versions/1.0.9

That being said, I aim to conduct my own data preprocessing to have a feel of the data cleaning process and update with a Jupyter notebook here. For this dataset, individuals had to watch 2000-4000 images of natural objects and their stimulus response (animate vs inanimate) was collected.
The current Object_preprocessing Jupyter notebook contains data analyses, results and figures.

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

# Data analysis
## One subject
1.  Understand metadata of first subject (e.g., event markers, object classes)
2.  Plot epoched data and their conditions (animate vs inanimate)
3.  Create butterfly plots of all signals and their conditions (animate vs inanimate)

<img width="651" height="311" alt="sub01_all_channels" src="https://github.com/user-attachments/assets/f5dc35ca-e4d8-4cdd-b7d7-fcb47b36741a" />

<img width="651" height="311" alt="sub01_all_channels_animate" src="https://github.com/user-attachments/assets/57af33c4-f00c-4c72-85a9-e6a231f32b1b" />

<img width="651" height="311" alt="sub01_all_channels_inanimate" src="https://github.com/user-attachments/assets/1bed7a33-54ee-4d05-b7c9-243641667cff" />

4.  Plot global field power and their conditions (animate vs inanimate)

<img width="811" height="611" alt="sub01_all_channels_GFP" src="https://github.com/user-attachments/assets/b358031d-be27-4fbb-b980-d524e74645a7" />

5.  Create scalp topomaps and their conditions (animate vs inanimate)

<img width="610" height="167" alt="sub01_all_channels_topomap" src="https://github.com/user-attachments/assets/5a658c70-e375-4d0c-acbd-278370efb674" />

<img width="610" height="171" alt="sub01_all_channels_animate_topomap" src="https://github.com/user-attachments/assets/98a288af-98f3-46ec-8c2d-1192487f55a5" />

<img width="610" height="167" alt="sub01_all_channels_inanimate_topomap" src="https://github.com/user-attachments/assets/f3934ecc-20c4-41d5-a133-5f8ea3027f2b" />

6.  Combine butterfly plots and scalp topomaps and their conditions (animate vs inanimate)

<img width="809" height="431" alt="sub01_all_channels_joint" src="https://github.com/user-attachments/assets/089e7968-c55e-4544-bdd1-c38bdddc681f" />

<img width="809" height="431" alt="sub01_all_channels_animate_joint" src="https://github.com/user-attachments/assets/cbb5e264-e83f-47eb-afc5-506f7090a9ba" />

<img width="809" height="431" alt="sub01_all_channels_inanimate_joint" src="https://github.com/user-attachments/assets/55a1d27b-1ef8-49aa-872b-60fa1abad175" />

7.  Compare difference between conditions (animate vs inanimate)

<img width="809" height="431" alt="sub01_animate_inanimate_difference" src="https://github.com/user-attachments/assets/aaea6fa9-44cf-4c56-b45a-c864fa93fbaa" />

8.  Average across channels with ROIs
9.  Extract mean amplitudes of ROI for first subject = 8.0341 µV
10.  Create butterfly plots of ROI signals and their conditions (animate vs inanimate)

<img width="651" height="311" alt="sub01_ROI_channels" src="https://github.com/user-attachments/assets/6d528ff4-ca98-4e2d-b645-b18887a34763" />

<img width="651" height="311" alt="sub01_ROI_channels_animate" src="https://github.com/user-attachments/assets/cc3487c9-fc66-4585-8ce1-6e2401f22934" />

<img width="651" height="311" alt="sub01_ROI_channels_inanimate" src="https://github.com/user-attachments/assets/a8927365-dd81-44d2-babc-0b83faf49b07" />

11.  Plot global field power of ROI and their conditions (animate vs inanimate)

<img width="811" height="611" alt="sub01_ROI_channels_GFP" src="https://github.com/user-attachments/assets/2070823f-de9e-435f-9daf-c8b3044b9d58" />

12.  Combine butterfly plots and scalp topomaps of ROI and their conditions (animate vs inanimate)

<img width="809" height="431" alt="sub01_ROI_channels_joint" src="https://github.com/user-attachments/assets/472931af-442d-4b6e-8d6d-18acf1d2f83d" />

<img width="809" height="431" alt="sub01_ROI_channels_animate_joint" src="https://github.com/user-attachments/assets/43b2e60a-4417-4cde-a4d6-306c2eb71231" />

<img width="809" height="431" alt="sub01_ROI_channels_inanimate_joint" src="https://github.com/user-attachments/assets/16f4b508-2091-4f1a-b0d3-ee1b1fad0f1a" />

13.  Conduct independent t-test between conditions (animate vs inanimate), t = -0.368, p = 0.7125

## All subjects
14.  Compute grand average across all 19 subjects
15.  Create butterfly plots of ROI signals and their conditions (animate vs inanimate) for all subjects

<img width="651" height="311" alt="all_subs_ROI_channels" src="https://github.com/user-attachments/assets/b65f5d08-c8cc-4200-b8b1-a6857996c302" />

<img width="651" height="311" alt="all_subs_ROI_channels_animate" src="https://github.com/user-attachments/assets/25172446-42cd-46eb-9448-33d429ba7db7" />

<img width="651" height="311" alt="all_subs_ROI_channels_inanimate" src="https://github.com/user-attachments/assets/c70f6b03-281c-49a0-8994-e55c6a29497a" />

16.  Combine butterfly plots and scalp topomaps of ROI and their conditions (animate vs inanimate) for all subjects

<img width="809" height="431" alt="all_subs_ROI_channels_joint" src="https://github.com/user-attachments/assets/73a0561d-ff8d-47c0-a1d2-27a1fafefaea" />

<img width="809" height="431" alt="all_subs_ROI_channels_animate_joint" src="https://github.com/user-attachments/assets/6bb86b6a-875d-48e2-ba64-1c3531214e4b" />

<img width="809" height="431" alt="all_subs_ROI_channels_inanimate_joint" src="https://github.com/user-attachments/assets/4a408c07-2923-4ee8-ba7a-1b5d0f59787f" />

17.  Conduct paired t-test between conditions (animate vs inanimate) for all subjects, t = -2.620, p = 0.0174
18.  Extract mean amplitudes for all subjects

<img width="545" height="372" alt="all_subs_animate_inanimate_difference" src="https://github.com/user-attachments/assets/4bdbccfc-033b-42ab-96e6-f3e3d507c664" />

# References
Eimer, M. (2012). The Face-Sensitive N170 Component of the Event-Related Brain Potential. In A. J. Calder, G. Rhodes, M. H. Johnson, & J. V. Haxby (Eds.), Oxford Handbook of Face Perception. Oxford University Press. https://doi.org/10.1093/oxfordhb/9780199559053.013.0017

Gao, C., Conte, S., Richards, J. E., Xie, W., & Hanayik, T. (2019). The neural sources of N170: Understanding timing of activation in face-selective areas. Psychophysiology, 56(6), e13336. https://doi.org/10.1111/psyp.13336

Larson, E., Gramfort, A., Engemann, D. A., Leppakangas, J., Brodbeck, C., Jas, M., Brooks, T. L., Sassenhagen, J., McCloy, D., Luessi, M., King, J.-R., Höchenberger, R., Brunner, C., Goj, R., Favelier, G., van Vliet, M., Wronkiewicz, M., Appelhoff, S., Rockhill, A., … user27182. (2026). MNE-Python (v1.12.1). Zenodo. https://doi.org/10.5281/zenodo.19666955

Luck, S. J. (2014). An introduction to the event-related potential technique, second edition. MIT Press.

Rossion, B., & Jacques, C. (2011). The N170: Understanding the Time Course of Face Perception in the Human Brain. In E. S. Kappenman & S. J. Luck (Eds.), The Oxford Handbook of Event-Related Potential Components. Oxford University Press. https://doi.org/10.1093/oxfordhb/9780195374148.013.0064

Wang, Y., Huang, H., Yang, H., Xu, J., Mo, S., Lai, H., Wu, T., & Zhang, J. (2019). Influence of EEG References on N170 Component in Human Facial Recognition. Frontiers in Neuroscience, 13, 705. https://doi.org/10.3389/fnins.2019.00705

Zhang, G., Zhou, M., Zhen, S. et al. A large-scale MEG and EEG dataset for object recognition in naturalistic scenes. Sci Data 12, 857 (2025). https://doi.org/10.1038/s41597-025-05174-7
