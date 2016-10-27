# EPP622-Project

#Getting the Arabidopsis protein database and unzip
~~~
[Newton:sigma00 input]$ wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/001/735/GCF_000001735.3_TAIR10/GCF_000001735.3_TAIR10_protein.faa.gz
--2016-10-27 13:56:50--  ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/001/735/GCF_000001735.3_TAIR10/GCF_000001735.3_TAIR10_protein.faa.gz
           => “GCF_000001735.3_TAIR10_protein.faa.gz”
Resolving ftp.ncbi.nlm.nih.gov... 130.14.250.10, 2607:f220:41e:250::12
Connecting to ftp.ncbi.nlm.nih.gov|130.14.250.10|:21... connected.
Logging in as anonymous ... Logged in!
==> SYST ... done.    ==> PWD ... done.
==> TYPE I ... done.  ==> CWD (1) /genomes/all/GCF/000/001/735/GCF_000001735.3_TAIR10 ... done.
==> SIZE GCF_000001735.3_TAIR10_protein.faa.gz ... 11867691
==> PASV ... done.    ==> RETR GCF_000001735.3_TAIR10_protein.faa.gz ... done.
Length: 11867691 (11M) (unauthoritative)

100%[======================================>] 11,867,691  12.7M/s   in 0.9s    

2016-10-27 13:56:51 (12.7 MB/s) - “GCF_000001735.3_TAIR10_protein.faa.gz” saved [11867691]

[Newton:sigma00 input]$ ls
GCF_000001735.3_TAIR10_protein.faa.gz  peptides
[Newton:sigma00 input]$ gunzip GCF_000001735.3_TAIR10_protein.faa.gz 
[Newton:sigma00 input]$ ls
GCF_000001735.3_TAIR10_protein.faa  peptides
~~~

#Raw files from mass spec were put into MaxQuant, MaxQuant can not be run on the command line, so I have taken the perameters and coppied here:
~~~
Parameter	Value
Version	1.5.5.1
User name	robertslab
Machine name	DROBERTS7010
Date of writing	10/14/2016 14:53:23
Fixed modifications	Carbamidomethyl (C)
Include contaminants	True
PSM FDR	0.01
Protein FDR	0.01
Site FDR	0.01
Use Normalized Ratios For Occupancy	True
Min. peptide Length	7
Min. score for unmodified peptides	0
Min. score for modified peptides	40
Min. delta score for unmodified peptides	0
Min. delta score for modified peptides	6
Min. unique peptides	0
Min. razor peptides	1
Min. peptides	1
Use only unmodified peptides and	True
Modifications included in protein quantification	Oxidation (M);Acetyl (Protein N-term)
Peptides used for protein quantification	Razor
Discard unmodified counterpart peptides	True
Min. ratio count	2
Use delta score	False
iBAQ	False
iBAQ log fit	False
Match between runs	False
Find dependent peptides	False
Fasta file	C:\Users\Robertslab\Desktop\Sterling\Mass Spec\Arabidopsis_thaliana.TAIR10.pep.all.fa
Decoy mode	revert
Include contaminants	True
Advanced ratios	True
Fixed andromeda index folder	
Temporary folder	
Combined folder location	
Second peptides	True
Stabilize large LFQ ratios	True
Separate LFQ in parameter groups	False
Require MS/MS for LFQ comparisons	True
Calculate peak properties	False
Main search max. combinations	200
Advanced site intensities	True
Write msScans table	True
Write msmsScans table	True
Write ms3Scans table	True
Write allPeptides table	True
Write mzRange table	True
Top x mass window [Da]	100
Max. peptide mass [Da]	12000
Min. peptide length for unspecific search	8
Max. peptide length for unspecific search	25
Razor protein FDR	True
Disable MD5	False
Max mods in site table	3
Match unidentified features	False
MS/MS tol. (FTMS)	20 ppm
Top MS/MS peaks per 100 Da. (FTMS)	12
MS/MS deisotoping (FTMS)	True
MS/MS deisotoping tolerance (FTMS)	7
MS/MS deisotoping tolerance unit (FTMS)	ppm
MS/MS higher charges (FTMS)	True
MS/MS water loss (FTMS)	True
MS/MS ammonia loss (FTMS)	True
MS/MS dependent losses (FTMS)	True
MS/MS recalibration (FTMS)	False
MS/MS tol. (ITMS)	0.5 Da
Top MS/MS peaks per 100 Da. (ITMS)	8
MS/MS deisotoping (ITMS)	False
MS/MS deisotoping tolerance (ITMS)	0.15
MS/MS deisotoping tolerance unit (ITMS)	Da
MS/MS higher charges (ITMS)	True
MS/MS water loss (ITMS)	True
MS/MS ammonia loss (ITMS)	True
MS/MS dependent losses (ITMS)	True
MS/MS recalibration (ITMS)	False
MS/MS tol. (TOF)	40 ppm
Top MS/MS peaks per 100 Da. (TOF)	10
MS/MS deisotoping (TOF)	True
MS/MS deisotoping tolerance (TOF)	0.01
MS/MS deisotoping tolerance unit (TOF)	Da
MS/MS higher charges (TOF)	True
MS/MS water loss (TOF)	True
MS/MS ammonia loss (TOF)	True
MS/MS dependent losses (TOF)	True
MS/MS recalibration (TOF)	False
MS/MS tol. (Unknown)	0.5 Da
Top MS/MS peaks per 100 Da. (Unknown)	8
MS/MS deisotoping (Unknown)	False
MS/MS deisotoping tolerance (Unknown)	0.15
MS/MS deisotoping tolerance unit (Unknown)	Da
MS/MS higher charges (Unknown)	True
MS/MS water loss (Unknown)	True
MS/MS ammonia loss (Unknown)	True
MS/MS dependent losses (Unknown)	True
MS/MS recalibration (Unknown)	False
Site tables	Oxidation (M)Sites.txt
~~~
#Several .txt files came out, including peptides.txt and a proteins.txt (MaxQuant aligns peptides with the proteome)
#I will use the MaxQuant alignment as a control, and try to align the peptide.txt with the arabidopsis proteome using blast. 

~~~
[Newton:sigma00 input]$ module switch intel-compilers/2016u3
[Newton:sigma00 input]$ module load blast/2.4.0
[Newton:sigma00 input]$ mkdir 1_blast
[Newton:sigma00 input]$ head peptides 
AAQEALYVR	
AGKEENVKAAQEALYV
AQEALYVRCKANSEATAFNKQSGCMDENVSCEKWAK	
IHVKSFERAFNKQSGC	
VSCEKWAKAGECQKNPALEESNYELEGK	
ASYMDKVRALEESNYE	
SNYELEGKIKEWYEKHDLDQVAGR	
KITSSGQRDLDQVAGR	
DLDQVAGRIAAAVIG 
INGFGR
