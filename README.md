Not too sure why a copy and paste from Word has so may italics in it as there were none in the original. Just started learning GitHub.

This program uses an old trick to determine whether a number is divisible by a factor or not by performing a series of multiplication and addition/subtraction calculations. We
take a number and apply a rule to it.

You may have encountered the trick of figuring out whether a number is divisible by 7 by using a multiply and subtract method on the digits. This program extends that concept as
there is a pattern to the numbers and the formulas have been determined for all numbers ending in 1,3,7 or 9 (see below). We do not need to determine this formula for numbers
divisible by 2,3 or 5 as there are other simple methods for doing this.

Before we go on, I just need to point out that this is the result of learning to program in about 6 months. I will make no apologies for layou style as I like to see a lot of
code onthe one screen. Apologies for the actual code content will be granted on request. ;-)

On with the show. The essence of this program is to take a number with a lot of digits and then shrink that down to a number that we can then use subtraction as way of doing
division with up to 8 steps of subtraction in the final test of divisibility. In half out factors we are using an addition and divide by ten method before we do the final test 
nd the other half use subtraction (assuming an even distribution of primes in  respect to their last digit). Divide by ten is done by getting rid of the last digit in our array,
the ones digit, eg 1 2 3 4 5 becomes 1 2 3 4.

The multipliers we use are calculated according to the rules as shown under the table below:

Setup for factors ending in 1 - multiplier is factor divided by 10 as integer. Multiples of 1s are subtracted.

Setup for factors ending in 3 and 7 – multiplier is factor divided by 10 as integer, then multiplied by 3, then 1 is added to 3s and 2 to 7s.
Multiples of 3s are added.Multiples of 7s are subtracted.

Setup for factors ending in 9 - multiplier is factor divided by 10 as integer then 1 is added to that number. Multiples of 9s are added.


Take a number. We will use 343 and test whether it is divisible by 7.
The multiplier for 7 is 2 (7 divided by 10 plus 2) and it is a subtractive process.

We multiply the last digit of our number by 2 and then take the last digit away from our original number and subtract our multiplication result from the remainder.

343	2*3=6		34-6=28
28	2*8=16	2-16=-14

 Here we stop but if we took it a step further we would get

-14	2* -4 = -8	-1- -8=7

Thus 343 is divisible by 7.

Let’s try another:

For number is 92 and the factor is 23: the multiplier for 23 is 7 and it is an additive process.

92	7*2=14	9+14=23

And another:

23 and 9. The multiplier for 9 is 1 and it is additive.

23	3*1=3		2+3=5

23 is not evenly divisible by 9

This was written as a way of learning the C programming language. It started off with an array system that could do really, really big numbers by a series of arrays but could 
only do factors up to (2^64)-1. This approach was testing one factor at a time. A future version of this program may incorporate the series of arrays system but until now it
is limited to numbers of 128,000 digits in length. That is what my 4Gb laptop can handle.

As we can see factors ending in either 1, 3, 7, or 9 can be tested with the above process. Even numbers are tested by checking whether the last digit is 0, 2, 4, 6 or 8 and 
divisibility of five is similarly calculated by checking for 0 or 5. Divisibility by 3 is done by taking the sum of the digits and checking whether that is divisible by 3.
We can check very large number with these tricks.
A separate 7 test is done and if the number fails this test we go into a loop testing factors starting at 7 and alternating in +2 and +4 to skip factors of three
A different test is done for 11s; two sums are made form each alternating digit and then one sum subtracted from the other:
A test for 13s is also done and this method is described in the 2,3,5,7,11,13 test project. It's on the same principle as the above 11 method but uses numbers made up of 
bunches of three digits.

14641
(1+6+1)-( 4+5)=0

2746502
(2+4+5+2)-(7+6+0)=0


 
Multiplier values for some factors:
1s minus	3s	plus	7s	minus	9s	plus		7s	plus		3s	minus
11 1     13 4    17 5     19 2     7  5     23 16
31 3     43 13   37 11    29 3     47 33    53 37
<<Whole table removed as it did not display properly on viewing.>>
 As we can see our multipliers are less than a third (or less) of our factors and the additional columns [7s plus and 3s minus] have higher multipliers so not used).

Formula for (minus) 1s:		x=num/10
Formula for (plus) 3s:		x=((num/10)*3)+1
Formula for (minus) 7s:		x=((num/10)*3)+2
Formula for (plus) 9s:		x=(num/10)+1

Formula for (plus) 7s:		x=((num/10)*7)+5
Formula for (minus) 3s:	x=((num/10)*7)+2


In this version we use a side counting system to filter out multiples of 2,3,5,7,11 and 13. Our basic counting system is an alternative +2,+4 so our count goes that goes 
like this: 11,13,17,19,23,25,29,31,35....
skips multiples of 3 and even numbers. We eliminate multiples of 5 by detrmining whether the last digit is 5. We eliminate multiples of 7,11 and 13 by using a counting system
(v,w,x,y).

We can do the filtering of these numbers as we have used the 2,3,5,7,11,13 testing module described in another project.

I wrote this to see if there was a faster way to determine the primality of a number - turns out it's rather slow but it can determine the divisibility of 2,3,5,7,11,and 13
relatively quickly on quite large numbers. It can determine that 999999999999989 is prime in just under 16 seconds on my 1.1Ghz laptop. 99999999999973 takes a few seconds.
I thought with the use of a single multiplier (the last digit) and a less than a third multiplier (see formulas) and simple array addition or subtraction that these
operations may speed up the process.

Print statements have been left in for debugging and for seeing how it works. Toggle z to equal 1 to enable printouts. conio.h included to highlight factors and factor multiples
in printout.
At the prompt input a number up to 1000 (can be increased) digits long and end it with an 'e'*, then press enter. A crude status bar will indicate progress by counting back dots
from the
number of digits the root of the number is expected to have. Obviously some numbers need not go all the way to root to find their lowest multiple.
Output of 1 indicates the number is prime.

I think I can make this code even more confusing and submit it as an entry to the Obfucated C Code Contest. Primarily working on the novelty of the idea. Obviously the
variable and function names need to be shrunk and possibly a define needed(#define "something" for(j=1;j<=n;j++) cuts a bit out).

Tested extensively but I can't guarantee that there will not be errors. It is very possible that experienced programmers can make this a little more efficient. I think I would
like one day to be able to code something like this (or simple portions of it) in assembly, but that's a long way off.

Some speed was lost on the way especially using functions. This and other ways of shrinking the code may have comprimised accuracy. It may be possible to take t=8 down for a
slight speed increase with the adjustment of the program. Again, some things comprimised to shrink the code.

* The longer version of this has the abililty to filter out carriage returns in the input so you can input really, really big numbers (like up to 128,000 digits long) and not be
limited by keyboard buffers. 1001 (7x11x13) chosen as the number is used in the 7,11,13 test.
