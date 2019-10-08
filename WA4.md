fastqc C.ferri_R1.fastq
fastqc C.ferri_R2.fastq
cutadapt -q 20,20 -a CTGTCTCTTATACACATCTCCGAGCCCACGAGAC -A CTGTCTCTTATACACATCTGACGCTGCCGACGA -m 50 --max-n 0 -o C.ferri_R1.cutadapt.fastq -p C.ferri_R2.cutadapt.fastq C.ferri_R1.fastq C.ferri_R2.fastq
bowtie2 -x C.ferri -1 C.ferri_R1.fastq -2 C.ferri_R2.fastq -S 6008.sam
