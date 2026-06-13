# GENERATORS(yield)
 A generator is a special Python function that returns data chunk-by-chunk using the yield keyword instead of loading everything into a giant list at once.
### Why??
It completely stops Out-of-Memory (OOM) crashes. If an upstream system passes you a massive 20GB dataset, standard Python loops will try to load all 20GB into your computer's RAM, 
causing it to crash. A generator streams it line-by-line, keeping memory usage close to zero.

