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
### Running Prodigal on Multiple Genomes
### Unzip the Genomes File
```bash
unzip NCBI_dataset.zip -d genomes/
```
This extracted the genomes into a directory named genomes/.
### Output
```
@hernanym ➜ /workspaces/Week-5 (main) $ unzip NCBI_dataset.zip -d genomes/
Archive:  NCBI_dataset.zip
   creating: genomes/NCBI_dataset/
  inflating: genomes/NCBI_dataset/GCA_000006745.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000006825.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000006865.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000007125.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000008525.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000008545.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000008565.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000008605.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000008625.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000008725.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000008745.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000008785.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000027305.1.fna  
  inflating: genomes/NCBI_dataset/GCA_000091085.2.fna 
```
Files have been successfully extracted. Now, you can proceed with running Prodigal on these genome files and counting the genes.

### Script
''' bash 
genome_dir="genomes/NCBI_dataset/"
output_dir="prodigal_outputs/"

#Create a directory to store Prodigal outputs
mkdir -p $output_dir

 #Loop through all genome files in the directory
for genome in $genome_dir/*.fna; do
    # Get the base name of the genome file (without the directory and extension)
    base_name=$(basename "$genome" .fna)
    
    # Run Prodigal on the genome file
    prodigal -i "$genome" -o "$output_dir/${base_name}.gff" -f gff
    
    # Count the number of CDS (genes) in the GFF file
    num_genes=$(grep -c "CDS" "$output_dir/${base_name}.gff")
    
    # Print the genome file and the gene count
    echo "$base_name: $num_genes"
done
'''
### Run Script 
'''bash 
@hernanym ➜ /workspaces/Week-5 (main) $ genome_dir="genomes/NCBI_dataset/"
@hernanym ➜ /workspaces/Week-5 (main) $ output_dir="prodigal_outputs/"
@hernanym ➜ /workspaces/Week-5 (main) $ mkdir -p $output_dir
@hernanym ➜ /workspaces/Week-5 (main) $ for genome in $genome_dir/*.fna; do
> base_name=$(basename "$genome" .fna)
> prodigal -i "$genome" -o "$output_dir/${base_name}.gff" -f gff
> num_genes=$(grep -c "CDS" "$output_dir/${base_name}.gff")
> echo "$base_name: $num_genes"
> done
'''
### Output 
'''
GCA_000006745.1: 3594
GCA_000006825.1: 2032
GCA_000006865.1: 2383
GCA_000007125.1: 3152
GCA_000008525.1: 1579
GCA_000008545.1: 1866
GCA_000008565.1: 3248
GCA_000008605.1: 1009
GCA_000008625.1: 1776
GCA_000008725.1: 897
GCA_000008745.1: 1063
GCA_000008785.1: 1505
GCA_000027305.1: 1748
GCA_000091085.2: 1063
'''
### Genome with Highest Number of Genes: 
```
GCA_000006745.1, with 3,594 genes.
```
### Save Gene Counts to a File Using Bash
```bash
for genome in $genome_dir/*.fna; do
    base_name=$(basename "$genome" .fna)
    prodigal -i "$genome" -o "$output_dir/${base_name}.gff" -f gff
    num_genes=$(grep -c "CDS" "$output_dir/${base_name}.gff")
    echo "$base_name: $num_genes"
done > genome_gene_counts.txt
```
The > genome_gene_counts.txt part at the end of the loop redirects all the output into a file named genome_gene_counts.txt.
### You can check the contents of the file by running:
```bash
cat genome_gene_counts.txt
```
