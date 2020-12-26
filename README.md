# Calculate-Agreement-Disagreement (Javascript Implementation for each Formula):

*Measures of Disagreement/Agreement level that the number of voters are more than the selected categories.*

Calculation dis/agreement for the group is important for collective status statistics and opinion, also matter of interest in physiological and social apps to have an overall view and understanding of students within the group of teenage students about specific social objects with limited choices. 
In this overview, we define and compare the methods to calculate the dis/agreement. include their JS functions. The whole functions can also be found inside of
the GitHub package as a HTML file. 

Methods which are selected for this document are :
1. Dispersion index (DI)
2. Fleiss' kappa (Pi section of FK)
3. Group disagreement (GD):
4. Entropy-based diversity index (H) 
5. Simpson’s Diversity Index (SDI)

If these measures are normalized on a scale ranging from 0 to 1, this correspondence is expressed by the equation D = 1 – A. In this sense, dispersion and 
entropy are D-measures whereas inter-rater reliability id an A-measure.

Our interest is to calculate the dis/agreement for the cases in which the number of categories **K** are lower than the number of voters (participants) 
**N**, then we have **N>K**.
One example of the approach that we are could be a task for the group of students  **N=6**  (thirty students) has to categorize an artifact which can be a 
single image into the different categories **K=4**. The categories can be "Hate," "discrimination," "Cyber bullying" and none. 
when all students vote for Hate, then the expected is **Disagreement = 0**.  
Here if we have different tree images and six students (N=6) has to vote and choose between the mentioned 4 categories (K=4), the desired result will be somethinglike below:

<p align="center" width="100%">
    [6,0,0,0]
    <img width="23%" src="https://user-images.githubusercontent.com/17232450/103105085-a45c9100-462b-11eb-8bf8-41569969514e.png"> 
    [3,1,1,1]
    <img width="23%" src="https://user-images.githubusercontent.com/17232450/103105183-5431fe80-462c-11eb-8198-aa0407751c7b.png"> 
    [2,2,1,1]                                                                                                                             
    <img width="23%" src="https://user-images.githubusercontent.com/17232450/103105335-77a97900-462d-11eb-8c16-1d9bee2259ad.png"> 
</p>

### 1. Dispersion index (DI):
The “dispersion index” (DI) is one of the few genuine statistical dispersion measures that work with nominal or categorical variables. We rely on the description and definition given by Walker (1999) [1]:

<img width="75%" src = "https://user-images.githubusercontent.com/17232450/103105551-d0c5dc80-462e-11eb-973c-112df449cbc4.png">

code:
```
//================Dispersions Messurment=========================
{
//let k = catNs.length; //  k is constant (number of toxic categories which is 4 in this example)
let k = 4; 
catNs.map(a => a.tag);
function arraysum(array) {
return array.reduce(function (accu, i){
    return accu + i;
    }, 0)
}
let n = arraysum(catNs);
let catN2s = catNs.map(function (i) {
    return i * i;
});
let sumN2 = arraysum(catN2s);
let Divergence = 0;
if (n === 0) {
  println("DM :" + (Divergence));
} else {
        Divergence = (k === 1) ? 1 : (k * (n * n - sumN2)) / ((k - 1) * n * n);
        // println("Normalised Agreement measure:" + (1 - Agreement * Agreement));
        println("DM :" + (Divergence));
    }
```    
    
### 2. Fleiss' kappa (Pi section of FK)

Fleiss' kappa (Fleiss, 1971) is a statistical measure for evaluating the reliability of agreement between a fixed number of raters when assigning 
certain ratings to possibly multiple items. The Pi-value is normalized and measures agreement, so that 1 – Pi can serve as a D-measure. Pi param-
eter of Fleiss' kappa, which only works when evaluating raters' agreement reflection of raters for one specific artifact [2].

<img width="75%" src = "https://user-images.githubusercontent.com/17232450/103105734-dff95a00-462f-11eb-979d-89a9881ab32e.png"> 

