# Lessons Learned

## Nextflow and nf-core

Through the installation and execution of nf-core/rnaseq, I learned the fundamentals of reproducible bioinformatics workflows.

### Workflow Management

- Nextflow automates multi-step bioinformatics analyses using workflows.
- nf-core provides community-developed and standardized pipelines built on Nextflow.
- Workflow execution can be resumed using the `-resume` option, avoiding unnecessary recomputation.

### Containerization

- Docker containers are automatically downloaded when a pipeline is executed.
- Docker Desktop must be running when using the Docker profile.
- Containers improve reproducibility by ensuring identical software environments.

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

### HISAT2 and Genome Indexing

- HISAT2 automatically builds genome indexes from the reference genome.
- Large genomes generate `.ht2l` index files.
- Index files are stored in Nextflow work directories and reused during analysis.

### Troubleshooting

One RNA-seq sample failed during alignment.

Error:

```text
Killed (ERR): hisat2-align exited with value 137
```

Further investigation revealed:

```text
Memory cgroup out of memory
Killed process (hisat2-align-l)
```

This showed that:

- exit code 137 often indicates forced termination by the operating system
- Linux OOM (Out Of Memory) logs can be used to diagnose memory issues
- bioinformatics analyses frequently require computational resource management

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

### Research Skills

The most important lesson was that bioinformatics is not only about running software.

Successful analysis requires:

- understanding workflow structures
- troubleshooting computational problems
- interpreting log files
- managing computational resources
- documenting procedures for reproducibility

## Next Steps

- Complete RNA-seq analysis using a higher-memory server.
- Explore parameter optimization in HISAT2.
- Perform downstream analyses such as count matrix generation and differential expression analysis.
- Apply the same workflow concepts to ATAC-seq data.
