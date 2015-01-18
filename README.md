# 16-bit-Unsigned-Divider
Designed for 16-bit unsigned data.  All the values here are unsigned integers.<br />

###### 1.1 Mechanism 
Explained in pseudo code(Q: quotient, R: remainder, N: dividend, D: divisor) N/D=Q...R
```
if D == 0 then throw an Exception end
Q = 0; R = 0;
for i =  n/2 -1..0 do // n is data width of N
 R = R << 2 
 R(1:0) = N(2i+1:2i) 
 if R >= 3D then
  R = R – 3D; Q(2i+1:2i) = 3; end
 else if R >= 2D then
  R = R – 2D; Q(2i+1:2i) := 2; end
 else if R>= D then
  R = R – D; Q(2i+1:2i) := 1; end
end
```
###### 1.2 Basic Schematic
![image] (https://dl.dropboxusercontent.com/s/kx1ykn9j2o9fqyw/image2.jpeg)

###### 1.3 Functionality Test

Use Perl(see [here](https://github.com/CWang24/16-bit-Unsigned-Divider/blob/master/divider_function_test_vec_gen.pl)) to create a vector file like this(N=8, D=3):
```
radix 4 4 1 1 1 1 
io  i  i  i  i  i  i 
vname Ni<15:12> Ni<11:8> Ni<7:4> Ni<3:0> D<3:0> D<15:12> D<11:8> D<7:4> D<3:0> Nselect reset clk ~clk
slope 0.01
vih 1.8
tunit ns
0 0 0 0 8 0 0 0 3 0 0 1 0
5 0 0 0 8 0 0 0 3 0 1 0 1
7.5 0 0 0 8 0 0 0 3 1 1 1 0
10 0 0 0 8 0 0 0 3 1 1 0 1
12.5 0 0 0 8 0 0 0 3 1 1 1 0
15 0 0 0 8 0 0 0 3 1 1 0 1
17.5 0 0 0 8 0 0 0 3 1 1 1 0
20 0 0 0 8 0 0 0 3 1 1 0 1
22.5 0 0 0 8 0 0 0 3 1 1 1 0
25 0 0 0 8 0 0 0 3 1 1 0 1
27.5 0 0 0 8 0 0 0 3 1 1 1 0
30 0 0 0 8 0 0 0 3 1 1 0 1
32.5 0 0 0 8 0 0 0 3 1 1 1 0
35 0 0 0 8 0 0 0 3 1 1 0 1
37.5 0 0 0 8 0 0 0 3 1 1 1 0
40 0 0 0 8 0 0 0 3 1 1 0 1
42.5 0 0 0 8 0 0 0 3 1 1 1 0
45 0 0 0 8 0 0 0 3 1 1 0 1
47.5 0 0 0 8 0 0 0 3 1 1 1 0
50 0 0 0 8 0 0 0 3 1 1 0 1
```
After simulation, we get the waveforms like this:
![image] (https://dl.dropboxusercontent.com/s/oeqk7gkmfqukmaf/image9.png?dl=0)
It's displaying Quotient[QO<15>:Q<0>]= and Remainder[R<15>:R<0>]=<br />
(Since I do not have the license of this Cadence Virtuoso any more, I could only view the circuits I designed at that time, while not allowed to run any simulation. The waveform figure above is one output of this circuit, but obviously the result is not corresponding to the input setting I wrote above.)<br />
(But trust me the design is abosolutely correct, otherwise we would not be able to carry on with the following processor design, while in the end actually our design was among the top 10 designs of that semester)