```
//=================Pi parameter of Fleiss' kappa==========================
{
   let Pi = 0;
   let n = 0;
   catNs.map(x => (n = x + n));
   let n1 = 0;
   let SumNpow2k = 0;
   let map1Pow2 = catNs.map(x => (n1 = (x * x)));
   map1Pow2.map(x => (SumNpow2k = x + SumNpow2k));
   Pi = (1 / (n * (n - 1))) * ((SumNpow2k) - (n));
   println("1-Pi   :  " + (1 - Pi)); // Pi is toggled for dis
   document.write("<br>");
}
```
### 3. Group disagreement (GD):
To quantify disagreement, Whitworth (2007) has introduced a measure that builds up an overall disagreement value from pairwise individual disagreement values forming a “disagreement matrix” (dij). The binary value dij is 0 if the two raters i and j have given different ratings (or tags), otherwise it is 1 (including for the diagonal values dii).[3] An individual's disagreement (di) with the rest of the group is then the sum of disagreements with each other group member, divided by the number of pairs (n-1):

 <img width="75%" src = "https://user-images.githubusercontent.com/17232450/103107208-5a2fdb80-463c-11eb-9e79-d8f8bf50b803.png">

The overall group disagreement is then the average of the disagreement of all its members.
If all raters and ratings agree (unanimously), the value GD will be 0. The maximum possible value 1 of group disagreement can only be reached if there are at least as many categories as there are raters (otherwise some raters would have to coincide in their ratings). GD is actually a genuine measure of disagreement. To make it comparable to the other measures targeting agreement, we can move to “group agreement” GA defined as 1 – GD. These measures can be formulated in the same way using an “agreement matrix” (aij) where aij = 1 - dij. Here, the aij values can be grouped and summed up in terms of the frequencies per category (for reasons of space, this cannot be fully elaborated here):
 
 <img width="45%" src = "https://user-images.githubusercontent.com/17232450/103107224-792e6d80-463c-11eb-85e0-045a197c8a58.png">

Given that the sum of frequencies over all categories is equal to the number of raters, i.e. we can rewrite the above formula:

 <img width="75%" src = "https://user-images.githubusercontent.com/17232450/103107237-96fbd280-463c-11eb-87ba-9f399102cef9.png">
