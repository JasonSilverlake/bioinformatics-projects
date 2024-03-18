# bioinformatics-projects
This repository contains projects and Python scripts I've developed in Anaconda, showcasing my current Python skills. 

# Bioinformatics Project Using Biopython

## Project Overview

This project focuses on processing DNA sequence data using the Biopython library. It combines multiple DNA sequences from `.seq` files into a single multi-FASTA formatted file, with each sequence's identifier prefixed by its original filename. This is particularly useful for bioinformatics analyses where managing multiple sequences in a standardized format is essential.

## Concept of Biopython

Biopython is a set of freely available tools for biological computation written in Python. It provides capabilities to work with DNA, RNA, and protein sequences, among other features. In this project, Biopython is used to parse sequence data from `.seq` files, manipulate sequence records, and output them in a commonly used format.

## How It Works

1. **Reading Sequence Files**: The script scans a specified directory for `.seq` files, which contain DNA sequence data.
   
2. **Processing Sequences**: For each `.seq` file found, the script reads the file's contents using Biopython's `SeqIO.parse()` function. This function allows for easy handling of sequence data in various formats.

3. **Combining Sequences**: Each sequence record is then modified by prefixing its ID with the filename it originated from. This step ensures uniqueness and traceability of sequences.

4. **Writing to Multi-FASTA File**: All processed sequence records are written to a single output file in FASTA format, facilitating further bioinformatics analysis.

## Rationale

The motivation behind this approach includes:
- **Traceability**: Prefixing sequence IDs with filenames aids in tracing sequences back to their sources.
- **Standardization**: Combining sequences into a multi-FASTA file standardizes the data format, simplifying downstream analyses.
- **Efficiency**: Automating the process saves time and reduces errors compared to manual sequence file management.

## Code Example

Below is a simplified version of the core script logic:

```python
from Bio import SeqIO
import os

input_dir = 'path/to/input/directory'
output_file = 'combined_sequences.fasta'

with open(output_file, 'w') as outfile:
    for filename in os.listdir(input_dir):
        if filename.endswith('.seq'):
            file_path = os.path.join(input_dir, filename)
            for record in SeqIO.parse(file_path, "fasta"):
                record.id = os.path.splitext(filename)[0] + "_" + record.id
                SeqIO.write(record, outfile, "fasta")
