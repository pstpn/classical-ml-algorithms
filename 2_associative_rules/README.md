# Association rules

Finding the sets of goods that are bought together, with the classical algorithm written out
and a faster one from a library kept beside it as a control.

## Data

The Online Retail dataset, half a million invoice lines from a UK gift wholesaler, reshaped
into baskets so that each invoice becomes the set of items it contains.

## Method

`apriori.py` implements Apriori, which grows candidate itemsets one element at a time and
prunes any candidate with an infrequent subset, since a set cannot be more frequent than its
parts. `rules.py` turns the frequent sets into rules and scores them by support, confidence
and lift, where lift is the one that matters — confidence alone rewards any rule pointing at
a popular item, while lift asks whether the items appear together more often than chance
would explain.

FP-Growth from `mlxtend` is run over the same baskets. It avoids generating candidates at
all by compressing the transactions into a prefix tree, which is what makes it the practical
choice at this size.

## What comes out

Both find the same rules at the same thresholds, which is the check that the hand-written
version is correct. The difference is in cost, since Apriori rescans the transactions for
every level of itemset while FP-Growth builds its tree once.
