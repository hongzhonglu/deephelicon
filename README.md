# DeepHelicon
![](https://img.shields.io/badge/DeepHelicon-executable-519dd9.svg)
![](https://img.shields.io/badge/last_released_date-Feb_2020-green.svg)

###### tags: `transmembrane protein` `v0.1`

## Overview
DeepHelicon is a predictor for precisely predicting inter-helical residue contacts in transmembrane proteins. This repository is a standalone package of DeepHelicon. Apart from the package, we will consider a [webserver](https://) for DeepHelicon to develop.

## System Requirement
    
The software is only allowed to be run on a Linux operation system. Please be sure of python (version>3.5) installed before using. We highly recommend a package [Anaconda](https://www.anaconda.com/distribution/), an integrated development environment of python, which eases the use and management of python packages.

## Installation
    
1. **install the dependencies and specify where their executables are**.
    * [HHblits](https://github.com/soedinglab/hh-suite) - generating multiple sequence alignments
    * [CCMpred](https://github.com/soedinglab/CCMpred) - predictor of residue contacts
    * [Gaussian DCA](https://github.com/carlobaldassi/GaussDCA.jl) - predictor of residue contacts
    * [Freecontact](https://rostlab.org/owiki/index.php/FreeContact) - predictor of residue contacts
    * [plmDCA](https://github.com/debbiemarkslab/plmc) - predictor of residue contacts
    * [TMHMM](http://www.cbs.dtu.dk/cgi-bin/nph-sw_request?tmhmm) - predictor of transmembrane segments
    * [EVcouplings](https://github.com/debbiemarkslab/EVcouplings) - python interface used for predicting protein structure, function and mutations using evolutionary sequence covariation
    * [Uniprot database](http://wwwuser.gwdg.de/~compbiol/data/hhsuite/databases/hhsuite_dbs/old-releases/) - a curated protein sequence database for hhblits
    
    > **_NOTE_**
    
    1. Download either the recommended Uniprot database, or other database curated for HHblits and make it work with hhblits.
    2. Download and specify the path of EVcouplings package in src/Plmc_dhc_rs.py. Please do not rename this package.
    3. Please add the paths of the above executable programs to `src/troll.sh`.


2. **install DeepHelicon**

    To obtain the latest version of DeepHelicon, do
    ```
    git clone https://github.com/2003100127/deeptmcon.git
    ```

3. **install python dependencies**
    
    ```    
	pip install -r requirements.txt
	```

## Usage

1. **`src/troll.sh`**

    * description
        troll.sh is used to generate transmembrane topologies and most of evolutionary coupling features, including CCMpred, EVfold, plmDCA.

    * shell commands
        * general
        ```
        ./troll.sh -n NAME -c CHAIN -i /INPUT/PATH/
        ```
        * example
        ```
        ./troll.sh -n 2wsc -c 2 -i ./input/
        ```
    * description
	    * required
        ```
        -n --name -> a sequence name.
        -c --chain -> a chain name
        -i --input -> input path
        ```

2. **`src/gdca.julia`**
    
    * description
        gdca.julia is used to generate Gaussian DCA file. You'd better run it cf. https://github.com/carlobaldassi/GaussDCA.jl.
        
3. **`run_deephelicon.py`**
    
    * description
        If you have the feature files shown in the `input/` directory, you can skip over steps 1-2 to step 3. We tested this step in a rigorous way. Be sure of every feature file already in the `input/` or your preferred input file path. Before start, an available `EVcouplings` tool must be configured with our program properly. Finally, it works easily like this. 
    
	* python commands
	    * general
	    ```
        python run_deephelicon.py -n NAME -c CHAIN -i /YOUR/input/PATH/ -o /YOUR/OUTPUT/PATH/
        ```
	    * example
        ```
        python run_deephelicon.py -n 2wsc -c 2 -i ./input/ -o ./output/
        ```
	* description
	    * required
        ```
        -n --name -> a sequence name.
        -c --chain -> a chain name
        -i --input -> input path
        -o --output --> prediction results
        ```

2. description of output file
	* format
	  This predictor returns predictions of inter-helical residue contacts in tansmembrane proteins. If non-transmembrane segment or <1 transmembrane segment is detected, the programe will not return final results. However, you can still utilize the intermediate results at stage 1 and 2 as stated in the paper. Considering <1 helix detection by inside transmembrane topology predictor, we will consider extending our module to generate a file including entire results in the future work.
    * example
	  
      ```mermaid
        graph LR
        A[position1] -->B[amino acid 1]
            B --> C[position2]
            C --> D[amino acid 2]
        ```
      
      ```
          1          Y         6	     F  	 0.08136672
          |          |         |         |            |
          |          |         |         |            |
      position1      |     position2     |       prediction score   
              amino acid 1         amino acid 2           
      ```

## How to cite
J. Sun. D. Frishman. DeepHelicon: xxxxxxxxxxx.

## Contact
If you have any problem in using it, please feel free to contact
> jianfeng.sunmt{[({at})]}gmail.com
> jianfeng.sun{[({at})]}tum.