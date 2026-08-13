# Support vector machines

Detecting the P300 response in EEG, a genuinely hard classification problem where the signal
is buried in noise and the classes are far from balanced.

## Data

The BI2013a dataset from MOABB under the P300 paradigm, 80 820 epochs of 16 channels by 103
samples. An epoch is labelled Target when it followed the stimulus the subject was counting
and NonTarget otherwise, and targets are the rare class by design of the experiment.

## Method

Epochs are decimated into a 96-dimensional feature vector per trial and standardised. Three
support vector machines are trained, a linear one on the full set and an RBF and a
polynomial one on a subsample, since the kernel methods do not scale to the full set here.
The split is made with `GroupShuffleSplit` over subjects, so that no subject appears in both
train and test and the score measures generalisation to a new person rather than to a new
epoch from a known one.

## Results

| Model | Accuracy | Precision | Recall | F1 | ROC AUC |
|-------|---------:|----------:|-------:|---:|--------:|
| Polynomial, subsample | 0.691 | 0.264 | 0.480 | 0.341 | 0.637 |
| RBF, subsample | 0.697 | 0.266 | 0.469 | 0.340 | 0.649 |
| Linear, full | 0.616 | 0.235 | 0.576 | 0.333 | 0.631 |

The numbers are modest and that is the honest result for cross-subject P300 with plain
SVMs. Accuracy is the misleading column, since predicting NonTarget always would score
higher than any of these; the ROC AUC around 0.64 is what says the models have found real
signal. The linear model on the full data trades precision for recall, catching more targets
at the cost of more false alarms, which is the trade-off a downstream speller would have to
be tuned against.
