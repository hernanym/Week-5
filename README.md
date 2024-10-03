# Week-5 Genome Annotation
## Question 1: 
Given the amino acid sequence "KVRMFTSELDIMLSVNGPADQIKYFCRHWT", what is the number of amino acids in the encoded peptide (not including the stop codon)? How many bases are contained in the open reading frame of the DNA sequence encoding the amino acids (including the stop codon)?

## Using genome_annotation.py: 
```python
def calculate_orf_info(amino_acid_sequence):
    
    # Calculate the number of amino acids in the sequence
    num_amino_acids = len(amino_acid_sequence)
    
    # Calculate the number of bases in the ORF (3 bases per amino acid + 3 bases for stop codon)
    num_bases_in_orf = (num_amino_acids * 3) + 3
    
    return num_amino_acids, num_bases_in_orf

# Example usage
amino_acid_sequence = "KVRMFTSELDIMLSVNGPADQIKYFCRHWT"
amino_acids_count, orf_bases_count = calculate_orf_info(amino_acid_sequence)

print(f"Number of amino acids: {amino_acids_count}")
print(f"Number of bases in ORF (including stop codon): {orf_bases_count}")
```
## To Run: 
```bash
python genome_annotation.py 
```
Output 
```
Number of amino acids: 30
Number of bases in ORF (including stop codon): 93
```
## Question 2: 
Run prodigal on one of the genomes you have previously downloaded. Using command line tools, count how many genes were annotated
### Prodigal Installation
Prodigal is already installed in the Codespaces environment, but if you need to install it on a new system, you can use the following command:
```bash
sudo apt-get install prodigal
```
### Run Prodigal for Gene Annotation
Run Prodigal on the genome file (GCA_000006745.fasta) and output the results in GFF format:
```bash
prodigal -i GCA_000006745.fasta -o output.gff -f gff
```
**-i**: Specifies the input genome file.
**-o**-o: Specifies the output file (output.gff).
**-f**: Specifies the format of the output (in this case, gff).
### Count the number of CDS (Genes) Annotated 
```bash
grep -c "CDS" output.gff
```
### Output
```bash
3594
```
## Question 3: 


## Code Breakdown 
### 1a. Take command line parameters for a FASTA file containing a genome 
```python
'''
LLM: ChatGPT (Python) 4o

Prompt: 
How do I write a python code that takes command-line parameters for an input file? 
The input file will consist of a FASTA file containing a genome.

'''
