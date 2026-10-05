## HISAT2 Alignment Statistics

The nf-core/rnaseq workflow did not successfully complete because the HISAT2 alignment process was terminated by an out-of-memory (OOM) event.

Despite the workflow failure, HISAT2 summary logs were generated for several samples, providing preliminary alignment statistics.

### S1

```text
Total pairs: 21,191,247
Overall alignment rate: 17.98%
```

### S2

```text
Total pairs: 22,045,059
Overall alignment rate: 17.36%
```

### S3

```text
Total pairs: 23,153,392
Overall alignment rate: 15.51%
```

### S5

```text
Total pairs: 23,546,628
Overall alignment rate: 15.53%
```

### Summary

| Sample | Total Pairs | Alignment Rate |
|---------|------------:|---------------:|
| S1 | 21,191,247 | 17.98% |
| S2 | 22,045,059 | 17.36% |
| S3 | 23,153,392 | 15.51% |
| S5 | 23,546,628 | 15.53% |

Although the workflow did not finish successfully, alignment summary logs were produced before termination.

The observed mapping rates ranged from approximately 15% to 18%, indicating that reads were successfully aligned to the reference genome, but at a relatively low rate.

Further investigation will be required to determine whether the observed alignment rates are associated with:

- reference genome quality
- annotation quality
- sequencing quality
- alignment parameters
- computational limitations during alignment

Although HISAT2 generated alignment summaries, the workflow ultimately terminated because of an out-of-memory (OOM) event.

Therefore, it remains possible that memory limitations affected the overall alignment process and downstream analyses.
``
