# RFC

This document describes an extension of `mudata` that formalizes the hierarchical features relationship between different levels of quantification in MS-based proteomics. 


## User-facing functionality 

### Initialization

```python
import mudata as md
from scipy.sparse import csr_matrix

msdata = md.MuData(
    # These are the raw data levels
    {
        "protein_level": ad.AnnData(...),
        "peptide_level": ad.AnnData(...),
        "precursor_level": ad.AnnData(...),
    },
    # This stores the feature mapping as adjacency matrix of a DAG
    varp = csr_matrix(...)
)

```


## Class Methods
```python
msdata.to_anndata(level="precursors")
# Extracts precursor level and propagates metadata from all "higher" levels to `msdata.var`
```

## Tools
### Aggregation

```python
# Aggregation of lower level information
utils.tl.aggregate(msdata, feature="feature", on_column="gene")
```

```python
# Plotting 
utils.pl.barplot(msdata, feature="gene_A", var_level="gene", extraction_level="precursor", )
```

## Wants

- [ ] serializable
- [ ] interoperable with R

## Roadmap
### Minimal viable product
1. Implement DAG with varp attribute
2. Mark object ms-data/hierarchical feature-compatible (e.g. by adding a special key/value pair to mdata.uns)
### Robust implementation
3. Later: Implement custom class
4. Potential extensions: custom index (pandas index extension)
5. validation of hierarchies (DAG) level 


