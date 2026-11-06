# Exercise 1: Installation

Install tools needed for the exercises in the course:

- [sierra-local](https://github.com/PoonLab/sierra-local)
- [nextflow](https://github.com/nextflow-io/nextflow)

*(Note that you can view an outline of this document by clicking the icon that
looks like a bullet point list, to the far right just above the header above)*

## Dependencies

This guide assumes you have access to a Linux environment, as highlighted in
the [preparations information](https://learning.ecdc.europa.eu/course/view.php?id=1258#section-2).

HIV drug-resistance testing will be performed using `sierra-local`, which is integrated into the `nf-core/virlarecon` nextflow pipeline.
To run `sierra-local` and `nf-core/viralrecon`, you also need to set up a Conda or Pixi environment.

In this guide, we will go with Pixi, as it is, in our experience, faster and more
robust than Conda.

## Setting up nextflow and sierra-local from Bioconda with Pixi

Below is a guide on how to set up tools through the bioconda repository, but
using Pixi instead of Conda, for greater speed and flexibility.

1. Install Pixi
  - The easiest way is to run the official install script from the [webpage](https://prefix.dev):

    ```bash
    curl -fsSL https://pixi.sh/install.sh | bash
    ```

    But there are [alternative installation methods](https://pixi.prefix.dev/latest/installation/#alternative-installation-methods) too.
2. Reload your shell, for example by executing bash again:

    ```bash
    bash
    ```

3. Create a folder for your exercise:

    ```bash
    mkdir -p hiv
    cd hiv
    ```

4. Create a new pixi environment in this folder:

    ```bash
    pixi init -c conda-forge -c bioconda
    ```

   This will create a file called `pixi.toml` inside the current folder.

5. You can now run `pixi shell`,
   so that all installed software is available in your `$PATH` variable:

   ```bash
   pixi shell
   ```

   You can see that you have the pixi environment loaded by the `(hiv)` part
   added to the left in your terminal.

6. Now you can install nextflow via Pixi:

    ```bash
    pixi add nextflow=25.10.4 sierra-local=0.4.4 python=3.10 tree
    ```

7. Done! Now you should be able to check that `nextflow` and `sierra-local` are installed with:

    ```bash
    nextflow -h
    sierralocal -h
    ```

## Take home message

How to use `pixi` to install and manage software for the exercises.
