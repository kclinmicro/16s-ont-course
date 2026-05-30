# Exercise 2: Install and run the Emu-based Trana pipeline

In this exercise we will install the
[Trana](https://github.com/genomic-medicine-sweden/TRANA) pipeline, developed
by [Frans Wallin](https://www.linkedin.com/in/frans-wallin-4bb570153/), [Ryan Kennedy](https://www.linkedin.com/in/ryan-james-kennedy/), us at Karolinska and others within Genomic
Medicine Sweden, and which includes [Emu](https://github.com/treangenlab/emu)
as a module, together with some quality checking and filtering software, as
well as some modules for showing results graphically, such as
[Krona](https://github.com/marbl/Krona/wiki) and the [TranaVy](https://github.com/kclinmicro/TranaVy)
reporting tool developed by us, and more.

Since the installation of all these tools can be quite complex, we will be
using an [Ansible](https://docs.ansible.com/) installation script developed by
us, which installs all the tools and scripts needed to run the pipeline, with a
single command.

The script is optimized for use on GridIon instruments, which Ubuntu Linux, but
generally works well on most Ubuntu-like Linuxes, including on GitHub
codespaces. Only some adjustments to the available CPUs and memory will be
needed below.

The only initial step is installing Ansible, but that is generally very easy.

## Installing Trana and TranaVy via Ansible

1. Install Ansible

    Ansible is available via the Ubuntu package repository, so can be installed via apt:

    ```bash
    sudo apt update
    sudo apt install ansible
    ```

2. Clone and run the install script repo

    The install script repo is supposed to be in a specific directory:
    `/data/trana/install`, which is under the `/data` folder where all sequencing
    data is stored on GridIon instruments. This, we start by creating this folder:

    ```bash
    sudo mkdir -p /data/trana/install
    ```

    And then we change ownership of the whole data folder to our current user,
    so that we can create files in it without sudo:

    ```bash
    sudo chown -R codespace:codespace /data
    ```

    ... and finally we enter it:

    ```bash
    cd /data/trana/install
    ```

    Here, we clone the repository to the current folder (which is why we end
    with the `.`, to mark the current folder):

    ```bash
    git clone https://github.com/genomic-medicine-sweden/trana-setup-gridion.git .
    ```

3. Run the install script

    Now we are ready to run the install script.

    In order to simplify this even more, we have added a Makefile with a rule to run
    it, so we only need to do:

     ```bash
     make install
     ```

     This will run the Ansible install script on our local machine.

## Run Trana on example data

Now we are ready to try running TRANA on some example data. To start with, we
thus need to download some data to run on, and put it in the `/data` folder.
Then we can use a script included in the install library, that will detect new
data and run Trana on it.

1. Download test data

    Enter the `/data` folder:

    ```bash
    cd /data
    ```

    Now download the test data tarball:

    ```bash
    wget https://github.com/kclinmicro/16s-ont-course/releases/download/v0.0.1/16s-course-data.tar.gz
    ```

    And untar it:

    ```bash
    tar -zxvf 16s-course-data.tar.gz
    ```

    Now we copy the `16s_ont_example` folder directly under `/data`, where we are already:

    ```bash
    cp -r data/16s_ont_example .
    ```

    So now, this folder should be in: `/data/16s_ont_example`.

    The start script we will now use detects all data folders starting with
    `16s_ont_*`, so it is important that we keep this part of the name as is.

2. Now another thing we need before staring, is to have a "barcode sheet",
   which maps the barcodes used in the sequencing, to sample names. The run
   script we will use expect such a barcode file in the
   `/data/trana/barcodesheets` directory, with the same name as the data
   folder, but ending with `.csv`.

   We have already created a barcodesheet for you, which is available in the
   data we just downloaded, so we just need to put this file in the correct place:

   We create the folder:

   ```bash
   mkdir -p /data/trana/barcodesheets
   ```

   ... and put the barcodesheet there:

   ```bash
   cp 16s_ont_example/16s_ont_example.csv /data/trana/barcodesheets
   ```

3. Adjust CPU and memory settings for Nextflow

    The last thing we need to do is to adjust the max CPU and memory settings,
    which are optimized for GridIon in the config file shipped with the test
    script.

    If we run on GitHub codespaces, or a local laptop, we need to adjust these.

    If you are on GitHub codespaces, open the file
    `/data/trana/install/gridion.config` and change according to this diff:

    ```diff
    params {
    -    max_memory = '60.GB'
    -    max_cpus   = 16
    +    max_memory = '6.GB'
    +    max_cpus   = 2
         max_time   = '72.h'
     }

     process {
         resourceLimits = [
    -        cpus: 16,
    -        memory: '60.GB',
    +        cpus: 2,
    +        memory: '6.GB',
             time: 72.h
    ]
    ```

    If you are using a local laptop, you might be able to use a slightly higher
    number of cores and memory, depending on your laptop's hardware specs.


4. Now we are ready to run the pipeline using the start script.

    We first move to the run folder, where the run scripts are and where also
    all logs will be stored, in a `logs` folder:

    ```bash
    cd /data/trana/run
    ```

    ... and then we run the run script:

    ```bash
    ./detect-data-and-run.sh
    ```

    **(TO BE CONTINUED!)**
