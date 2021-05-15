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

## Questions
For questions, please email L (dot) Snoek (at) UvA (dot) nl.
