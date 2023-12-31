# Gene2Tab

## Description

This script is used to convert the output of [ABRICATE](https://github.com/tseemann/abricate) tabulated output into a matrix samples with the genes as columns and the presence/absence of the gene as the values.

The script can use as input a directory containing multiple `.tab` files or a single `.tab` file. The output will be a `.csv` file. Each file should contain the `#File` `Sequence` and `GENE` columns, the other ones are optional. 

By default, **the script will only consider genes with a coverage and identity of 90% or more**. This can be changed with the `--min_coverage` and `--min_identity` flags.

Example: 
    
File1.tab
```tsv
#FILE	SEQUENCE	START	END	STRAND	GENE	COVERAGE	COVERAGE_MAP	GAPS	%COVERAGE	%IDENTITY	DATABASE	ACCESSION	PRODUCT	RESISTANCE
Isolate1	S1-length_513	53228	54445	+	ceoA	1-1218/1218	========/======	2/2	99.92	99.67	card	U97042:0-1218	ceoA is a periplasmic linker subunit of the CeoAB-OpcM efflux pump	aminoglycoside;fluoroquinolone
Isolate1	S1-length_513	54491	57575	+	ceoB	1-3084/3084	========/======	1/1	100	99.87	card	U97042:1263-4347	ceoB is a cytoplasmic membrane component of the CeoAB-OpcM efflux pump	aminoglycoside;fluoroquinolone
Isolate1	S1-length_513	57702	59240	+	opcM	1-1536/1536	========/======	5/5	99.93	99.16	card	U38944.1:0-1536	OpcM is an outer membrane factor protein found in Burkholderia cepacia. It is part of the CeoAB-OpcM complex.	aminoglycoside;fluoroquinolone
Isolate1	S1-length_233	145199	146378	+	amrA	24-1200/1200	========/======	15/23	97.25	80.84	card	BX571965.1:2152165-2150965	amrA is the efflux pump subunit of the AmrAB-OprM multidrug efflux complex. amrA corresponds to 1 locus in Pseudomonas aeruginosa PAO1 and 1 locus in Pseudomonas aeruginosa LESB58.	aminoglycoside
Isolate1	S1-length_233	146394	149503	+	amrB	1-3110/3132	========/======	2/2	99.27	88.17	card	BX571965.1:2150949-2147817	amrB is the membrane fusion protein of the AmrAB-OprM multidrug efflux complex.	aminoglycoside
Isolate1	S1-length_265	25329	26405	+	Burkholderia_pseudomallei_Omp38	1-1122/1122	========/======	14/59	95.37	80.78	card	AY312416:0-1122	Heterologous expression of Burkholderia pseudomallei Omp38 (BpsOmp38) in Omp-deficient E. coli host cells lowers their permeability and in consequence their antimicrobial susceptibility to penicillin G cefoxitin ceftazidime and imipenem.	carbapenem;cephalosporin;cephamycin;monobactam;penam;penem
Isolate2	S2-length_512	25329	26405	+	Burkholderia_pseudomallei_Omp38	1-1122/1122	========/======	14/59	95.37	80.78	card	AY312416:0-1122	Heterologous expression of Burkholderia pseudomallei Omp38 (BpsOmp38) in Omp-deficient E. coli host cells lowers their permeability and in consequence their antimicrobial susceptibility to penicillin G cefoxitin ceftazidime and imipenem.	carbapenem;cephalosporin;cephamycin;monobactam;penam;penem
```

File2.tab
```tsv
#FILE	SEQUENCE	START	END	STRAND	GENE	COVERAGE	COVERAGE_MAP	GAPS	%COVERAGE	%IDENTITY	DATABASE	ACCESSION	PRODUCT	RESISTANCE
Isolate2	S2-length_512	25329	26405	+	Burkholderia_pseudomallei_Omp38	1-1122/1122	========/======	14/59	95.37	80.78	card	AY312416:0-1122	Heterologous expression of Burkholderia pseudomallei Omp38 (BpsOmp38) in Omp-deficient E. coli host cells lowers their permeability and in consequence their antimicrobial susceptibility to penicillin G cefoxitin ceftazidime and imipenem.	carbapenem;cephalosporin;cephamycin;monobactam;penam;penem
```

Will be converted to:

```csv
Sample,ceoA,ceoB,opcM,amrA,amrB,Burkholderia_pseudomallei_Omp38
BUR-BAB-IMI-102146,1,1,1,1,1,1
AA2,0,0,0,0,0,1
```

If the `--transpose` flag is used, the output will be:

```csv
Sample,Isolate1,Isolate2
ceoA,1,0
ceoB,1,0
opcM,1,0
amrA,1,0
amrB,1,0
Burkholderia_pseudomallei_Omp38,1,1
```

## Installation

```bash
pip install gene2tab
```

## Usage

See all the available options with:

```bash
gene2tab -h
```

Running the script. The input can be a single `.tab` file or a directory containing multiple `.tab` files. The output will be a `.csv` file.

```bash
gene2tab -i [output_directory or file.tab] -o output.csv --min_coverage 0.9 --min_identity 0.9 
```

You can also transpose the output with the `--transpose` flag.

```bash
gene2tab -i [output_directory or file.tab] -o output.csv --min_coverage 0.9 --min_identity 0.9 --transpose
```

If your files use a different delimiter than tab, you can specify it with the `--input_file_delimiter` flag.

```bash
gene2tab -i [output_directory or file.tab] -o output.csv --min_coverage 0.9 --min_identity 0.9 --input_file_delimiter ','
```

If you want a different delimiter in the output file, you can specify it with the `--output_file_delimiter` flag.

```bash
gene2tab -i [output_directory or file.tab] -o output.csv --min_coverage 0.9 --min_identity 0.9 --output_delimiter ';'
```


## License

Apache License 2.0

