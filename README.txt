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

Sample Usage examples:

disect([_s,_r,___w],[[9,1,2,3,[4,5]]]); => []
disect([_s,_r,__w],[1,2,[3,[4,5]]]); => [[_s,1],[_r,2],[__w,[[3,[4,5]]],[]]]
disect([___q,___e,___r,___s,___w,___t],[1,2,3,4,5]);
=> [[___q,[]],[___e,[]],[___r,[]],[___s,[]],[___w,[]],[___t,[],[1,2,3,4,5]]]


For detailed explaination:

https://drive.google.com/file/d/0B36DQjLI_-hxek5zX3V3MHMzLXc/edit?usp=sharing






