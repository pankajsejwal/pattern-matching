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


dissect([_a,[__a1]],[1,[2,3,[[5]]]]); => [[a,[1]],[a1,[2,3,[[5]]]]]

Now that list elements have been separated as per patterns all one needs to do rearrange them as needed, for example,
rearrange(dissect([_a,[__a1],_c],[1,[2,3,[[5],7]],4]),[a,a1,c]); => [1,2,3,[[5],7],4]

If some pattern doesn't match then it returns the original input list unmanipulated.

For operations like,
rearrange(dissect([_a,[__a1],_c],[1,[2,3,[[5],7]],4]),[a,a1*c,c^3]);
=> [1,8,64]
This is not what one had expected, but not to worry as Mathematica will also give unpredictable results on sequences.
One can expect predictable results only on atoms/lists obtained as pattern matching output.
rearrange(dissect([_a,[__a1],_c],[1,[[[5],7]],4]),[a,a1*c,c^3]);
=> [1,[[20],28],64]

Also one can do checks like that in Mathematica,taking a more nested list,
eer:dissect([_a,[_a1,_a2,__b,[_e,__f],[_g,_h]],_c],[1,[2,3,4,[[5,6],7,8],[7,8,8,9]],4]);
map(lambda([y],if(first(last(y))>=4)then y),sublist(eer,lambda([x],first(x)=c))); => [c,[4]]

To be able to do it, APIs related to 'Position' of element in list have been used and can be obtained from another
file named 'positions' in GIT.
I would request everyone to use it and if one finds bugs, please share it with me.


If someone tries and faces any problem, I would be glad to interact with them and sort it out.


For detailed explaination:

https://www.academia.edu/8315769/Mathematica_style_pattern_matching_without_using_function_closures






