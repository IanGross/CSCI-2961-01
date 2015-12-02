I read the book and the slides.

Here are the various tables my RStudio Produced

![File](http://i.xomf.com/wkvgn.png)

![File](http://i.xomf.com/mjjhka.png)

![File](http://i.xomf.com/qdxlqa.png)

![File](http://i.xomf.com/kwnxna.png)

![File](http://i.xomf.com/cvcbka.png)


Update on our project:

Was not able to accomplish much over the past week. We will continue work by getting RocketFish to work on our machines and start to fix easy issues.

Here's the code that I used to make rules and produce the graphs shown above, in case you need to look at it
```
> str(Titanic)
 table [1:4, 1:2, 1:2, 1:2] 0 0 35 0 0 0 17 0 118 154 ...
 - attr(*, "dimnames")=List of 4
  ..$ Class   : chr [1:4] "1st" "2nd" "3rd" "Crew"
  ..$ Sex     : chr [1:2] "Male" "Female"
  ..$ Age     : chr [1:2] "Child" "Adult"
  ..$ Survived: chr [1:2] "No" "Yes"
> df <- as.data.frame(Titanic)
> head(df)
  Class    Sex   Age Survived Freq
1   1st   Male Child       No    0
2   2nd   Male Child       No    0
3   3rd   Male Child       No   35
4  Crew   Male Child       No    0
5   1st Female Child       No    0
6   2nd Female Child       No    0
> 
> 
> install.packages("arulesViz")
Installing package into ‘C:/Users/grossi2/Documents/R/win-library/3.2’
(as ‘lib’ is unspecified)
trying URL 'https://cran.rstudio.com/bin/windows/contrib/3.2/arulesViz_1.0-4.zip'
Content type 'application/zip' length 608059 bytes (593 KB)
downloaded 593 KB

package ‘arulesViz’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
	C:\Users\grossi2\AppData\Local\Temp\Rtmpm6lrbv\downloaded_packages
> install.packages("arules")
Installing package into ‘C:/Users/grossi2/Documents/R/win-library/3.2’
(as ‘lib’ is unspecified)
trying URL 'https://cran.rstudio.com/bin/windows/contrib/3.2/arules_1.3-0.zip'
Content type 'application/zip' length 1867019 bytes (1.8 MB)
downloaded 1.8 MB

package ‘arules’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
	C:\Users\grossi2\AppData\Local\Temp\Rtmpm6lrbv\downloaded_packages
> load("C:/Users/grossi2/Documents/RPI Work Files/Computer Science/Open Source Software - CSCI 2961-01/labs/titanic.raw.rdata")
> summary(titanic.raw)
  Class         Sex          Age      
 1st :325   Female: 470   Adult:2092  
 2nd :285   Male  :1731   Child: 109  
 3rd :706                             
 Crew:885                             
 Survived  
 No :1490  
 Yes: 711  
           
           
> library(arules)
Loading required package: Matrix

Attaching package: ‘arules’

The following objects are masked from ‘package:base’:

    %in%, abbreviate, write

> rules.all <- apriori(titanic.raw)
Apriori

Parameter specification:
 confidence minval smax arem  aval
        0.8    0.1    1 none FALSE
 originalSupport support minlen maxlen target
            TRUE     0.1      1     10  rules
   ext
 FALSE

Algorithmic control:
 filter tree heap memopt load sort verbose
    0.1 TRUE TRUE  FALSE TRUE    2    TRUE

Absolute minimum support count: 220 

set item appearances ...[0 item(s)] done [0.00s].
set transactions ...[10 item(s), 2201 transaction(s)] done [0.00s].
sorting and recoding items ... [9 item(s)] done [0.00s].
creating transaction tree ... done [0.00s].
checking subsets of size 1 2 3 4 done [0.00s].
writing ... [27 rule(s)] done [0.00s].
creating S4 object  ... done [0.00s].
> rules.all
set of 27 rules 
> inspect(rules.all)
   lhs               rhs             support confidence      lift
1  {}             => {Age=Adult}   0.9504771  0.9504771 1.0000000
2  {Class=2nd}    => {Age=Adult}   0.1185825  0.9157895 0.9635051
3  {Class=1st}    => {Age=Adult}   0.1449341  0.9815385 1.0326798
4  {Sex=Female}   => {Age=Adult}   0.1930940  0.9042553 0.9513700
5  {Class=3rd}    => {Age=Adult}   0.2848705  0.8881020 0.9343750
6  {Survived=Yes} => {Age=Adult}   0.2971377  0.9198312 0.9677574
7  {Class=Crew}   => {Sex=Male}    0.3916402  0.9740113 1.2384742
8  {Class=Crew}   => {Age=Adult}   0.4020900  1.0000000 1.0521033
9  {Survived=No}  => {Sex=Male}    0.6197183  0.9154362 1.1639949
10 {Survived=No}  => {Age=Adult}   0.6533394  0.9651007 1.0153856
11 {Sex=Male}     => {Age=Adult}   0.7573830  0.9630272 1.0132040
12 {Sex=Female,                                                  
    Survived=Yes} => {Age=Adult}   0.1435711  0.9186047 0.9664669
13 {Class=3rd,                                                   
    Sex=Male}     => {Survived=No} 0.1917310  0.8274510 1.2222950
14 {Class=3rd,                                                   
    Survived=No}  => {Age=Adult}   0.2162653  0.9015152 0.9484870
15 {Class=3rd,                                                   
    Sex=Male}     => {Age=Adult}   0.2099046  0.9058824 0.9530818
16 {Sex=Male,                                                    
    Survived=Yes} => {Age=Adult}   0.1535666  0.9209809 0.9689670
17 {Class=Crew,                                                  
    Survived=No}  => {Sex=Male}    0.3044071  0.9955423 1.2658514
18 {Class=Crew,                                                  
    Survived=No}  => {Age=Adult}   0.3057701  1.0000000 1.0521033
19 {Class=Crew,                                                  
    Sex=Male}     => {Age=Adult}   0.3916402  1.0000000 1.0521033
20 {Class=Crew,                                                  
    Age=Adult}    => {Sex=Male}    0.3916402  0.9740113 1.2384742
21 {Sex=Male,                                                    
    Survived=No}  => {Age=Adult}   0.6038164  0.9743402 1.0251065
22 {Age=Adult,                                                   
    Survived=No}  => {Sex=Male}    0.6038164  0.9242003 1.1751385
23 {Class=3rd,                                                   
    Sex=Male,                                                    
    Survived=No}  => {Age=Adult}   0.1758292  0.9170616 0.9648435
24 {Class=3rd,                                                   
    Age=Adult,                                                   
    Survived=No}  => {Sex=Male}    0.1758292  0.8130252 1.0337773
25 {Class=3rd,                                                   
    Sex=Male,                                                    
    Age=Adult}    => {Survived=No} 0.1758292  0.8376623 1.2373791
26 {Class=Crew,                                                  
    Sex=Male,                                                    
    Survived=No}  => {Age=Adult}   0.3044071  1.0000000 1.0521033
27 {Class=Crew,                                                  
    Age=Adult,                                                   
    Survived=No}  => {Sex=Male}    0.3044071  0.9955423 1.2658514
> rules <- apriori(titanic.raw, control = list(verbose=F),
+                  + parameter = list(minlen=2, supp=0.005, conf=0.8),
Error: unexpected '=' in:
"rules <- apriori(titanic.raw, control = list(verbose=F),
                 + parameter ="
>                  + appearance = list(rhs=c("Survived=No", "Survived=Yes"),
+                                      + default="lhs"))
Error: unexpected '=' in:
"                 + appearance = list(rhs=c("Survived=No", "Survived=Yes"),
                                     + default="
> quality(rules) <- round(quality(rules), digits=3)
Error in quality(rules) : 
  error in evaluating the argument 'x' in selecting a method for function 'quality': Error: object 'rules' not found
> rules.sorted <- sort(rules, by="lift")
Error in sort(rules, by = "lift") : 
  error in evaluating the argument 'x' in selecting a method for function 'sort': Error: object 'rules' not found
> inspect(rules.sorted)
Error in inspect(rules.sorted) : 
  error in evaluating the argument 'x' in selecting a method for function 'inspect': Error: object 'rules.sorted' not found
> 
> rules <- apriori(titanic.raw, control = list(verbose=F),
+                  + parameter = list(minlen=2, supp=0.005, conf=0.8),
Error: unexpected '=' in:
"rules <- apriori(titanic.raw, control = list(verbose=F),
                 + parameter ="
>                  + appearance = list(rhs=c("Survived=No", "Survived=Yes"),
+                                      + default="lhs"))
Error: unexpected '=' in:
"                 + appearance = list(rhs=c("Survived=No", "Survived=Yes"),
                                     + default="
> rules <- apriori(titanic.raw, control = list(verbose=F), parameter = list(minlen=2, supp=0.005, conf=0.8),
+ appearance = list(rhs=c("Survived=No", "Survived=Yes"), default="lhs"))
> quality(rules) <- round(quality(rules), digits=3)
> rules.sorted <- sort(rules, by="lift")
> inspect(rules.sorted)
   lhs             rhs            support confidence  lift
1  {Class=2nd,                                            
    Age=Child}  => {Survived=Yes}   0.011      1.000 3.096
2  {Class=2nd,                                            
    Sex=Female,                                           
    Age=Child}  => {Survived=Yes}   0.006      1.000 3.096
3  {Class=1st,                                            
    Sex=Female} => {Survived=Yes}   0.064      0.972 3.010
4  {Class=1st,                                            
    Sex=Female,                                           
    Age=Adult}  => {Survived=Yes}   0.064      0.972 3.010
5  {Class=2nd,                                            
    Sex=Female} => {Survived=Yes}   0.042      0.877 2.716
6  {Class=Crew,                                           
    Sex=Female} => {Survived=Yes}   0.009      0.870 2.692
7  {Class=Crew,                                           
    Sex=Female,                                           
    Age=Adult}  => {Survived=Yes}   0.009      0.870 2.692
8  {Class=2nd,                                            
    Sex=Female,                                           
    Age=Adult}  => {Survived=Yes}   0.036      0.860 2.663
9  {Class=2nd,                                            
    Sex=Male,                                             
    Age=Adult}  => {Survived=No}    0.070      0.917 1.354
10 {Class=2nd,                                            
    Sex=Male}   => {Survived=No}    0.070      0.860 1.271
11 {Class=3rd,                                            
    Sex=Male,                                             
    Age=Adult}  => {Survived=No}    0.176      0.838 1.237
12 {Class=3rd,                                            
    Sex=Male}   => {Survived=No}    0.192      0.827 1.222
> subset.matrix <- is.subset(rules.sorted, rules.sorted)
> subset.matrix[lower.tri(subset.matrix, diag=T)] <- NA
> redundant <- colSums(subset.matrix, na.rm=T) >= 1
> which(redundant)
 {Class=2nd,Sex=Female,Age=Child,Survived=Yes} 
                                             2 
 {Class=1st,Sex=Female,Age=Adult,Survived=Yes} 
                                             4 
{Class=Crew,Sex=Female,Age=Adult,Survived=Yes} 
                                             7 
 {Class=2nd,Sex=Female,Age=Adult,Survived=Yes} 
                                             8 
> 
> rules.pruned <- rules.sorted[!redundant]
> inspect(rules.pruned)
  lhs             rhs            support confidence  lift
1 {Class=2nd,                                            
   Age=Child}  => {Survived=Yes}   0.011      1.000 3.096
2 {Class=1st,                                            
   Sex=Female} => {Survived=Yes}   0.064      0.972 3.010
3 {Class=2nd,                                            
   Sex=Female} => {Survived=Yes}   0.042      0.877 2.716
4 {Class=Crew,                                           
   Sex=Female} => {Survived=Yes}   0.009      0.870 2.692
5 {Class=2nd,                                            
   Sex=Male,                                             
   Age=Adult}  => {Survived=No}    0.070      0.917 1.354
6 {Class=2nd,                                            
   Sex=Male}   => {Survived=No}    0.070      0.860 1.271
7 {Class=3rd,                                            
   Sex=Male,                                             
   Age=Adult}  => {Survived=No}    0.176      0.838 1.237
8 {Class=3rd,                                            
   Sex=Male}   => {Survived=No}    0.192      0.827 1.222
> 
> rules <- apriori(titanic.raw, parameter = list(minlen=3, supp=0.002, conf=0.2), appearance = list(rhs=c("Survived=Yes"),lhs=c("Class=1st", "Class=2nd", "Class=3rd","Age=Child", "Age=Adult"),default="none"),control = list(verbose=F))
> rules.sorted <- sort(rules, by="confidence")
> inspect(rules.sorted)
  lhs                      rhs            support     confidence
1 {Class=2nd,Age=Child} => {Survived=Yes} 0.010904134 1.0000000 
2 {Class=1st,Age=Child} => {Survived=Yes} 0.002726034 1.0000000 
5 {Class=1st,Age=Adult} => {Survived=Yes} 0.089504771 0.6175549 
4 {Class=2nd,Age=Adult} => {Survived=Yes} 0.042707860 0.3601533 
3 {Class=3rd,Age=Child} => {Survived=Yes} 0.012267151 0.3417722 
6 {Class=3rd,Age=Adult} => {Survived=Yes} 0.068605179 0.2408293 
  lift     
1 3.0956399
2 3.0956399
5 1.9117275
4 1.1149048
3 1.0580035
6 0.7455209
> 
> library(arulesViz)
Loading required package: grid

Attaching package: ‘arulesViz’

The following object is masked from ‘package:arules’:

    abbreviate

The following object is masked from ‘package:base’:

    abbreviate

> plot(rules.all)
> plot(rules.all, method="grouped")
> plot(rules.all, method="graph")
"rror: unexpected input in "plot(rules.all, method="graph")
> plot(rules.all, method="graph")
> plot(rules.all, method="graph", control=list(type="items"))
> plot(rules.all, method="paracoord", control=list(reorder=TRUE))
```
