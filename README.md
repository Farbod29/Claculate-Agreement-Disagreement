## Calculate-Agreement-Disagreement
Measures of Disagreement/Agreement level that the number of voters is more than the selected categories.
Calculation dis/agreement for the group is important for collective status statistics and opinion, also matter of interest in physiological and social apps to have an overall view and understanding of students within the group of teenage students about specific social objects with limited choices. 
In this overview, we define and compare the methods to calculate the dis/agreement. Which their JS functions. The whole functions can also be found inside of the GitHub document. 
Methods which are selected for this document are :

If these measures are normalized on a scale ranging from 0 to 1, this correspondence is expressed by the equation D = 1 – A. In this sense, dispersion and entropy are D-measures whereas inter-rater reliability id an A-measure.

Our interest is to calculate the dis/agreement for the cases in which the number of categories **K= 4** are lower than the number of voters (participants) **N**, then we have **N>K**.
One example of the approach that we are could be a task for the group of students  **N** N=6 (thirty students) has to categorize an artifact which can be a single image into the different categories **K= 4** categories can be "Hate," "discrimination," "Cyber bullying" and none. 
when all students vote for Hate, then the expected **Disagreement = 0**.  
here if we have different tree images and six students (N=6) has to vote and choose between the mentioned 4 categories (K=4), the desired result will be sth like below: 
<p align="center" width="100%">
    [6,0,0,0]
    <img width="26%" src="https://user-images.githubusercontent.com/17232450/103105085-a45c9100-462b-11eb-8bf8-41569969514e.png"> 
    [3,1,1,1]
    <img width="26%" src="https://user-images.githubusercontent.com/17232450/103105183-5431fe80-462c-11eb-8198-aa0407751c7b.png"> 
    [2,2,1,1]                                                                                                                             
    <img width="26%" src="https://user-images.githubusercontent.com/17232450/103105335-77a97900-462d-11eb-8c16-1d9bee2259ad.png"> 
</p>

### 1. Dispersion index (DI):
The “dispersion index” (DI) is one of the few genuine statistical dispersion measures that work with nominal or categorical variables. We rely on the description and definition given by Walker (1999) [1]:
![Screenshot 2020-12-24 at 21 27 22](https://user-images.githubusercontent.com/17232450/103105551-d0c5dc80-462e-11eb-973c-112df449cbc4.png)

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

Fleiss' kappa (Fleiss, 1971) is a statistical measure for evaluating the reliability of agreement between a fixed number of raters when assigning certain ratings to possibly multiple items. The Pi-value is normalized and measures agreement, so that 1 – Pi can serve as a D-measure. Pi parameter of Fleiss' kappa, which only works when evaluating raters' agreement reflection of raters for one specific artifact [2].

<img width="73%" src = "https://user-images.githubusercontent.com/17232450/103105734-dff95a00-462f-11eb-979d-89a9881ab32e.png"> 

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





