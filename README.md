## AOMIC: the Amsterdam Open MRI Collection

AOMIC is a set of publicly available MRI datasets acquired at the Spinoza Centre (location REC), University of Amsterdam, the Netherlands. At the moment, we're finalizing the data curation process and we aim to release the data on [openneuro.org](openneuro.org) before the end of the year. For now, you can learn more about the collection in our [CCN](ccneuro.org) submission ([download](AOMIC_CCN2019.pdf)).

### How to download the data?
The entire dataset, including all derivatives, is very large (~53GB raw data + ~355GB derivatives), so we recommend against downloading everything at once (unless you actually want to use all data, of course).
Instead, you can use the [awscli](https://aws.amazon.com/cli/) tool to programmatically download the relevant files. 
The `awscli` tool can be installed using `pip` (i.e., `pip install awscli`). Now, if you're only interested in the raw T1-weighted scans, you can download *only* those files using the following command:

```
aws s3 sync --no-sign-request s3://openneuro.org/ds002790 /your/ouput/dir --exclude "*" --include "sub-*/anat/*T1w.nii.gz"
```

The `--exclude "*"` part makes sure that all files are ignored except those matching the `--include` filter. 
Similarly, if you'd only want to download the Fmriprep-preprocessed resting-state files in "MNI152NLin2009cAsym" space only, you can use the following command:

```
aws s3 sync --no-sign-request s3://openneuro.org/ds002790 /your/ouput/dir --exclude "*" --include "derivatives/fmriprep/sub-*/func/*task-restingstate*space-MNI*desc-preproc_bold.nii.gz"
```

You can, of course, also download a single file, e.g., the `participants.tsv` file:

```
aws s3 sync --no-sign-request s3://openneuro.org/ds002790 /your/ouput/dir --exclude "*" --include "participants.tsv"
```

### Questions
For questions, please email L (dot) Snoek (at) UvA (dot) nl.
