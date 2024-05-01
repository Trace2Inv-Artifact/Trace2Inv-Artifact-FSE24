## Description

This folder contains the storage mappings for some contracts which cannot be analyzed using compiler outputs. 

Particularly, for contracts compiled with vyper-0.2.15 or before, there is no such an "-f layout" option, so I really cannot find storage layout. 

Therefore, it requires me to predict storage Layout using past trace data. Luckily, it is not a common case and I can do it manually.


Other scenarios include developers used their customized storage Layout file (Vyper) or even customized compilers to compiler the contracts. 






