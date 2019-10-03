# Degust

- Visualise RNA-seq differential expression data.
- Perform your own DGE analysis, or use the inbuilt server to analyse from your own "counts" file.

Access a public web service running [Degust](http://degust.erc.monash.edu)

View a [short video](https://www.youtube.com/watch?v=ucucQ_LtZ1g) of the interface in use.

Read a summary on the <a href='http://drpowell.github.io/degust/'>Degust home page</a>.

## Example Screenshots

<a href="docs/images/screenshot-libsize.png"><img src="docs/images/screenshot-libsize.png" width="200"/></a>
<a href="docs/images/screenshot-mds.png"><img src="docs/images/screenshot-mds.png" width="400"/></a>
<br/>
<a href="docs/images/screenshot-boxplot.png"><img src="docs/images/screenshot-boxplot.png" width="200"/></a>
<a href="docs/images/screenshot-mds3d.png"><img src="docs/images/screenshot-mds3d.png" width="400"/></a>

# FAQ

See [FAQ.md](FAQ.md)

# How to Cite

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3258933.svg)](https://doi.org/10.5281/zenodo.3258933)

# Installation

If you do not want to use the [public Degust installation](http://degust.erc.monash.edu), you may install your own.

You first need to grab a copy of Degust.

        git clone git@github.com:Victorian-Bioinformatics-Consortium/degust.git

Degust can be installed in two ways:

1. Perform your own DGE analysis, and use only the [web frontend from Degust](#frontend-installation-only)
2. Install the [frontend and back-end software](#full-installation) to perform analysis and visualise the results.

## Frontend installation only\*

!! Frontend installation is only compatible with `Python 2.x`. `Python 3.x` will return an error with the module `StringIO`.

To use the frontend visualisation, you will need to have done your own DGE analysis with a tool like edgeR or voom. You will need CSV file contain a line per gene, and the following columns:

- ID - containing a unique identifier for each gene (required)
- Adjusted p-value - The adjusted p-value (FDR or similar) for that gene (required)
- Log intensity for each condition - Used to compute the log fold-change (required)
- Average intensity across the conditions - Used for the MA-plot (required)
- Gene info - Arbitrary information columns to display in the gene list table (optional)
- Read counts - Read counts for each replicate, only used for display purposes (optional)

The simplest approach is to download [degust.py](http://drpowell.github.io/degust/dist/latest/degust.py) then run it with your csv file as a parameter. This will create a single HTML page that you view or share. Run `python degust.py --help` to find the parameters to specify the column names for your CSV.

```
python degust.py --help
```

| Required Arguments: | Description                         |
| ------------------- | ----------------------------------- |
| csvfile             | CSV file to process (default stdin) |

---

| Optional Arguments: | Description                                                                                                                                                                                                                                         |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-h, --help`          | show this help message and exit                                                                                                                                                                                                                     |
| `-o OUT, --out OUT`   | Output file (default stdout)                                                                                                                                                                                                                        |
| `--name NAME`         | Name for this DGE comparison                                                                                                                                                                                                                        |
| `--notour NOTOUR`     | Do not show the tour on first load                                                                                                                                                                                                                  |
| `--primary PRIMARY`   | Name for the primary condition that the fold-changes are relative to                                                                                                                                                                                |
| `--avg AVG`           | Name for average intensity column in CSV file                                                                                                                                                                                                       |
| `--fdr FDR`           | Name for "FDR" column in CSV file (default "adj.P.Val")                                                                                                                                                                                             |
| `--logFC LOGFC`       | Comma separated names for "logFC" columns in CSV file                                                                                                                                                                                               |
| `--info INFO`         | Comma separated names for info columns in CSV file                                                                                                                                                                                                  |
| `--counts COUNTS`     | Specify 'count' columns - only used for display in the table. Specify the name of the logFC column then a colon followed by comma separate count columns. Use multiple times for multiple conditions. Example: --counts cond1:cond1-rep1,cond1-rep2 |
| `--link-col LINK_COL` | Name for column to use with "--link-url"                                                                                                                                                                                                            |
| `--link-url LINK_URL` | Gene info URL. Used when double-clicking the gene-table. Any "%s" will be replaced with the value from the specified "--link-col"                                                                                                                   |
| `--tab`               | Specify that the csv file is actually tab delimited                                                                                                                                                                                                 |
| `--cuffdiff`          | Input file is from cuffdiff (gene_exp.diff). This will set the columns automatically. Note this is still experimental                                                                                                                               |

optional arguments can be used to identify the name of the column required in your csv file

### Sample command

```bash
python degust.py degust-1.csv --avg AveExpr --fdr FDR --logFC Keap1KO --info symbol --out index.html
```

## Full installation

See [INSTALL.md](INSTALL.md)

## License

Degust is released under the GPL v3 (or later) license, see <a href='http://github.com/drpowell/degust/blob/master/COPYING.txt'>COPYING.txt</a>
