# Installation

## Objective

Learn how to install and run Nextflow as a workflow manager for bioinformatics pipelines.

## Reference

The installation process was mainly based on the following tutorial:

- Zenn, "Nextflowのチュートリアル",(https://zenn.dev/reprod_x_ngs/articles/90a6dd69e785d5)

## Environment

- Ubuntu 24.04.4 LTS (WSL2)
- OpenJDK 25.0.3 LTS
- Docker 29.4.1
- Nextflow 26.04.6

## Installation Steps

### 1. Install Nextflow

```bash
curl -s https://get.nextflow.io | bash
```

This command downloads the Nextflow executable.

### 2. Make the file executable

```bash
chmod +x nextflow
```

### 3. Move Nextflow to a system path

```bash
sudo mv nextflow /usr/local/bin
```

This allows Nextflow to be executed from any directory.

### 4. Verify installation

```bash
nextflow info
```

Output:

```text
Version: 26.04.6 build 12646
Runtime: Groovy 4.0.31
Java: OpenJDK 25.0.3+9-LTS
System: Linux 6.6.87.2-microsoft-standard-WSL2
```

## Additional Software

### Java

```bash
java --version
```

Output:

```text
openjdk 25.0.3 2026-04-21 LTS
OpenJDK Runtime Environment Temurin-25.0.3+9
```

### Docker

```bash
docker --version
```

Output:

```text
Docker version 29.4.1
```


