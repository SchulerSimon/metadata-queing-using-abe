# metadata-query-using-abe

#### this is a proof of concept, it is not designed to be used in production or enterprise context 
- this project requires charm-crypto (a python wrapper for stanford pbc elliptic curve cryptography)
	- see http://pages.cs.wisc.edu/~ace/install-charm.html

### idea:
The idea of this project was to create a cryptographically secure and privacy preserving matching of stakeholders in a medial context. 

Lets say that we have a number of patients that have a number of metrics assigned to them:
- their ethnic origin 
- their age
- a condition/disease

Lets also say that there are researchers that would like to get participants for medical studies. The participants should be: 
- from asia or europe
- between 18 and 35
- should have autism or cancer 

It is obvious why having a central and easily decryptable database of patients, with their respective information, is a bad idea. 

With the encrypthion-scheme provided in this example, matching of patiens and researchers happens completely encrypted. The matching of patients and researchers dose not reveal any more information than needed to fulfill the query. Researchers know that the patients given back are within their parameters, but they know no more.  

This is possible with the usage of [Attribute-Based-Encryption](https://en.wikipedia.org/wiki/Attribute-based_encryption). 


Have a look at `[~repo]/prototype/actors/patient.py` to get a feel for how patients are created
```python
Patient(asian, 22, autism)
```

Have a look at `[~repo]/prototype/actors/query.py` to get a feel for how queries work
```python
Queue(
	"(asian or european or north_american) and (22 to 100) and (cancer or autism)"
)
```

Originally this was designed with Blockchain in mind, so that matching happens in a decentralized way. 
The class Smartcontract (`[~repo]/prototype/actors/smartcontract.py`) is a dummy implementation of a smartcontract that is able to do the matching completely encrypted. This could be implemented in Solidity (for the Ethereum Blockchain).

#### contents:
- ```[~repo]/prototype/``` contains a prototype to query bit wise encoded metadata from nodes (or people) in a privacy preserving matter
- ```[~repo]/tests/``` contains tests for encoding- and decoding-speed of different ABE-Schemes
- ```[~repo]/string_encryption/``` contains a prototype for encoding strings with ECC (Elliptic Curve Cryptography). This could be very handy once the prototype is used in a more complex manner

#### requirements:
- python3
- charm-crypto

### installation:
- install python3
	- https://www.python.org/downloads/
- install charm-crypto
	 -  http://pages.cs.wisc.edu/~ace/install-charm.html

#### run the prototype:
```bash
cd [~repo]/prototype/
python3 pyrototype.py
```

*the prototype is implemented with CPabe09. Because FAME has better performance the prototype should be updated to use FAME*


#### run string encoding with EEC
```bash
cd [~repo]/string_encoding/
python3 concept.py
```


#### run the tests:
for testing CPabe09 (slightly modified version to fit needs)
(https://jhuisi.github.io/charm/charm/schemes/abenc/abenc_waters09.html#module-abenc_waters09)


```bash
cd [~repo]/speed_tests/cp_abe/
python3 test.py
```

for testing FAME
(https://jhuisi.github.io/charm/charm/schemes/abenc/ac17.html#ac17.AC17CPABE)


```bash
cd [~repo]/speed_tests/fame_abe/
python3 test.py
```


##### notes:
If you have any questions, you are welcome to write me: schuler.simon@gmx.net
