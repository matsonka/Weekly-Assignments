efetch -db=nucleotide -id=CP000141.1 -format=fastq>C.hydro_6008.fastq



gdown.pl https://drive.google.com/file/d/1PWWO5wVRRThLBXXEZjyWZHIb9udVcnCS/edit C.ferri_R1.fastq
gdown.pl https://drive.google.com/file/d/1mZFvpSIctuBihkOlQX9vhrkxng3cRmvK/edit C.ferri_R2.fastq


fastqc C.ferri_R1.fastq
fastqc C.ferri_R2.fastq
cutadapt -q 20,20 -a CTGTCTCTTATACACATCTCCGAGCCCACGAGAC -A CTGTCTCTTATACACATCTGACGCTGCCGACGA -m 50 --max-n 0 -o C.ferri_R1.cutadapt.fastq -p C.ferri_R2.cutadapt.fastq C.ferri_R1.fastq C.ferri_R2.fastq
bowtie2-build C.hydrogenoformans_Z2901.fasta C.hydro
bowtie2 -x C.ferri -1 C.ferri_R1.cutadapt.fastq -2 C.ferri_R2.cutadapt.fastq -S 6008C.ferri.sam


