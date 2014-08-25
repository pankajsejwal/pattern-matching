pattern-matching
================

To implement Mathematica style pattern matching in Maxima.
This work is in its initial stage.

What this achieves is seggreagating the list based on "_","__" & "___" patterns exactly as Mathematica. 
Mathematica's pattern matcher is quite powerful and can do a lot, but this program helps in investigation.

Methods:
1) disect : main body of program.
2) propagate : handles "_".
3) propagate2: handles "__".
4) propagate_3: handles "___".

The basic idea is that "__" & "___" act as bags and once the data is propagated to one of these, entries before these
are never backtracked.


