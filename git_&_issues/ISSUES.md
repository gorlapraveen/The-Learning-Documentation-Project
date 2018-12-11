## Git Issues :



1. `error: insufficient permission for adding an object to repository database .git/objects`


Solution: 
   
       git gc


Even when you have same error, then you need aggressive gc

        git gc --aggressive

This is the things that clearly makes the biggest impact.

