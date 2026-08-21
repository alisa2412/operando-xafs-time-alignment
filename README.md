# operando-xafs-time-alignment
A Python workflow developed during a Faraday Institution FUSE placement to
time-match operando Ni K-edge XAFS spectra with electrochemical voltage and
capacity data.

## What it does

- Reads and preprocesses XAFS spectra using Larch.
- Extracts the Ni K-edge position, E0, using two definitions:
  derivative maximum and normalised half-height, μ(E) = 0.5.
- Uses XAFS file timestamps to define each scan acquisition interval.
- Matches each scan to an overlapping window of raw electrochemical data.
- Calculates time-weighted mean voltage and capacity for every XAFS scan.
- Produces a combined table and comparison plots.

## Why time weighting?

Electrochemical measurements may not be equally spaced in time. Each value is
weighted by the duration it represents, so densely sampled regions do not
dominate the average assigned to an XAFS scan.

## Requirements

Python 3, NumPy, pandas, matplotlib, and Larch.

## Data

This repository does not include unpublished experimental data. Users should
provide their own time-stamped XAFS files and electrochemical data.

## Data setup

Place the input files in a folder named `data` in the same directory as the notebook:

```text
operando-xafs-time-alignment/
├── operando-xafs-time-alignment.ipynb
└── data/
    ├── LNO_freshcell_highvoltage_C01.csv
    ├── scan_001.dat
    ├── scan_002.dat
    └── ...
```

The notebook searches for XAFS files using:

```python
data_dir = 'data'
filepaths = sorted(glob.glob(os.path.join(data_dir, '*.dat')))
```

Therefore, all XAFS `.dat` files must be placed in the `data/` folder.

The electrochemical file is currently loaded using:

```python
ec = pd.read_csv('data/LNO_freshcell_highvoltage_C01.csv')
```

To use a different electrochemical file, place it in the `data/` folder and update the filename in this line. The CSV is expected to contain time, voltage, current and capacity columns in the same order as the supplied dataset.

## Author

Alisa Yakovenko, BSc (Hons) Physics, University of Edinburgh.

Developed during a Faraday Institution FUSE placement with Galo Páez Fajardo.
