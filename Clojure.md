# Clojure

## Data Structures

Clojures data strucures are *immutable*.

1) Numbers
2) Strings::
    1) No interpolation, can concatenate only with _str_ function.
    2) only double quates _"_
3) Maps::
    1) Similar to dictionaries
    2) Empty map: {}
    3) Example:: 
            1) {:first-name "Charlie"
                :last-name "McDonald"}
    4)  Maps can be nested
    5) can be written also as (hash-map :a 1 :b 2)
4) Keywords::
    1) Primary used as keys in maps
    2) Ex. :a, :rubmle, :34, :_? etc.
    3) Keywords can be used as funtions that look up the corresponding key to a map
    4) Vectors
    5) Lists
    6) Sets::
        1) #{"kurt vonnegut 20 :icicle}"}

## Functions

### Defining functions
``` clojure
(def function-name
    "DocString"
    ![pic](arguments)
    (println "Function body")
)
  ```
    
1) Clojure automatically return the last form evaluated
2) All functions are created equal
3) Anonymous function::
    1) (fn ![pic](param-list) function body)
   
