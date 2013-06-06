# shogun features wishlist:
 
 1. OpenMP support
 2. replace SG_REF + SG_UNREF with smart pointers (maybe c++11?)
 3. support for drop-in replacement for std malloc (memory managment). e.g. jemalloc
 4. thread pool
 5. add CSGObject::clone() that implements clone() for all the derived classes
 6. implement baseline ML algorithms that are almost in every other ML library are available (random forests, adaboost)
 7. documention/howto/examples for each and every algorithm we have in shogun. the examples preferable implemented in python
 8. large scale
 9. SGString -> SGReferencedData
 10. SGSparse* -> SGReferencedData
 11. CSGObject::equals() support
 12. nice model selection syntax