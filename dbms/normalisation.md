# Normalisation

process of minimizing redundancy in a relation  
features are,

1. Elimination of Data Redundancy
1. Ensure Data consistency
1. Avoid Anomolies

### Anomolies

inconsistencies that prevent operations.

1. Insertion Anomolies
    - cannot insert into refering relation
    - cause is referenced relation is not present
1. Updation/Deletion Anomolies
    - cannot update/delete referenced relation
    - cause is refering relation is present

Normalisation prevents Anomolies.

## Types

### 1st NF

-   only singled valued attributes (no composite or mutivalued)
-   every value in a column should have same domain
-   each column should have same name
-   order of rows and columns is not important
-   primary key must exist or no duplicate rows

when er diagram is converted into schema, its already 1NF

### 2nd NF

-   should be 1NF
-   no partial functional depedency
-   no proper subset of candidate keys defines a npa
-   union of proper subset are also considered

### 3rd NF

-   its 2nd NF
-   no transitive depedency among non prime attributes
-   i.e. no npa -> npa, for non trivial depedencies
-   here composite of pa & npa is npa

### BCNF

-   its 3rd NF
-   determinant is super key for all non trivial FDs.

### 4th NF

-   its BCNF
-   has no muti-valued depedency

### 5th NF

-   its 4NF
-   no further lossless decomposition possible

## Decomposition

divide relations, it must be

1. Depedency preserving (except for BCNF)
    - FD is equivalent to FD1 union FD2
    - to find FD set, find closure of each attribute
1. Lossless
    - if R1 natural join R2 is R
    - atleast one common attribute
    - common attribute must be super key atleast one subrelation
    - no extra records

### Natural Join

-   cartisian product then selection of same column
-   if no same column, all cartisian products

