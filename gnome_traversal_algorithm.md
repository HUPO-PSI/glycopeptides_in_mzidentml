# GNOme Ontology Traversal

## Valid Monosaccharides

The following monosaccharides are indexed by GNOme:

1. Hex
2. HexNAc
3. dHex
4. NeuAc
5. NeuGc
6. Pen
7. Fuc

The following "free" substituents are also included:

1. S - sulfate
2. P - phosphate

In order to map a glycan composition to an entry in GNOme, it must be composed of only these components. Glycans containing other monosaccharides may be included, but they will be encoded as "Xxx".

## Resolution Algorithm

### Step 1. Build Subsumption Graph
1. Construct a directed graph where all terms are nodes.
2. For each term *p*, find all terms *C* which have an `is_a` relationship with them and create an edge from *p* to *c* for each *c* in *C*.

### Step 2. Construct Mass Index
1. For each child term of `GNO:00000001` *c*, if the `name` of `c`  matches the pattern `/molecular weight (\d+(\.\d+)?) Da/`, then add `c` to a list of `(term, mass)` pairs `I`.
2. Sort `I` by `mass`. 

### Step 3. Index Traversal
1. For query glycan `G`, compute the neutral monoisotopic mass of `G`. Search the index `I` from Step 2 for the mass of `G`, finding the nearest available term  within 0.1 Da.
2. 