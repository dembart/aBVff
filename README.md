BVlain is the module for bond valence site energy calculations and for the bond valence energy landscape construction. The program is based on the theory developed by S. Adams and co-authors:<br>  <br>  
(1) H. Chen, L.L. Wong, S.Adams; SoftBV - a software tool for screening the materials genome of inorganic fast ion conductors. Acta Crystallogr. B 75 (2019), 18-33. https://doi.org/10.1107/S2052520618015718 (as the source of the code) <br>  <br>  
(2) H. Chen, S. Adams; Bond softness sensitive bond-valence parameters for crystal structure plausibility tests. IUCrJ 4 (2017) 614-625. https://doi.org/10.1107/S2052520618015718 (as the source of the BV parameters)<br>  <br>  
(3) L.L. Wong, K.C. Phuah, R. Dai, H. Chen, W.S. Chew, S. Adams; Bond Valence Pathway Analyzer - An Automatic Rapid Screening Tool for Fast Ion Conductors within softBV. Chemistry of Materials 33 (2021) 625 - 641. https://doi.org/10.1021/acs.chemmater.0c03893 for the pathway analyser algorithm and the user interface.<br>  <br>  


## Installation
* Write the following comand to the command line:

```Python
pip install BVlain
``` 

<br>    
That's it.<br><br>

### Note!

* If you've got an error related to the C++ ("error: Microsoft Visual C++ 14.0 is required. Get it with "Build Tools for Visual Studio": https://visualstudio.microsoft.com/downloads/") and if your system is Windows. Then:<br><br>

* Go to the link: https://visualstudio.microsoft.com/visual-cpp-build-tools/


* Press "Download Build Tolls" button


* Run the downloaded .exe file and install Build Tools. Open it and check the mark related to the C++. Install C++ with the default package selection (~6 Gb)


![](https://github.com/dembart/BVLain/raw/01db73bf551630175b847f2cde7fe5549e49cf27/BuildToolsInstallation.png)


* Reboot your PC


* After all, run: ```pip install --upgrade setuptools``` <br>


## Usage

* Import the module executing the command:
```Python
from BVlain.BVlain import *
```

* You need to read a structure:<br>
<blockquote> Hope you have a CIF you want to study</blockquote>

* Copy the pathway to your CIF<br><br>

* Asign it to some variable

```Python
cif = "/Users/artemdembitskiy/Desktop/BV/cifs/NVP_siman.cif"
```
<blockquote> Oxidation states should be assigned in the CIF</blockquote>

* Read the structure with the following command:

```Python
st = structure_read(cif)
```
* Now we are ready for the migration barrier calculation, but first, several words about the function used for this:


<blockquote>

* There are a lot of input parameters for the calculation (the full list is at the bottom)


* But for inexperienced user the only two are required, while the others are set by default 


* These two are your structure and the mobile ion which migration barrier you want to estimate</blockquote>


* Calculate the barrier with the following command:


```Python
barrier(struct = st, mobile_ion = "Na+")
```
<blockquote> The output is migration barriers along three main directions, the lowest barrier among them, and the time spent on calculation</blockquote>


* The full list of input parameters for ```barrier``` function:<br>
<blockquote> If a default value is not mentioned then this value is None </blockquote>


* name - name of your system or whatever you want. "Lain" is by default.


* struct - the structure you want to study (see paragraph 2).


* mobile_ion - the ion for which barriers will be calaculated.


* r_cut - a radius within which the neighbours of the mobile ion will be treated. It is a float. 8 is by default.


* f_sc - the screening factor. If you don't know what it is don't touch it. 0.74 is by default. 


* resolution - a mesh grid resolution (in angstroms). 0.25 is by default. You can face RAM related crashing if resolution is lower than 0.15.


* E_step - the precision of the migration barrier calculation (in eV). 0.1 is by default.


* E_cut - the maximum energy above which the barrier will be set to infinity and the exact value will not be calculated. 5 is by default. 


* species_to_remove - a list of species you wish to remove before the calculation. Example: ["N3-","H1+"]


* vesta - None by default. If = 1 then the volumetric data (BVSE field) will be written in a VESTA 3.0 readable format.
<blockquote> path_to_output should be determined </blockquote>


* report - None by default. If = 1 then the report in .txt will be written
<blockquote> path_to_output should be determined </blockquote>


* path_to_cif - the pathway to your structure. That is for those who whants to read the structure implicitly.



* path_to_output - path to the output (report and volumetric data)


## Example

```Python
from BVlain.BVlain import *
cif = "/Users/artemdembitskiy/work/BV/cifs/NVP_siman.cif"
output = "/Users/artemdembitskiy/work/BV/output"
st = structure_read(cif)
Ea = barrier(name = "NaVPO4F", struct = st, mobile_ion = "Na+",
             vesta = 1, report = 1, path_to_output = output)
```


