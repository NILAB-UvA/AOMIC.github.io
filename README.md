# AOMIC: the Amsterdam Open MRI Collection
The Amsterdam Open MRI Collection (AOMIC) is a collection of three datasets with multimodal (3T) MRI data including structural (T1-weighted), diffusion-weighted, and (resting-state and task-based) functional BOLD MRI data, as well as detailed demographics and psychometric variables from a large set of healthy participants (*N* = 928, *N* = 226, and *N* = 216). Notably, task-based fMRI was collected during various robust paradigms (targeting naturalistic vision, emotion perception, working memory, face perception, cognitive conflict and control, and response inhibition) for which extensively annotated event-files are available. For each dataset and data modality, we provide the data in both raw and preprocessed form (both compliant with the Brain Imaging Data Structure), which were subjected to extensive (automated and manual) quality control. 

## The data
All raw/preprocessed data is publicly available from the Openneuro data sharing platform:

* ID1000: [https://openneuro.org/datasets/ds003097](https://openneuro.org/datasets/ds003097)
* PIOP1: [https://openneuro.org/datasets/ds002785](https://openneuro.org/datasets/ds002785)
* PIOP2: [https://openneuro.org/datasets/ds002790](https://openneuro.org/datasets/ds002790)

![overview](https://docs.google.com/drawings/d/e/2PACX-1vTqWmkIqfLq6-K6Ue106kvWhySohACMQ1l8qHZOTWWQaHm30TfILyzD5PzpgzOG5LKkZ-qhf1JX1GOJ/pub?w=5460&h=3401)

Moreover, there are group-level maps (such as task-based whole-brain constrast maps) available on [Neurovault](https://neurovault.org/):
* ID1000: [https://neurovault.org/collections/7105/](https://neurovault.org/collections/7105/)
* PIOP1: [https://neurovault.org/collections/7103/](https://neurovault.org/collections/7103/)
* PIOP2: [https://neurovault.org/collections/7104/](https://neurovault.org/collections/7104/)

## The paper
The contents and curation process of AOMIC is described in detail in [this paper](https://www.nature.com/articles/s41597-021-00870-6), published in Nature Scientific Data. If you re-use the data, please cite our paper accordingly:

Snoek, L., van der Miesen, M. M., Beemsterboer, T., Van Der Leij, A., Eigenhuis, A., & Scholte, H. S. (2021). The Amsterdam Open MRI Collection, a set of multimodal MRI datasets for individual difference analyses. *Scientific data, 8*(1), 1-23.

## How to download the data?
The entire dataset, including all derivatives, is very large (~53GB raw data + ~355GB derivatives), so we recommend against downloading everything at once (unless you actually want to use all data, of course).

Instead, you can use the [awscli](https://aws.amazon.com/cli/) tool to programmatically download the relevant files. 
The `awscli` tool can be installed using `pip` (i.e., `pip install awscli`). Now, if you're only interested in the raw T1-weighted scans, you can download *only* those files using the following command:

```
aws s3 sync --no-sign-request s3://openneuro.org/ds002790 /your/output/dir --exclude "*" --include "sub-*/anat/*T1w.nii.gz"
```

The `--exclude "*"` part makes sure that all files are ignored except those matching the `--include` filter. 
Similarly, if you'd only want to download the Fmriprep-preprocessed resting-state files in "MNI152NLin2009cAsym" space only, you can use the following command:

```
aws s3 sync --no-sign-request s3://openneuro.org/ds002790 /your/output/dir --exclude "*" --include "derivatives/fmriprep/sub-*/func/*task-restingstate*space-MNI*desc-preproc_bold.nii.gz"
```

You can, of course, also download a single file, e.g., the `participants.tsv` file:

```
aws s3 sync --no-sign-request s3://openneuro.org/ds002790 /your/ouput/dir --exclude "*" --include "participants.tsv"
```

Note that the data is organized following the Brain Imaging Data Structure ([BIDS](bids.neuroimaging.io)). All raw data is located in subject-specific folders directly under the root directory. Data from an example subject (sub-0100) from PIOP1 looks, for example, as follows (only data from the `workingmemory` task is shown for brevity):

```
sub-0100
├── anat
│   ├── sub-0100_T1w.json
│   └── sub-0100_T1w.nii.gz
├── dwi
│   ├── sub-0100_dwi.bval
│   ├── sub-0100_dwi.bvec
│   ├── sub-0100_dwi.json
│   └── sub-0100_dwi.nii.gz
└── func
    ├── sub-0100_task-workingmemory_acq-seq_bold.json
    ├── sub-0100_task-workingmemory_acq-seq_bold.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_events.tsv
    ├── sub-0100_task-workingmemory_acq-seq_recording-respcardiac_physio.json
    ├── sub-0100_task-workingmemory_acq-seq_recording-respcardiac_physio.phy
    └── sub-0100_task-workingmemory_acq-seq_recording-respcardiac_physio.tsv.gz
```

Preprocessed data is organized in the `derivatives/fmriprep` directory, which also has subject-specific subdirectories organized as follows (shown for example subject sub-0100):

```
derivatives/fmriprep/sub-0100
├── anat
│   ├── sub-0100_desc-aparcaseg_dseg.nii.gz
│   ├── sub-0100_desc-aseg_dseg.nii.gz
│   ├── sub-0100_desc-brain_mask.json
│   ├── sub-0100_desc-brain_mask.nii.gz
│   ├── sub-0100_desc-preproc_T1w.json
│   ├── sub-0100_desc-preproc_T1w.nii.gz
│   ├── sub-0100_dseg.nii.gz
│   ├── sub-0100_from-MNI152NLin2009cAsym_to-T1w_mode-image_xfm.h5
│   ├── sub-0100_from-orig_to-T1w_mode-image_xfm.txt
│   ├── sub-0100_from-T1w_to-fsnative_mode-image_xfm.txt
│   ├── sub-0100_from-T1w_to-MNI152NLin2009cAsym_mode-image_xfm.h5
│   ├── sub-0100_hemi-L_inflated.surf.gii
│   ├── sub-0100_hemi-L_midthickness.surf.gii
│   ├── sub-0100_hemi-L_pial.surf.gii
│   ├── sub-0100_hemi-L_smoothwm.surf.gii
│   ├── sub-0100_hemi-R_inflated.surf.gii
│   ├── sub-0100_hemi-R_midthickness.surf.gii
│   ├── sub-0100_hemi-R_pial.surf.gii
│   ├── sub-0100_hemi-R_smoothwm.surf.gii
│   ├── sub-0100_label-CSF_probseg.nii.gz
│   ├── sub-0100_label-GM_probseg.nii.gz
│   ├── sub-0100_label-WM_probseg.nii.gz
│   ├── sub-0100_space-MNI152NLin2009cAsym_desc-brain_mask.json
│   ├── sub-0100_space-MNI152NLin2009cAsym_desc-brain_mask.nii.gz
│   ├── sub-0100_space-MNI152NLin2009cAsym_desc-preproc_T1w.json
│   ├── sub-0100_space-MNI152NLin2009cAsym_desc-preproc_T1w.nii.gz
│   ├── sub-0100_space-MNI152NLin2009cAsym_dseg.nii.gz
│   ├── sub-0100_space-MNI152NLin2009cAsym_label-CSF_probseg.nii.gz
│   ├── sub-0100_space-MNI152NLin2009cAsym_label-GM_probseg.nii.gz
│   └── sub-0100_space-MNI152NLin2009cAsym_label-WM_probseg.nii.gz
├── figures
│   ├── sub-0100_desc-reconall_T1w.svg
│   ├── sub-0100_dseg.svg
│   ├── sub-0100_task-workingmemory_acq-seq_desc-bbregister_bold.svg
│   ├── sub-0100_task-workingmemory_acq-seq_desc-carpetplot_bold.svg
│   ├── sub-0100_task-workingmemory_acq-seq_desc-compcorvar_bold.svg
│   ├── sub-0100_task-workingmemory_acq-seq_desc-confoundcorr_bold.svg
│   ├── sub-0100_task-workingmemory_acq-seq_desc-rois_bold.svg
│   └── sub-0100_task-workingmemory_acq-seq_desc-sdc_bold.svg
└── func
    ├── sub-0100_task-workingmemory_acq-seq_desc-confounds_regressors.json
    ├── sub-0100_task-workingmemory_acq-seq_desc-confounds_regressors.tsv
    ├── sub-0100_task-workingmemory_acq-seq_space-fsaverage5_hemi-L.func.gii
    ├── sub-0100_task-workingmemory_acq-seq_space-fsaverage5_hemi-R.func.gii
    ├── sub-0100_task-workingmemory_acq-seq_space-MNI152NLin2009cAsym_boldref.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-MNI152NLin2009cAsym_desc-aparcaseg_dseg.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-MNI152NLin2009cAsym_desc-aseg_dseg.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-MNI152NLin2009cAsym_desc-brain_mask.json
    ├── sub-0100_task-workingmemory_acq-seq_space-MNI152NLin2009cAsym_desc-brain_mask.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-MNI152NLin2009cAsym_desc-preproc_bold.json
    ├── sub-0100_task-workingmemory_acq-seq_space-MNI152NLin2009cAsym_desc-preproc_bold.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-T1w_boldref.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-T1w_desc-aparcaseg_dseg.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-T1w_desc-aseg_dseg.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-T1w_desc-brain_mask.json
    ├── sub-0100_task-workingmemory_acq-seq_space-T1w_desc-brain_mask.nii.gz
    ├── sub-0100_task-workingmemory_acq-seq_space-T1w_desc-preproc_bold.json
    └── sub-0100_task-workingmemory_acq-seq_space-T1w_desc-preproc_bold.nii.gz
```

The data for PIOP2 and ID1000 are organized in the same way as the example PIOP1 subject from above.

## Questions
For questions, please email L (dot) Snoek (at) UvA (dot) nl.
