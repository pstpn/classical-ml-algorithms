# Exploratory analysis

Feature selection done from information theory rather than from a library call, on
measurements from oil wells: pressures, depths, choke diameters and the rest.

The notebook implements entropy, information gain and split information by hand, and applies
them to the multi-valued columns. Entropy measures how mixed a column is, information gain
measures how much of that mixing a feature removes, and split information is the correction
that stops the measure from favouring a feature simply for having many distinct values,
which is the failure mode plain information gain is known for.

The result is a ranking of the columns by how much they actually tell about the target,
which is the input to any modelling that follows.
