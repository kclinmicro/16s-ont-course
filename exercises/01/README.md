# Exercise 1: Install and run Emu

## Dependencies

This guide assumes you have access to a Linux environment, as highlighted in
the [preparations information](https://learning.ecdc.europa.eu/course/view.php?id=1258#section-2).

To run Emu, you also need to set up a Conda or Pixi environment.

In this guide we will go with Pixi, as it is in our experience faster and more
robust than Conda.

## Setting up Emu from Bioconda with Pixi

Below is a guide on how to set up Emu through the bioconda repository, but
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

3. Create a folder for your exercise with Emu:

    ```bash
    mkdir -p ex1
    cd ex1
    ```

4. Create a new pixi environment in this folder:

    ```bash
    pixi init
    ```

   This will create a file called `pixi.toml` inside the current folder.
5. Open the file in an editor and change the line:

    ```toml
    channels = ["conda-forge"]
    ```

    ... to:

    ```toml
    channels = ["conda-forge", "bioconda"]
    ```

6. After saving the above change in `pixi.toml`, you can now run `pixi shell`,
   so that all installed software are available in your `$PATH` variable:

   ```bash
   pixi shell
   ```

   You can see that you have the pixi environment loaded by the `(ex1)` part
   added to the left in your terminal.
   - A small caveat if you run GitHub codespaces and your prompt string is very long, is that you can:
      - Clear the terminal properly with the `clear` command.
      - Set a shorter prompt string, e.g. by running `export PS1="[\W]$ "`,
        which will only print the current working directory in square brackets,
        and a dollar sign. An even simpler version with just a dollar sign,
        would be `export PS1="$ "`.
7. Now you can install Emu via Pixi:

    ```bash
    pixi add emu
    ```

8. Done! Now you should be able to check that Emu is installed, with:

    ```bash
    emu -h
    ```

    ... and, for the central command:

    ```bash
    emu abundance -h
    ```

## Run Emu on some test data

- **May 30, 2026: This part is currently being updated**
