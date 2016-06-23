# p53-chip-seq-go

Generate GO results table/graphs for P53 genomics project

run script: `./run.sh` (see "Building" section)

## About

The purpose of this assignment is to determine highly enriched GO terms

Originally, terms were filtered to those which matched keywords such as 'cell death', 'apoptosis', and 'caspase'. However, filtering based on the keywords did not 

## Data Source

GO analysis files generated from Homer analysis of P53 ChIP-Seq files

## Process

For each folder in the DmGOs directory, there is a `geneOntology.html` file.

For each `geneOntology.html` file, top 10 rows with lowest p-value are outputted to a results file with the term, p-value, and level 4 ancestor traceback. The level 4 ancestor traceback may contain multiple terms, including the original term if it is level 4. Level 4 is used because higher levels (0~3) are too generic.

The level 4 traceback is based on the Gene Ontology data file from [http://geneontology.org/page/download-ontology]().


## Requirements

1. beautifulsoup4
2. goatools
  * fisher
    * numpy

## Directory tree

The following directory tree is assumed by `Assignment2.py`:

```
Assignment2
│
├───assignment2 (this Git repository)
│   │   Assignment2.py
│   │   run.sh
│   │   go-basic.obo
│   │   ...
│   │
│
│
└───DmGOs
    ├───Kc167_P53_NT60_A_GO
    │   │   geneOntology.html
    │   │   ...
    │
    ├───Kc167_P53_NT60_B_GO
    │   ...
```

## Setting up directories on HPC

Make sure you have properly configured your HPC account's Git settings AND added your HPC SSH key to your GitHub account. ([wiki](https://github.com/zhoulab/assignment-2/wiki/Using-GitHub-with-HPC))

1. Log in to HPC:

    ```
    ssh <YOUR_HPC_USERNAME>@hipergator.rc.ufl.edu
    ```

2. Make a directory for the project:

    ```
    mkdir Assignment2
    ```

3. Make a directory for the GO folders (we will need to populate it using `scp` outside of the SSH session): 

    ```
    mkdir Assignment2/DmGOs
    ````

4. Clone this git repository (will create under the `Assignment2` directory:

    ```
    git clone git@github.com:zhoulab/assignment-2.git Assignment2/assignment2
    ```

5. Exit the SSH session (`CTRL+D`) and copy an existing DmGOs folder from your local machine into the `DmGOs` directory.

    ```
    scp -r /path/to/local/DmGOs <YOUR_HPC_USERNAME>@hipergator.rc.ufl.edu:/path/to/desired/DmGOs
    ```

## Building

Make sure you are in the `assignment2` directory.

Run `Assignment.py` with `python` and `virtualenv`:

```
./run.sh
```

The repository comes with a virtual environment (`ve/`). If `run.sh` does not work, try the teardown and bootstrap process:

```
./teardown.sh
```

```
./bootstrap.sh
```
