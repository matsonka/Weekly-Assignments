wget https://github.com/stechtmann/BL4300-5300/raw/master/data/Weekly_Assignment_data/Unk_therm.faa


make a blastable database for the protein sequence
makeblastdb -in Unk_therm.faa -dbtype prot -title Unk_therm


download the hsp.fasta
wget https://github.com/stechtmann/BL4300-5300/raw/master/data/Weekly_Assignment_data/HSP_prot.fasta


Query the blastable database with hsp.fasta

blastp -db Unk_therm.faa -query HSP_prot.fasta -out HSP_BLAST.txt -outfmt 7




How many HSPs were found in the unknown organism?
Provide your justification for how many HSPs were in the organism (use information in the BLAST ouput E-value, length, percent ID, etc).



How many HSP have paralogs?


Provide a justification for the presence of paralogs.


