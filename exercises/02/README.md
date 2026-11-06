# Exercise 2: Run sierra-local and check the HIV drug resistance database

[sierra-local](https://github.com/PoonLab/sierra-local) is a local implementation of the Stanford HIVdb algorithm for mutation-based resistance scoring using consensus sequences.

## sierra-local arguments

1. Actiavte the pixi environment installed in the previous analysis

    ```bash
    cd hiv/
    pixi shell
    ```

2. Check the arguments of `sierra-local`.
   The default HIV database used for the analysis is not the latest. You can either pre-download the latest database and provide it as an argument, or you can use the `--forceupdate` argument to update the database to the latest version during the analysis.

    ```
    $ sierralocal -h
    usage: sierralocal [-h] [-o OUTFILE] [-xml XML] [-json JSON] [--cleanup] [--forceupdate] [-alignment {post,nuc}] [-apobec_csv APOBEC_CSV] [-unusual_csv UNUSUAL_CSV] [-sdrms_csv SDRMS_CSV] [-mutation_csv MUTATION_CSV]
                       [-updater_outdir UPDATER_OUTDIR]
                       fasta [fasta ...]

    Local execution of Stanford HIVdb algorithm for mutation-based resistance scoring of sequences.

    positional arguments:
      fasta                 List of input files.

    options:
      -h, --help            show this help message and exit
      -o OUTFILE            Output filename.
      -xml XML              <optional> Path to HIVdb ASI2 XML file (default: HIVDB_9.4.xml)
      -json JSON            <optional> Path to JSON HIVdb APOBEC DRM file
      --cleanup             Deletes NucAmino alignment file after processing.
      --forceupdate         Forces update of HIVdb algorithm. Requires network connection.
      -alignment {post,nuc}
                            Alignment program to use, "post" for post align and "nuc" for nucamino
      -apobec_csv APOBEC_CSV
                            <optional> Path to CSV APOBEC csv file (default: apobecs.csv)
      -unusual_csv UNUSUAL_CSV
                            <optional> Path to CSV file to determine if is unusual (default: rx-all_subtype-all.csv)
      -sdrms_csv SDRMS_CSV  <optional> Path to CSV file to determine SDRM mutations (default: sdrms_hiv1.csv)
      -mutation_csv MUTATION_CSV
                            <optional> Path to CSV file to determine mutation type (default: mutation-type-pairs_hiv1.csv)
      -updater_outdir UPDATER_OUTDIR
                            <optional> Path to folder to store updated files from updater (default: sierralocal/data folder)
    ```

## HIV drug resistance database

The database used by `sierra-local` is originally from [Stanford HIVdb](https://hivdb.stanford.edu/hivdb/by-patterns/).
For a better understanding of the HIV drug-resistance testing database, we need to clone the `sierral-local` repository locally.

1. Create a folder for your exercise outside of the pixi environment:

    ```bash
    cd ../hiv
    mkdir -p exercise1
    cd exercise1
    ```

2. Clone the sierra-local repo:

    ```bash
    git clone https://github.com/PoonLab/sierra-local.git
    ```

3. Download the latest HIVdb and save it to the `sierralocal/data` folder. You can also re-direct the output to a different folder
    with the `-update_outdir` argument, if you want to save it somewhere else.

    ```bash
    python3 sierralocal/updater.py # saved in sierralocal/data folder
    ```

4. Check the latest HIVdb in the `sierra-local/sierralocal/data` folder on the left side of the window.

    Some files are hardcoded in `sierra-local`, but the following files can be updated to the latest version:

    ```bash
    HIVDB_10.2.xml                  - XML file containing the HIVdb algorithm.
    apobec_drms.json                - JSON file containing the APOBEC DRM data.
    apobec.csv                      - CSV file containing the APOBEC mutations.
    mutation-type-pairs_hiv1.csv    - CSV file containing the mutation type pairs.
    rx-all_subtype-all.csv          - CSV file containing the unusual mutations.
    sdrms_hiv1.csv                  - CSV file containing the SDRM mutations.
    ```

## sierra-local test run

1. Download a test dataset from the `sierra-local` repository:

    ```bash
    python3 scripts/retrieve_hivdb_data.py RT RT.fa

    ```

2: Run `sierra-local`. For usage of `sierra-local`, you can either check the online [tutorial](https://github.com/PoonLab/sierra-local/tree/dev)
    or check the `README.md` file in the cloned sierra-local repository. There are two ways to run `sierra-local`:

- Option1: include the `--forceupdate` argument to update the database to the latest version during the analysis.

    ```bash
    sierralocal --forceupdate -updater_outdir hivdb_latest RT.fa -o RT_results.json
    ```

- Option2: use the pre-downloaded latest HIVdb in the `sierralocal/data` folder.

    ```bash
    sierralocal RT.fa -o RT_results.json \
        -xml sierralocal/data/HIVDB_10.2.xml \
        -json sierralocal/data/apobec_drms.json \
        -apobec_csv sierralocal/data/apobecs.csv \
        -unusual_csv sierralocal/data/rx-all_subtype-all.csv \
        -sdrms_csv sierralocal/data/sdrms_hiv1.csv \
        -mutation_csv sierralocal/data/mutation-type-pairs_hiv1.csv
    ```

3. View the result JSON file on the left side of the window or in the terminal with the `less` command:

    ```bash
    less RT_results_v1.json
    ```

## Take home message

You can run `sierra-local` locally for the HIV drug resistance scoring algorithm using the consensus sequence data.

`sierra-local` uses the HIVdb database originally from [Stanford HIVdb](https://github.com/hivdb/hivfacts/tree/main/data)

Please remember to update the database to the latest version for your analysis.