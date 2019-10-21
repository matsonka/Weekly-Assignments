wget https://github.com/stechtmann/BL4300-5300/raw/master/data/Weekly_Assignment_data/Unk_therm.faa


make a blastable database for the protein sequence
makeblastdb -in Unk_therm.faa -dbtype prot -title Unk_therm


download the hsp.fasta
wget https://github.com/stechtmann/BL4300-5300/raw/master/data/Weekly_Assignment_data/HSP_prot.fasta


Query the blastable database with hsp.fasta

blastp -db Unk_therm.faa -query HSP_prot.fasta -out HSP_BLAST.txt -outfmt 7


Use winSCP to look at the HSP_BLAST.txt file to answer the questions

How many HSPs were found in the unknown organism?
There were 71 HSPs found in the unknown organism (there were 71 hits found in the 6 queries)

The E-value is a statistical measure to say what is the probability that I found this match by chance. If these numbers are very low then it means that there is a very low probability of us finding this by chance so it’s most likely a true match. So the lower the score the better


Based on the E-Values there are 10 potential HSPs in the unknown organism. Here are the 10 HSPs that were found in the unknown organism based on the e-values:
WP_103686269.1	Unk_1985	31.707	123	73	2	45	167	22	133	6.01e-17	70.1
WP_103686269.1	Unk_1863	34.066	91	56	1	79	169	31	117	2.11e-14	62.8
WP_103686269.1	Unk_1860	30.833	120	72	4	49	167	8	117	2.20e-14	62.8
WP_103686269.1	Unk_1117	25.773	97	64	2	73	169	33	121	1.91e-08	47.0
NP_418567.1	Unk_30	61.639	537	202	3	3	536	2	537	0.0	632
AJL35296.1	Unk_31	58.696	92	38	0	4	95	9	100	5.52e-34	109
AAA18300.1	Unk_1842	42.218	559	298	4	21	556	12	568	1.57e-139	416
AAA18300.1	Unk_301	27.723	101	67	2	152	252	100	194	7.26e-05	41.2
AAA18300.1	Unk_1187	26.946	167	106	6	175	338	172	325	1.30e-04	40.4
AEG34553.1	Unk_1970	32.800	625	285	17	557	1101	27	596	1.76e-54	201




There is no hard cut off to say this is what is a paralog so argue that you made the right choice, just give a logical argument use the twilight zone
e value first if its significant then look at bit score and %identity and if you have something that will fit within the twilight zone  or the safe zone


How many HSP have paralogs?


Provide a justification for the presence of paralogs.


