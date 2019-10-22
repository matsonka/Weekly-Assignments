wget https://github.com/stechtmann/BL4300-5300/raw/master/data/Weekly_Assignment_data/Unk_therm.faa


make a blastable database for the protein sequence
makeblastdb -in Unk_therm.faa -dbtype prot -title Unk_therm


download the hsp.fasta
wget https://github.com/stechtmann/BL4300-5300/raw/master/data/Weekly_Assignment_data/HSP_prot.fasta


Query the blastable database with hsp.fasta

blastp -db Unk_therm.faa -query HSP_prot.fasta -out HSP_BLAST.txt -outfmt 7


Use winSCP to look at the HSP_BLAST.txt file to answer the questions

How many HSPs were found in the unknown organism?
Just by looking at the data in the txt file it seems that there were 71 HSPs found in the unknown organism (there were 71 hits found in the 6 queries)


However, first we want to look at all of these hits and check their e-values to see what is a significant hit and a homolog (we want to cut out hits that are not significant). The E-value is a statistical measure to say what is the probability that I found this match by chance. If these numbers are very low then it means that there is a very low probability of us finding this by chance so it’s most likely a true match. So the lower the score the better


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


Next we should look further into these 10 hits that we concluded were good homologs from looking at the e-values to look at the percent identity and the length of the alignment to determine if any of these hits are homologs. The percent identity is a function of sequence length, and the longer the sequence is the less identity might be acceptable to put it into this family. We can look at the graph from twilight zone of protein homology which gives us a rule of thumb for interpreting the percent identity in getting something into a protein family. We want to try to get the percent identity and length of the alignment to be in the safe zone because they will be the most acceptable and could be within the same family. However, if the percent identity and the length of the alignment ends up in the twilight zone the it could or could not be apart of the same family. Here was my interpretations:

WP_103686269.1	Unk_1985	31.707	123	73	2	45	167	22	133	6.01e-17	70.1  In the safe zone (% identity is 31.707 and alignmnet length is 123)

WP_103686269.1	Unk_1863	34.066	91	56	1	79	169	31	117	2.11e-14	62.8  In the safe zone

WP_103686269.1	Unk_1860	30.833	120	72	4	49	167	8	117	2.20e-14	62.8  In the safe zone

WP_103686269.1	Unk_1117	25.773	97	64	2	73	169	33	121	1.91e-08	47.0  In the twilight zone

NP_418567.1	Unk_30	61.639	537	202	3	3	536	2	537	0.0	632  In the safe zone

AJL35296.1	Unk_31	58.696	92	38	0	4	95	9	100	5.52e-34	109  In the safe zone

AAA18300.1	Unk_1842	42.218	559	298	4	21	556	12	568	1.57e-139	416  In the safe zone

AAA18300.1	Unk_301	27.723	101	67	2	152	252	100	194	7.26e-05	41.2  In the twilight zone

AAA18300.1	Unk_1187	26.946	167	106	6	175	338	172	325	1.30e-04	40.4  In the twilight zone

AEG34553.1	Unk_1970	32.800	625	285	17	557	1101	27	596	1.76e-54	201  In the safe zone

Based on these interpretations we can get rid of all of the hits that were in the twilight zone because these could be or could not be potential HSPs and we want to interpret our data as best as we can. So we will be left with only the unknowns that fell into the safe zone. Based on the percent identity and alignment length there are now 7 potential HSP homologs in the unknown organism that are listed below:

WP_103686269.1	Unk_1985	31.707	123	73	2	45	167	22	133	6.01e-17	70.1  In the safe zone

WP_103686269.1	Unk_1863	34.066	91	56	1	79	169	31	117	2.11e-14	62.8  In the safe zone

WP_103686269.1	Unk_1860	30.833	120	72	4	49	167	8	117	2.20e-14	62.8  In the safe zone

NP_418567.1	Unk_30	61.639	537	202	3	3	536	2	537	0.0	632  In the safe zone

AJL35296.1	Unk_31	58.696	92	38	0	4	95	9	100	5.52e-34	109  In the safe zone

AAA18300.1	Unk_1842	42.218	559	298	4	21	556	12	568	1.57e-139	416  In the safe zone

AEG34553.1	Unk_1970	32.800	625	285	17	557	1101	27	596	1.76e-54	201  In the safe zone


Finally we can check the bit score to determine if something is significant and a homolog. To do the bit score it's just a score of the alignments so the significant alignments have higher the bit scores. The better the alignment, the higher the bit score. So we can look at the narrowed down 7 potential HSP homologs to see the bit scores:


WP_103686269.1	Unk_1985	31.707	123	73	2	45	167	22	133	6.01e-17	70.1    bit score 70.1

WP_103686269.1	Unk_1863	34.066	91	56	1	79	169	31	117	2.11e-14	62.8    bit score 62.8

WP_103686269.1	Unk_1860	30.833	120	72	4	49	167	8	117	2.20e-14	62.8      bit score 62.8

NP_418567.1	Unk_30	61.639	537	202	3	3	536	2	537	0.0	632                     bit score 632

AJL35296.1	Unk_31	58.696	92	38	0	4	95	9	100	5.52e-34	109               bit score 109

AAA18300.1	Unk_1842	42.218	559	298	4	21	556	12	568	1.57e-139	416         bit score 416

AEG34553.1	Unk_1970	32.800	625	285	17	557	1101	27	596	1.76e-54	201     bit score 201


In looking at the bit scores, 4 of the HSPs are above 100. 3 of these HSPs have e-values that are much smaller thann the 3 e-values of the HSPs that have bit scores less than 100. Again, if the e-values are very low then it means that there is a very low probability of us finding this by chance so it’s most likely a true match. So because the 3 HSPs with the smaller bit scores also don't have as low of e-values as the other HSPs we can conclude that they are not significant and homologs. There is 1 HSP that has an e-value of 0.0 which is a good e-value but it has the highest bit score of 632, making it's alignment the most significant. From this these HSPs are homologs  and paralogs to the unknown organism:

NP_418567.1	Unk_30

AJL35296.1	Unk_31

AAA18300.1	Unk_1842

AEG34553.1	Unk_197)

How many HSP have paralogs?
In looking at the bit scores and the e-values of the HSPs, there are 4 HSPs that have paralogs (see the above justifications as to why these 4 are the most significant paralogs)
