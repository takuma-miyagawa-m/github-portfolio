# Commands

This document records the major commands used while learning Nextflow and running the nf-core/rnaseq workflow.

---

## Step 1: Learn Nextflow Basics

Run the tutorial workflow.

```bash
nextflow run tutorial.nf
```

Re-run the workflow using cached results:

```bash
nextflow run tutorial.nf -resume
```

---

## Step 2: Run nf-core Test Dataset

Test the nf-core/rnaseq workflow.

```bash
nextflow run nf-core/rnaseq \
    -r 3.26.0 \
    -profile test,docker \
    --outdir test_results
```

---

## Step 3: Run RNA-seq Analysis

Run nf-core/rnaseq using a custom reference genome.

```bash
nextflow run nf-core/rnaseq \
    -r 3.26.0 \
    -profile docker \
    -c custom.config \
    --input samplesheet.csv \
    --fasta Amphioctopus_fangsiao_19519750/Chr_genome.fasta \
    --gff Amphioctopus_fangsiao_19519750/Chr_genome_final_gene.gff3 \
    --aligner hisat2 \
    --outdir results \
    -resume
```

---

## Step 4: Resource Optimization

Modified resource allocation using a custom configuration file.

custom.config

```groovy
process {

    resourceLimits = [
        cpus: 4,
        memory: 24.GB
    ]

    maxForks = 1

    withName: '.*HISAT2_ALIGN.*' {
        cpus = 2
        memory = 24.GB
        maxForks = 1

        ext.args = '--very-sensitive --mp 2,1'
    }

}
```
### Why I Modified custom.config

The default workflow configuration resulted in repeated failures during HISAT2 alignment.

To reduce memory pressure and simplify debugging, I modified the workflow configuration by:

- limiting the maximum number of concurrent processes (`maxForks = 1`)
- restricting CPU allocation
- allocating more memory to the HISAT2 alignment step
- adjusting HISAT2 alignment parameters

The `--very-sensitive --mp 2,1` option was added to test whether alignment sensitivity could be improved and potentially increase the observed mapping rate.

---

## Step 5: Alternative Alignment Test

Run the workflow using STAR.

```bash
nextflow run nf-core/rnaseq \
    -r 3.26.0 \
    -profile docker \
    -c custom.config \
    --input samplesheet_S1.csv \
    --fasta Amphioctopus_fangsiao_19519750/Chr_genome.fasta \
    --gff Amphioctopus_fangsiao_19519750/Chr_genome_final_gene.gff3 \
    --aligner star_salmon \
    --outdir results_star_s1
```

---

## Step 6: Troubleshooting

Inspect Nextflow logs.

```bash
nextflow log
```

```bash
tail -100 .nextflow.log
```

```bash
tail -f .nextflow.log | grep HISAT2
```

Inspect process errors.

```bash
cat .command.err
```

Inspect Linux kernel messages.

```bash
dmesg | grep -i killed
```
