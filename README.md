## PyFingerprint

![GitHub](https://img.shields.io/github/license/hcji/PyFingerprint)
![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/hcji/PyFingerprint?include_prereleases)
![GitHub repo size](https://img.shields.io/github/repo-size/hcji/PyFingerprint)


There are many types of chemical fingerprint for describing the molecule provided by different tools, such as RDKit, CDK and OpenBabel. This package aims to summarize them all.

### Dependencies

 1. [Anaconda for python 3.6 or later](https://www.anaconda.com/products/individual) 
 2. [Java SE Development Kit 11](https://www.oracle.com/java/technologies/java-se-development-kit11-downloads.html) 
 3. jpype
 
        pip install jpype1

 4. RDKit

        conda install -c rdkit rdkit
		
 5. OpenBabel
 
		conda install -c conda-forge/label/main openbabel
 
### Install

	pip install git+git://github.com/hcji/PyFingerprint@master

### Usage

    from PyFingerprint.fingerprint import get_fingerprint

    smi = 'CCCCN'
    cdktypes = ['standard', 'extended', 'graph', 'maccs', 'pubchem', 'estate', 'hybridization', 'lingo', 
                'klekota-roth', 'shortestpath', 'signature', 'substructure']
    rdktypes = ['rdkit', 'morgan', 'rdk-maccs', 'topological-torsion', 'avalon', 'atom-pair']
    babeltypes = ['fp2', 'fp3', 'fp4']

    output = {}
    for f in cdktypes:
        output[f] = get_fingerprint(smi, f)

    for f in rdktypes:
        output[f] = get_fingerprint(smi, f)
        
    for f in babeltypes:
        output[f] = get_fingerprint(smi, f)

    output_np = output.copy()
    for k, fp in output.items():
        output_np[k] = fp.to_numpy()
	
### Cite

[Predicting Molecular Fingerprint from Electron-Ionization Mass Spectrum with Deep Neural Networks](https://pubs.acs.org/doi/10.1021/acs.analchem.0c01450)

### Support fingerprint types:

	**standard**: Considers paths of a given length. These are hashed fingerprints, with a default length of 1024.
	**extended**: Similar to the standard type, but takes rings and atomic properties into account into account.
	**graph**: Similar to the standard type by simply considers connectivity.
	**hybridization**: Similar to the standard type, but only consider hybridization state.
	**estate**: 79 bit fingerprints corresponding to the E-State atom types described by Hall and Kier.
	**pubchem**: 881 bit fingerprints defined by PubChem.
	**klekota-roth**: 4860 bit fingerprint defined by Klekota and Roth.
	**shortestpath**: A fingerprint based on the shortest paths between pairs of atoms and takes into account ring systems, charges etc.
	**signature**: A feature,count type of fingerprint, similar in nature to circular fingerprints, but based on the signature descriptor.
	**circular**: An implementation of the ECFP6 fingerprint.
	**lingo**: An implementation of the LINGO fingerprint.
	**rdkit**: Another implementation of a Daylight-like fingerprint by RDKit.
	**maccs**: The popular 166 bit MACCS keys described by MDL.
	**avalon**: Substructure or similarity Avalon fingerprint.
	**atom-pair**: RDKit Atom-Pair fingerprint.
	**topological-torsion**: RDKit Topological-Torsion Fingerprint.
	**morgan**: RDKit Morgan fingerprint.
	**fp2**: OpenBabel FP2 fingerprint, which indexes small molecule fragments based on linear segments of up to 7 atoms in length.
	**fp3**: OpenBabel FP3 fingerprint, which is a fingerprint method created from a set of SMARTS patterns defining functional groups.
	**fp4**: OpenBabel FP4 fingerprint, which is a fingerprint method created from a set of SMARTS patterns defining functional groups.
	