The resulting formula is identical to the one of 𝑭𝑲 (Fleiss' kappa), i.e. 𝑮𝑨 = 𝟏 − 𝑮𝑫 = 𝑭𝑲 .

```
//================Group Disagreement=========================
{
   let n = 0;
   catNs.map(x => (n = x + n));
   //  println("number of students:");
   //  println(n);
   let disagreement = 0;
   let allSum = 0; // sum up all individual disagree
   //let frequency = 0;// number of voters for each category
   for (const frequency of catNs) { //runs over categories, frequency is the number of voter for each category
   // println(frequency);
   disagreement = n - frequency; // as mentioned in the paper we want to find the idea of the voter in comparison from rest of the ,
   // println("disagreement :"); // means if the group is empty then the ==>
   // println(disagreement);
   switch (frequency) {
       case (0) :
         disagreement = 0; // ==> disagreement will be zero (no one participate in X category)
         break;
       case (1) :
         allSum += (disagreement); //==> means just one person will be in x category and all other voters has different ideas (n-1 voters are disagree)
         break;
       default  :
         allSum += (disagreement * frequency);// ==> A AAAB in this case frequency is (A.frequency) = 4,
         // or we can say A happend 4 times, then instead of looping and calculation disagreement for each
         // A (vote) we consider one dis*frequency(number of voters for each category).
         }
    }
    GroupOfDisagreement = (allSum / (n * (n - 1)));
    //GroupOfAgreement = 1 - GroupOfDisagreement;
     println("GD : " + GroupOfDisagreement);
}
```
### 4. Entropy-based diversity index (H)
  Diversity or disagreement in a community can also be measured by the entropy using Shannon’s formula (counting only non-empty categories):
  
  <img width="24%" src = "https://user-images.githubusercontent.com/17232450/103107269-d2969c80-463c-11eb-895c-2506646769e3.png"> 

 The highest value for the Shannon measure is log⁡(n). The Normalized formula is:
 
  <img width="16%" src = "https://user-images.githubusercontent.com/17232450/103107282-ecd07a80-463c-11eb-9a93-5bc3d47ee5cf.png"> 

```
//=================Shanon diversity index ==========================
{
   let k = 4;
   let fk = 0;
   let n = 0;
   let shannon = 0;
   let e = Math.exp(1);
   catNs.map(x => (n = x + n));

   function CalculateSpi(fk) {
        return (fk / n);
   }

   catNs.map(fk => shannon += ((CalculateSpi(fk)) * getBaseLog(e, CalculateSpi(fk))));
   document.write("Shanon Diversity :  " + (-1) * shannon);
   document.write("<br>");
   document.write("Normalised Shanon Diversity :  " + ((-1) * shannon) / getBaseLog(e, n));//Math.E() Euler's number constant = 2.718281828459045
   document.write("<br>");
   //document.write(getBaseLog(e, n));
   //document.write("Normalised and round the result of Shanon Diversity :  " +  Math.round(((-1) * shannon) / getBaseLog(e, n)) );//Math.E() Euler's number        constant = 2.718281828459045
   //document.write("Normalised Shanon Diversity :  " + ((-1) * shannon)/1.3862943611199137);
   document.write("<br>");
   }
```

### 5. Simpson’s Diversity Index (SDI)

Simpson's Diversity Index (DI) is a measure of diversity that was introduced by Edward H. Simpson in 1949. It is often used in ecology to quantify the biodiversity of an environment [4]. Simpson's index takes into account the number of species present, as well as the abundance of each species. It can be used to quantify the diversity of a community also in the statistical calculation, for the modern application it can consider as disagreement measure among the raters.

 <img width="75%" src = "https://user-images.githubusercontent.com/17232450/103107674-da584000-4640-11eb-91c1-d243c23fe7ec.png"> 

according to previous sectoins → SDI=GD=(1-Pi)  
```
//=================  Simpson's index of diversity ==========================
{
    //document.write(getBaseLog(2.718281828459, 0.05));
    //let k = 4;
    let sumFk = 0;
    let n = 0;
    catNs.map(x => (n = x + n));
    catNs.map(fk => sumFk += (fk) * (fk - 1));
    let simpson = (1 - (sumFk / (n * (n - 1))));
    document.write("Simpson's index :  " + simpson);
 }
//===========================
```
 <img width="105%" src = "https://user-images.githubusercontent.com/17232450/103107682-eb08b600-4640-11eb-9ebf-0dc3c364aae9.png"> 
 
            **Figure 1. Values of disagreement for different measures (1 item, 6 raters, 4 possible tags)**

Figure 1 shows the values of disagreement resulting from the measures DI, GD, SDI (equal to 1 – FK) and H (entropy) for a simple situation with 6 raters giving one rating each for one item. We consider A, B, C, D as possible categorical values (however not necessarily all used). The set of example ratings is AAAAAA, AAAAAB, AAAABB, AAAABC, AAABBB, AABBCC, AAABCD, and AABBCD. The values of GD and DI appear to be very similar. A more detailed analysis shows that they only differ only in terms of the normalization
factor ( [𝑁2 − 𝑁 ]) instead of [ 𝑁2 − 𝑁2 (1)] ). This difference has a consequence for the possible maximum 𝐾
values, which is especially relevant when the number of categories is lower than the number of raters. As already noted by Whitworth (2007), the maximum value of GD tends to approach (K – 1) / K for a high number of raters, which amounts to 0.5 for K = 2. The normalization factor of DI corrects for this cap in the range of values. Based on this analysis, we have chosen to use DI as our measure of disagreement.

if you run the JS provided html file the output will be:

 <img width="79%" src = "https://user-images.githubusercontent.com/17232450/103107765-c3feb400-4641-11eb-8813-936671a78979.png">


The above article where writen under the supervison and contribution of RIAS institute. special thanks Prof. H. U Hoppe and Nils Malsen.

For any further question please dont hesitae to contact us:

http://rias-institut.de

fa@rias-institute.eu 


### REFERENCES 


[1]  Walker, Jeffery T. Statistics in criminal justice: Analysis and interpretation. Jones & Bartlett Learning, 1999.

[2]  Fleiss, J. L. (1971) "Measuring nominal scale agreement among many raters." Psychological Bulletin, Vol.    76, No. 5 pp. 378–382

[3] Whitworth, Gallupe, & McQueen, 2000. “Measuring Disagreement”

[4] Magurran, A. E. 1988. Ecological Diversity and its Measurement. Princeton University Press, Princeton, NJ.

[5] Shannon, Claude E. "A mathematical theory of communication." The Bell system technical journal 27.3 (1948): 379-423.

https://pure.mpg.de/rest/items/item_2383162_7/component/file_2456978/content

[6] ROBERT K. PEET , RELATIVE DIVERSITY INDICES1 https://pdfs.semanticscholar.org/eda4/19a5287c9a6e6ceaae05763473c882ab1ca9.pdf

#code#github#Code#Github#agreement#calculate#agreementmethod#
