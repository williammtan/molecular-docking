# Docking Script (dock.py)

## Overview

This Python script performs molecular docking using the `dockstring` library. It processes input SMILES strings from a CSV file, performs docking, and outputs the docking scores to a CSV file. The script also includes an option to convert SMILES strings to their canonical form using RDKit.

## Requirements

- Python 3.6 or later
- `dockstring`
- `pandas`
- `tqdm`
- `rdkit`
- `openbabel`

## Installation

1. Install the necessary Python packages:
   ```bash
   pip install dockstring pandas tqdm rdkit
   ```
2. Install Open Babel:
   ```bash
   sudo apt-get install openbabel
   ```

## Usage

The script can be run from the command line with the following options:

```bash
python dock.py --input_csv <path/to/input.csv> --smiles_column <SMILES_column_name> --mol2_path <path/to/mol2file.mol2> --output_path <path/to/output.csv> [options]
```

### Required Arguments

- `--input_csv`: URL or path to the input CSV file containing the SMILES strings.
- `--smiles_column`: Column name in the CSV file that contains the SMILES strings.
- `--mol2_path`: Path to the mol2 file of the target protein.
- `--output_path`: Path to the output CSV file where the docking results will be saved.

### Optional Arguments

- `--docking_dir`: Directory name/path where docking files will be stored (default: `dockdir`).
- `--mol_name`: Name of the molecule (default: `mol`).
- `--conf_path`: Path to the configuration file (`_conf.txt`) containing the center and box sizes.
- `--center_coords`: Center coordinates for the docking box (X Y Z). Required if `--conf_path` is not provided.
- `--box_sizes`: Box sizes for docking (X Y Z). Required if `--conf_path` is not provided.
- `--canonicalize`: Flag to convert SMILES to canonical SMILES.

### Examples

#### Using center coordinates and box sizes:

```bash
python dock.py --input_csv path/to/your/input.csv --smiles_column SMILES --mol2_path path/to/mol2file.mol2 --output_path path/to/output.csv --center_coords 68.0658 -5.1678 -54.97 --box_sizes 98.194 95.5592 116.24 --canonicalize
```

#### Using a configuration file:

```bash
python dock.py --input_csv path/to/your/input.csv --smiles_column SMILES --mol2_path path/to/mol2file.mol2 --conf_path path/to/conf.txt --output_path path/to/output.csv --canonicalize
```

### Format for `_conf.txt` File

If you choose to use a configuration file for the docking box parameters, the `_conf.txt` file should have the following format:

```
center_x = <center_x_value>
center_y = <center_y_value>
center_z = <center_z_value>

size_x = <size_x_value>
size_y = <size_y_value>
size_z = <size_z_value>
```

For example:

```
center_x = 68.0658
center_y = -5.1678
center_z = -54.97

size_x = 98.194
size_y = 95.5592
size_z = 116.24
```

### Notes

- Ensure that the input CSV file contains the correct column name for SMILES strings.
- If using the `--canonicalize` flag, RDKit will be used to convert SMILES strings to their canonical form.
- If the configuration file (`_conf.txt`) is not provided, the script requires the center coordinates and box sizes to be specified.

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Acknowledgments

- [Dockstring](https://github.com/rosenbjerg/dockstring)
- [RDKit](https://www.rdkit.org/)
- [Open Babel](http://openbabel.org/wiki/Main_Page)

Feel free to reach out with any questions or issues regarding the script. Happy docking!