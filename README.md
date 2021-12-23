# Modelling the dynamic range of second-generation toehold switches

Three open-source tools were developed for machine-learning based design of RNA devices, namely toehold switches. They have been developed for second-generation toehold switch designs, but could be adapted for first-generation toehold switches. 

(1) GrammarParser.py:

Used to return the domain structure of a toehold switch, i.e, parsing the sequence into its structural segments based on the grammar of dot-bracket representations. The dot-bracket representation could be obtained by `ViennaRNNA`'s RNAfold.
 - `Input`: Toehold switch sequence (`toehold_seq`) & predicted dot-bracket representation (`dot-bracket_rep`)
 - `Output`: Parsed domain sequences 
 -  Usage: `python GrammarParser toehold_seq dot-bracket_rep`

(2) predict.py:

Used to predict the efficacy (i.e, dynamic range) of a new toehold switch. Takes the non-redundant engineered feature values in order as arguments, and returns the dynamic range of the construct: 
 - `Input` (six `Features` in order): `Overall Switch MFE` `Bottom Region MFE` `RBS Linker MFE` `Net MFE` `Frequency of MFE structure` `Specific Heat at 37 deg C`
 - `Output`: Dynamic range of the given toehold switch construct
 -  Usage: `python predict.py InputFeatures`

  
(3) toehold_efficacy_predict.sh:
 
    An integrated script written in bash that provides an end-to-end pipeline for the prediction of toehold efficacy for second-generation toehold switches.  

    The script does the following:
 
    (i) calls ViennaRNA RNAfold to parse the input sequence into its dot-bracket representation
 
    (ii) calls GrammarParser to then extract the segments of the toehold switch based on this dot-bracket representation
 
    (iii) calls more ViennaRNA RNAfold utilities to obtain engineered feature values for the given toehold switch sequence
 
    (iv) passes these feature values as input to 'predict.py` and returns the dynamic range of the toehold switch sequence. 
 
 - `Input`: Toehold switch sequence(s) in .fasta or .txt format.
 - `Output`: Predicted dynamic range(s) of given toehold switch sequence(s), and engineered feature values.
 - Usage: `sh ./toehold_efficacy_predict.sh Input_Seq_File`
 
### Requirements:
 
(1) [`ViennaRNA`](https://www.tbi.univie.ac.at/RNA/) must be installed and available in the path. 
 
(2) Python 3.0 or above
 
(3) bash shell
 

## Data

The **data** folder consists of the engineered features for the 228 toehold instances from the literature [1,2,3]: 

(1) *all_features.csv* : consisting of all the engineered sequence and structural features

(2) *selected_features.csv* : consisting features with the best predictive capabilities, post feature-selection (see our manuscript for details).

## Citation 

Our software is made freely available for the scientific community under GNU GPL v3. To cite:
 
PRS Baabu, S Srinivasan, S Nagarajan, S Muthamilselvan, RR Suresh, T Selvi & A Palaniappan. [End-to-end computational approach to the design of RNA biosensors for miRNA biomarkers of cervical cancer](https://doi.org/10.1101/2021.07.09.451282). (2021) 

### Primary sources for building our dataset:
1. Green AA, Silver PA, Collins JJ, Yin P. Toehold switches: De-novo-designed regulators of gene expression. Cell 2014. https://doi.org/10.1016/j.cell.2014.10.002. 
2.  Pardee K, Green AA, Takahashi MK, Braff D, Lambert G, Lee JW, et al. Rapid, LowCost Detection of Zika Virus Using Programmable Biomolecular Components. Cell
2016;165:1255–66. https://doi.org/10.1016/j.cell.2016.04.059.
3. Green AA, Kim J, Ma D, Silver PA, Collins JJ, Yin P. Complex cellular logic computation using ribocomputing devices. Nature 2017. https://doi.org/10.1038/nature23271.
