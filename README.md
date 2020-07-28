This program uses an old trick to determine whether a number is divisible by a factor or not by performing a series of multiplication and addition/subtraction calculations. We take a number and apply a rule to it.

The multipliers we use are calculated according to the rules as shown under the table below:

Setup for factors ending in 1 - multiplier is factor divided by 10 as integer. Multiples of 1s are subtracted.

Setup for factors ending in 3 and 7 – multiplier is factor divided by 10 as integer then 1 is added to 3s and 2 to 7s. Multiples of 3s are added. Multiples of 7s are subtracted.

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
is limited to numbers of 128,000 digits in length. That is more than my laptop can handle.

As we can see factors ending in either 1, 3, 7, or 9 can be tested with the above process. Even numbers are tested by checking whether the last digit is 0, 2, 4, 6 or 8 and 
divisibility of five is similarly calculated by checking for 0 or 5. Divisibility by 3 is done by taking the sum of the digits and checking whether that is divisible by 3.
We can check very large number with these tricks.
A separate 7 test is done and if the number fails this test we go into a loop testing factors starting at 7 and alternating in +2 and +4 to skip factors of three
A different test is done for 11s; two sums are made form each alternating digit and then one sum subtracted from the other:

14641
(1+6+1)-( 4+5)=0

2746502
(2+4+5+2)-(7+6+0)=0



 
Multiplier values for some factors:
1s	minus	3s	plus	7s	minus	9s	plus		7s	plus		3s	minus
1	0	3	1	7	2	9	1		7	5		3	2
11	1	13	4	17	5	19	2		17	12		13	9
21	2	23	7	27	8	29	3		27	19		23	16
31	3	33	10	37	11	39	4		37	26		33	23
41	4	43	13	47	14	49	5		47	33		43	30
51	5	53	16	57	17	59	6		57	40		53	37
61	6	63	19	67	20	69	7		67	47		63	44
71	7	73	22	77	23	79	8		77	54		73	51
81	8	83	25	87	26	89	9		87	61		83	58
91	9	93	28	97	29	99	10		97	68		93	65
101	10	103	31	107	32	109	11		107	75		103	72
111	11	113	34	117	35	119	12		117	82		113	79
121	12	123	37	127	38	129	13		127	89		123	86
131	13	133	40	137	41	139	14		137	96		133	93
141	14	143	43	147	44	149	15		147	103		143	100
151	15	153	46	157	47	159	16		157	110		153	107
161	16	163	49	167	50	169	17		167	117		163	114
171	17	173	52	177	53	179	18		177	124		173	121
181	18	183	55	187	56	189	19		187	131		183	128
191	19	193	58	197	59	199	20		197	138		193	135
201	20	203	61	207	62	209	21		207	145		203	142
211	21	213	64	217	65	219	22		217	152		213	149

The columns at the right shows that 7s can be done with an additive process and 3s with a subtractive process, this not used.


Formula for 1s:		x=num/10
Formula for 3s:		x=((num/10)*3)+1
Formula for 7s:		x=((num/10)*3)+2
Formula for 9s:		x=(num/10)+1
Formula for plus 7s:		x=((num/10)*7)+5
Formula for minus 3s:	x=((num/10)*7)+2



In this version we use a side counting system to filter out multiples of 2,3,5,7,11 and 13. Our basic counting system is an alternative 2,4 so our count eg: 11,13,17,19,23,25,29
skips multiples of 3 and even numbers. We eliminate multiples of 5 by detrmining whether the last digit is 5. We eliminate multiples of 7,11 and 13 by using a counting system.

We can do the filtering of these numbers as we have used the 2,3,5,7,11,13 testing module described in another project.


I wrote this to see if there was a faster way to determine the primality of a number - turns out it's rather slow. It can determine that 999999999999989 is prime in just
under 16 seconds on my 1.1Ghz laptop. 99999999999973 takes a few seconds.

Better programmers can undoubtably make this a little quicker.
