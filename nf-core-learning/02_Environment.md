# Environment

## Operating System

```text
Ubuntu 24.04.4 LTS (Noble Numbat)
```

## System

```text
Linux 6.6.87.2-microsoft-standard-WSL2
```

## Workflow Management

```text
Nextflow 26.04.6 (build 12646)
```

## Java Runtime

```text
OpenJDK 25.0.3 LTS
Temurin-25.0.3+9
```

## Container Platform

```text
Docker 29.4.1
```

## Memory

```text
RAM : 27 GiB
Swap: 16 GiB
```
Although the laptop was equipped with 32 GB of physical memory, the WSL environment was configured to use approximately 27 GiB of RAM.

## Workflow

- nf-core/rnaseq

## Aligner

- HISAT2

## Reference Genome

- *Amphioctopus fangsiao* genome assembly

## Notes

This project was executed on Ubuntu running under WSL2.
Workflows were managed with Nextflow and executed in Docker containers.

## Project Structure

```text
rnaseq-nextflow/
├── samplesheet.csv
├── custom.config
├── Amphioctopus_fangsiao_19519750/
└── results/
```

