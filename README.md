# Calculate-Agreement-Disagreement
Measures of Disagreement/Agreement level that the number of voters is more than the selected categories.
Calculation dis/agreement for the group is important for collective status statistics and opinion, also matter of interest in physiological and social apps to have an overall view and understanding of students within the group of teenage students about specific social objects with limited choices. 
In this overview, we define and compare the methods to calculate the dis/agreement. Which their JS functions. The whole functions can also be found inside of the GitHub document. If these measures are normalized on a scale ranging from 0 to 1, this correspondence is expressed by the equation D = 1 – A. In this sense, dispersion and entropy are D-measures whereas inter-rater reliability id an A-measure.

Our interest is to calculate the dis/agreement for the cases in which the number of categories **K= 4** are lower than the number of voters (participants) **N**, then we have **N>K**.
One example of the approach that we are could be a task for the group of students  **N** N=6 (thirty students) has to categorize an artifact which can be a single image into the different categories **K= 4** categories can be "Hate," "discrimination," "Cyber bullying" and none. 
when all students vote for Hate then the expected **Disagreement = 0 **   

<p align="center" width="100%">
    [6,0,0,0]
    <img width="26%" src="https://user-images.githubusercontent.com/17232450/103105085-a45c9100-462b-11eb-8bf8-41569969514e.png"> 
    [3,1,1,1]
    <img width="26%" src="https://user-images.githubusercontent.com/17232450/103105183-5431fe80-462c-11eb-8198-aa0407751c7b.png"> 
    [2,2,1,1]                                                                                                                             
    <img width="26%" src="https://user-images.githubusercontent.com/17232450/103105335-77a97900-462d-11eb-8c16-1d9bee2259ad.png"> 
</p>

