# Lessons Learned

## Nextflow and nf-core

Through the installation and execution of nf-core/rnaseq, I learned the fundamentals of reproducible bioinformatics workflows.

### Workflow Management

- Nextflow automates multi-step bioinformatics analyses using workflows.
- nf-core provides community-developed and standardized pipelines built on Nextflow.
- Workflow execution can be resumed using the `-resume` option, avoiding unnecessary recomputation.
- Nextflow caches completed tasks, making it possible to continue analyses after interruptions.

### Containerization

- Docker Desktop must be running when using the Docker profile.
- Containers improve reproducibility by ensuring identical software environments.
- Docker allows complex bioinformatics software stacks to be executed without manually installing every dependency.

### Linux and Command Line Skills

During troubleshooting, I used Linux commands to investigate pipeline behavior:

```bash
nextflow log
tail -100 .nextflow.log
find work -name ".command.err"
dmesg | grep -i killed
```

I learned how to:

- inspect workflow logs
- investigate failed processes
- locate intermediate files
- diagnose execution errors
- navigate large directory structures produced by bioinformatics workflows

### HISAT2 and Genome Indexing

- HISAT2 automatically builds genome indexes from the reference genome.
- Large genomes generate `.ht2l` index files.
- Index files are stored in Nextflow work directories and reused during analysis.
- HISAT2 alignment statistics can be used to evaluate mapping performance.

### Choice of Aligner and Computational Constraints

During this project, I explored different alignment strategies, including HISAT2 and STAR.

HISAT2 was selected because it is often considered more memory-efficient than STAR, making it a suitable choice for a laptop-based analysis environment.

However, despite using HISAT2 and adjusting workflow resource settings, RNA-seq alignment against the *Amphioctopus fangsiao* genome could not be completed on my laptop environment.

Although my laptop was equipped with 32 GB of physical memory, the WSL environment was configured to use approximately 27 GiB of RAM:

```text
RAM : 27 GiB
Swap: 16 GiB
```

During alignment, the Linux kernel reported:

```text
Memory cgroup out of memory
Killed process (hisat2-align-l)
```

Through this experience, I learned that computational requirements depend strongly on the size and complexity of the reference genome.

Even when using a relatively memory-efficient aligner such as HISAT2, a large eukaryotic genome may require more memory than is practically available in a laptop-based analysis environment.

This highlighted the importance of considering both software selection and hardware limitations when designing bioinformatics analyses.

### Workflow Outputs

I learned how nf-core organizes workflow outputs into structured directories.

Examples of generated outputs included:

- FASTQ validation reports
- FastQC quality-control reports
- Trim Galore results
- HISAT2 alignment logs
- Nextflow execution reports
- workflow timelines
- workflow DAG visualizations

Navigating these outputs helped me understand how large bioinformatics workflows are organized and documented.

### Computational Resources

One of the most important lessons involved computational resources.

Initially, parameters such as

```groovy
cpus = 2
memory = 24.GB
```

were simply numbers in a configuration file.

However, after modifying resource settings and investigating workflow failures, I gained a practical understanding of these parameters.

- `cpus` can be viewed as the number of workers assigned to a task.
- `memory` can be viewed as the workspace available to those workers.

Through resource tuning and troubleshooting, I learned how computational resource allocation directly influences workflow performance and stability.

### Troubleshooting

One RNA-seq analysis failed during alignment.

Error:

```text
Killed
(ERR): hisat2-align exited with value 137
```

Further investigation revealed:

```text
Memory cgroup out of memory
Killed process (hisat2-align-l)
```

This showed that:

- exit code 137 often indicates forced termination by the operating system
- Linux OOM (Out Of Memory) logs can be used to diagnose memory issues
- workflow failures are not always caused by software bugs
- bioinformatics analyses frequently require computational resource management

I learned how to investigate workflow failures using:

- `.nextflow.log`
- `.command.err`
- Nextflow work directories
- Linux kernel logs (`dmesg`)

### RNA-seq Analysis

I learned how RNA-seq workflows proceed:

```text
FASTQ
↓
Quality Control
↓
Read Trimming
↓
Genome Indexing
↓
Alignment (HISAT2)
↓
BAM Generation
↓
Quantification
↓
Differential Expression Analysis
```

I also learned how reference genomes and annotation files are supplied to nf-core/rnaseq and how aligners such as HISAT2 and STAR are incorporated into RNA-seq workflows.

### Reproducibility

A key concept I learned was reproducibility.

By using:

- Nextflow
- nf-core
- Docker
- configuration files

the entire workflow can be documented and reproduced by other researchers.

This experience helped me appreciate the importance of reproducible research in modern computational biology.

### Research Skills

The most important lesson was that bioinformatics is not only about running software.

Successful analysis requires:

- understanding workflow structures
- troubleshooting computational problems
- interpreting log files
- managing computational resources
- documenting procedures for reproducibility

Through this project, I learned that solving computational problems is often as important as running the analysis itself.

## Next Steps

- Improve resource management for large RNA-seq datasets.
- Investigate the observed alignment rates (approximately 15–18%).
- Continue the RNA-seq workflow on a higher-memory server at the University of São Paulo (USP) to generate a count matrix.
- Perform downstream analyses, including quantification and differential expression analysis.
- Learn additional nf-core workflows, including ATAC-seq pipelines.
- Continue documenting bioinformatics projects through GitHub.
