# Exercise 3: Run the nf-core/viralrecon pipeline

In Exercise 2, you used `sierra-local` to predict HIV drug resistance from a consensus sequence. In this exercise, you will start with sequencing reads and run HIV drug-resistance analysis as part of the `nf-core/viralrecon` Nextflow pipeline.

The HIV drug-resistance workflow used in this exercise is available on the `dev` branch. Karolinska Institutet, Karolinska University Laboratory, and the Bioinformatics Unit of Instituto de Salud Carlos III collaborated on the integration. [Sarai Varona](https://github.com/svarona) and [Lili Andersson-Li](https://github.com/LilyAnderssonLee) carried out the original work.

The pipeline supports Illumina and Nanopore sequencing data and can assemble viral genomes and detect low-frequency variants within a host. [nf-core/viralrecon](https://github.com/nf-core/viralrecon/tree/dev)

## Test data

The exercise uses three publicly available samples. All three also appear in the [Stanford HIVdb sequencing-read examples](https://hivdb.stanford.edu/hivdb/by-reads/).

| Accession | Sequencing target |
| --- | --- |
| `DRR030302` | Whole-genome amplicons |
| `SRR4071760` | Protease and reverse transcriptase regions |
| `SRR6937100` | Integrase region |

The pipeline's test dataset retains **0.02%** of the original reads from each sample. [Test data sampling procedure](https://github.com/nf-core/test-datasets/tree/viralrecon#sampling-procedure)

## Run the analysis with the `test_hiv` profile

The `test_hiv` profile provides the sample sheet and parameters for this exercise. Both commands below use Docker, so make sure Docker is running before you start.

1. From the `hiv` directory you created in Exercise 1, activate the Pixi environment. If the environment is already active, continue to the next step.

   ```bash
   pixi shell
   ```

2. Create a working directory and clone the `dev` branch of the pipeline. Run the remaining commands from inside the cloned `viralrecon` directory.

   ```bash
   mkdir -p exercise2
   cd exercise2
   git clone --branch dev https://github.com/nf-core/viralrecon.git
   cd viralrecon
   ```

   The profile's settings are in [`conf/test_hiv.config`](https://github.com/nf-core/viralrecon/blob/dev/conf/test_hiv.config).

3. If you are using GitHub Codespaces, create `custom.config` to limit the CPU, memory, and time available to each task.

   ```bash
   cat > custom.config <<'CONFIG'
   process {
       resourceLimits = [
           cpus: 2,
           memory: '6.GB',
           time: '1.h'
       ]
   }
   CONFIG
   ```

   If your environment has sufficient resources, you can skip this step and omit `-c custom.config` from the command you choose below.

4. Choose one of the following commands. Both use the `test_hiv` profile and write results to `results_test/`.

   **Run the development branch directly from GitHub**

   ```bash
   nextflow run nf-core/viralrecon -r dev -profile test_hiv,docker --outdir results_test -c custom.config
   ```

   **Run the local checkout**

   ```bash
   nextflow run main.nf -profile test_hiv,docker --outdir results_test -c custom.config
   ```

   Allow about 20 minutes for the analysis. The runtime depends on your environment.

5. To resume a run, repeat the same command from the same directory and add `-resume`. Nextflow reuses results from completed tasks when their cache entries and outputs are still available. [How Nextflow resume works](https://seqera.io/blog/demystifying-nextflow-resume/)

Congratulations on completing the exercise! Give yourself a round of applause!

## Bonus

The bonus tips below can help you use `nf-core/viralrecon` in future analyses.

### Run the analysis on your own samples

The `hiv` profile loads the recommended settings for HIV drug-resistance analysis from `conf/hiv.config`. Replace `your_samplesheet.csv` with the path to your sample sheet. The example writes results to `results_hiv/`.

```bash
nextflow run nf-core/viralrecon -r dev -profile hiv,docker \
    --input your_samplesheet.csv \
    --outdir results_hiv
```

To adjust CPU, memory, or time limits for your dataset, put the settings in a custom configuration file and pass its path with `-c custom.config`. [nf-core configuration options](https://nf-co.re/docs/running/configuration/configuration-options)

For help preparing a sample sheet and choosing HIV-specific parameters, see the pipeline documentation. [nf-core/viralrecon HIV usage guide](https://github.com/nf-core/viralrecon/blob/dev/docs/usage.md#hiv)

### Run the analysis with a parameter file

You can save pipeline parameters in a YAML file and pass it to Nextflow with `-params-file`. Open the example file, replace the placeholder paths with paths for your analysis, and run the command from the directory that contains the file. [Example parameter file](example_params.yaml)

```bash
nextflow run nf-core/viralrecon -r dev -profile docker -params-file example_params.yaml
```

## Get help

For questions about the pipeline, use the `#viralrecon` channel on the nf-core Slack workspace. [Join nf-core Slack](https://nf-co.re/join/slack) · [Open #viralrecon](https://nfcore.slack.com/channels/viralrecon)
