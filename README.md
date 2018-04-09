# SQUAT - a Sequencing Quality Assessment Tool for Data Assessments before and after Genome Assemblies

SQUAT stands for **Sequencing QUality Assessment Tool**. It allows users to examine if their sequencing reads are truly representative of the original specie based on data assessments before and after genome assemblies. 

The tool aligns sequencing reads against the assembly with **[BWA](http://bio-bwa.sourceforge.net/)** and generates one pre-assembly and one post-assembly report at the end of the analysis.

Manual: [https://www.gitbook.com/book/luke831215/squat](https://www.gitbook.com/book/luke831215/squat)

<br>

## Getting started

### Github installation

	git clone https://github.com/luke831215/squat
	cd SQUAT; make install

### Dependency
- Python3
- Matplotlib
- Numpy
- Beautiful Soup

### Example data

For trial purposes, we extract 25000 reads from the specie **Saccharomyces cerevisiae** and map them to the assembly. Run the following command to start. See [Usage](https://luke831215.gitbooks.io/squat/content/usage.html) and [Output](https://luke831215.gitbooks.io/squat/content/output.html) for more details.

	./squat.sh example/SEQ.fastq -o example -r example/ASSEMBLY.fasta

After finishing, open `SEQ.html` in example directory to begin.

<br>

## Usage

### For impatient users,

	./squat.sh seq1 seq2 ... seqN
			 -o <output_dir>  
			 -r <genome_assembly> 

Please specify the path of the sequencing reads and the assembly to which they are mapped.

For paired-end reads, it is recommended to combine them into a single file. Otherwise, SQUAT also supports the input of multiple sequence files and generates multiple quality assessment reports in the same output directory.

### Primary output
`[output_dir]/[seq.html]`

SQUAT will generate an HTML index and a directory containing all the analysis information, both termed the same name as the sequencing reads file.

`[output_dir]/[seq.html]`

The table of content to link to other reports. (Index page)

`[output_dir]/[seq]/[pre-assembly_report.html]`

A pre-assembly report based on quality scores

`[output_dir]/[seq]/[post-assembly_report.html]`

A post-assembly report based on read mapping

For details of the output directory structure, see [output section](https://luke831215.gitbooks.io/squat/content/output.html).

<br>

## Command Options

SQUAT runs from the command line with the following options:  

**-h (or --help)**
> Display the complete command options on screen.

**-o < path >**
> The path to output directory.

**-r < str >**
>Path to the assembly file as reference for alignment. SQUAT accepts FASTA format.

**-g < path >**
>Assembly file. The tool accepts assemblies or reference genomes in FASTA format. (Remove contigs with all Ns before use)

**-t < int > (or --thread < int >)**
>Number of threads to use. The default value is 1/3 of the number of CPUs of the current machine.

**-k (or --keep)**
>Keep the sam file after each mapping experiment in `{output_dir}/{seq}/{aligner}`.

**-s < str >**
>Return the subset of sequencing reads with labels specified in capitals. For ex., **-s PSC** means only selecting reads labeled with P, S, and C). The subset of sequencing reads will be stored in `{output_dir}/{seq}/subset`.
    
**-g < str >**
> Path to the reference genome file for GAGE benchmark tool.

**--gage**
>Activate gage mode for assembly evaluation, must specify reference genome (-g).

**-c < float >**
> Threshold for overall sequencing quality. Sequencing datasets whose percentage of poor quality reads exceeding the threshold will be determined poor quality and fail the assessment, default 0.2.

**--mt < float > (or --mismatch_thre < float >)**
> Threshold for reads with substitution errors. Reads whose mismatch ratio exceeds the threshold will be determined poor quality, default 0.2.

**--ct < float > (or --clip_thre < float >)**
> Threshold for reads containing clips. Reads whose clip ratio exceeds the threshold will be determined poor quality, default 0.3.

**--ot < float > (or --others_thre < float >)**
> Threshold for reads with other errors. Reads whose error percentage exceeds the threshold will be determined poor quality, default 0.1

**--nt < float > (or --n_thre < float >)**
> Threshold for reads containing N. Reads whose N ratio exceeds the threshold will be determined  poor quality, default 0.1.

**--seed < int >**
> The seed for random sampling, default 0.	

For a complete list of command options, please check out our [manual](https://www.gitbook.com/book/luke831215/squat)


