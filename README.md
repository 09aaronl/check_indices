# check_indices
A Python script to check whether distinct indices of NGS libraries can be safely pooled together prior to sequencing.

**check_indices.py version: 1.0** Released: 03/30/2025

**Current functions:**
- `hamming` to calculate hamming distance between pairs of indices
- `diversity` to calculate expected base diversity across all index cycles

**Requirements: python3, numpy, pandas**


## hamming
To calculate pairwise hamming distance, run:
```bash
python check_indices.py hamming (-min, --min_distance <integer>) [input.csv] [output.csv]
```
where:
- `(-min or --min_distance)` is followed by integer. Pairwise Hamming distances less than this value will be flagged in the output. **Optional. Default: 3**
- `[input.csv]` is a path to a comma-separated value (csv) file containing an abbreviated Sample Sheet containing the headers 'Index,percent' or 'Index,Index2,percent'. **Required.**
- `[output.csv]` is a path to a file to which to write the pairwise Hamming distances, as a 2D matrix. **Required.**


## diversity
To calculate base diversity, run:
```bash
python check_indices.py diversity (-max, --max_monotemplate <float>) [input.csv] [output.csv]
```
where:
- `(-max or --max_monotemplate)` is followed by a percentage. Base monotemplate percentages greater than this value will be flagged in the output. **Optional. Default: 65.0**
- `[input.csv]` is a path to a comma-separated value (csv) file containing an abbreviated Sample Sheet containing the headers 'Index,percent' or 'Index,Index2,percent'. **Required.**
- `[output.csv]` is a path to a file to which to write the per-base diversities, as a 2D matrix. **Required.**


## Example
[examples/SampleSheet.csv](./examples/SampleSheet.csv) is an example of the `[input.csv]`.

[examples/hamming.csv](./examples/hamming.csv) is the output of `check_indices.py hamming`.
It was produced by running
```bash
python check_indices.py hamming -min 3 examples/SampleSheet.csv examples/hamming.csv
```

[examples/diversity.csv](./examples/diversity.csv) is the output of `check_indices.py diversity`.
It was produced by running
```bash
python check_indices.py diversity -max 65.0 examples/SampleSheet.csv examples/diversity.csv
```
