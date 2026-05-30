# Course material for: GenEpi-BioTrain VT27: Clinical application of Nanopore-based 16S metagenomic sequencing for diagnostics

Project repo for following course on bioinformatics for 16S sequencing analysis
on ONT, to be given at the ECDC course portal in June 2026:

[GenEpi-BioTrain - Virtual Training 27 - Clinical application of Nanopore-based 16S metagenomic sequencing for diagnostics](https://learning.ecdc.europa.eu/enrol/index.php?id=1258)

## Exercises

For the exercises, see the `/exercises` folder, or the links below:

1. [Exercise 1: Install and run Emu](https://github.com/kclinmicro/16s-ont-course/tree/main/exercises/01)
3. [Exercise 2: Troubleshoot Emu outputs](https://github.com/kclinmicro/16s-ont-course/tree/main/exercises/02)
2. [Exercise 3: Install and run Trana and TranaVy via install script](https://github.com/kclinmicro/16s-ont-course/tree/main/exercises/03)

## Some GitHub codespaces caveats

If you are using GitHub codespaces to run the exercises, we noticed a few small
caveats that can help improving the experience.

1. Sometimes the prompt string (the part just before your cursor), can get
   messed up so you don't see what you write. Ctrl+L doesn't even help then.
   What helps though is to clear the terminal with `clear`.
2. Sometimes the prompt can get so long that it is hard to read your own command.
    You can set a shorter prompt string, e.g. by running:

    ```bash
    export PS1="[\W]$ "
    ```

    which will only print the current working directory in square brackets, and
    a dollar sign. An even simpler version with just a dollar sign, would be:

    ```bash
    export PS1="$ "
    ```
