# DSI_project_4_plant_disease

Group Members:

Derik Vo

Veda Patel

Yasser Siddiqui

## Problem Statement:

[According to Adhikari, Oh, and Panthee (2019)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5666701/) they found that the world wide production of tomatoes is an estimated 161.7 million metric tons. This has an estimated evaluation of %59 billion dollars, of that the USA produces an estimated 13.2 million metrics tons-- placing third in total world production of tomatoes. According to the [USDA (2022)](https://www.ars.usda.gov/news-events/news/research-news/2021/wild-potatoes-tapped-for-late-blight-guard-duty/) late blight has inflicted an estimated $6.7 billion dollars in annual losses that includes tomatoes and potatoes. 

The USDA defines blight as a fungus-like pathogen that destroys a plant's leaves, stem, fruit, or tubers. Adhikari et al. (2019) explains blight reproduces asexually, and that it essentially goes dormant in winter and infects plants in warm and humid conditions. They state the condia, or a spore [Britannica](https://www.britannica.com/science/conidium), usually germinates at 8 to 32 celsius. Once these fungal spores grow they will eventually kill the host cells by producing toxins. These toxins and display symptoms such as "dark, small, necrotic, coalescing, and concentric lesions...on the leaf surface" (Adhikari et al., (2019). Additional, they state that lesions also appear on the stem and can extend to the flesh of the fruit.

Adhikari et al (2019) state the most common method of prevention of blight is through screening. However, they state that this can be labor intensive to identify and treat blight. Meeting this need the goal of this project is to use a neural network to correctly classify if a tomato plant is healthy, in the early stages of blight, or in the late stages of blight. With this tool we can pair it with machines to identify when a plant needs intervention. Furthermore, we can also work with engineers to build a machine to automatically apply treatment to infected plants.

For our project we will build two neural networks for the purposes of classification. [Model 1](./notebooks/PlantVillageModeling.ipynb) will be used to determine if a plant is healthy or has blight, so we can use that for transfer learning. [Model 2](./notebooks/PlantVillageModeling.ipynb) Will then be used to determine what stage of blight a plant is in.

The model will be evaluated using a confusion matrix, but we will primarily be focusing on the recall score, specifically the false negatives. Missing early stages of blight can have disastrous effects on crop yield due to spread. By the time late stage blight has set in, then it will be too late. Therefore our focus will be the recall score of early blight. 
_________________________________________________________________________________

## EDA

For our [EDA process](./notebooks/PlantVillageEDA.ipynb) we used Google google Colaboratory. To reproduce our results users will need to download the tomatoes dataset from the [PlanVillage_data Set](https://www.kaggle.com/datasets/emmarex/plantdisease) and mount it to their drive. The structure needs to have the master folder as "[plant name]" and sub folders should be "[{plant name}\_[status]\_[status]]" for example. **Tomato** folder should have the sub folders **Tomato_healthy**, **Tomato_Early_blight**, **Tomato_Late_blight**. File names are case sensitive as well.

During the EDA phase we downloaded the tomato dataset from [PlanVillage](https://www.kaggle.com/datasets/emmarex/plantdisease) where we found a total of 4500 images the distribution of images is as follow.
### Tomatoes
|Healthy|Early Blight|Late Blight|
|-----|-----|-----|
|1000 Images|1591 Images|1909 Images|

### Potatoes

|Healthy|Early Blight|Late Blight|
|-----|-----|-----|
|152 Images|1000 Images|1000 Images|

After loading our data we wanted to take the average pixel values of each class since the images were separated in their relative classes.

**Added images of examples** 

Although not immediately obvious there is already a difference that can be observed in the averaging of the pixel values of the three different classes. The healthy leaves show a bit more of a lighter green and shine. This could be indicative that healthier leaves reflect light better. The early blight leaves averaged out the darkest. This could be indicative that the loss of health lead to less reflectiveness in the leaves. The dark patches were also lowering the average value as well. The Late Blight, however, averaged out even lighter, but the it still doesn't have as much a reflectiveness to it, and the color value started to shift to yellow, presumably from all the green and brown color values from mixing.

The next step was to reorganize the file data set files into two categories one to determine if a plant is healthy or has blight, and two to determine if a plant has early blight or has late blight. These two categories will be used to train the two models mentioned earlier. The following provides insight on the structure of our data.

_______________________________________________________________________________________

## Modeling

For our modeling stage we have two separate notebooks one for our [Tomato](./notebooks/02_plant_village_potato_modeling.ipynb) which built 9 models to classify if a tomato is healthy or if its in early or late stages of blight. For our second model for [Potatoes](./notebooks/02_plant_village_tomato_modeling.ipynb) we built 5 models. 
### Tomato

||Precision|recall|f1|
|------|-----|-----|-----|
|Potato early blight|.87|.78|.82|
|Potato late blight|.89|.94|.92|
|Potato healthy|.99|.99|.99|

For our tomato model our best accuracy score was 96%, for our validation out score was 92%; However, it had a low recall score for early blight (.78). Which is not a result we want because the goal of our model was to limit the number of false negatives for early blight being categorized as healthy.



### Potatoes

||Precision|recall|f1|
|------|-----|-----|-----|
|Potato early blight|.99|.96|.97|
|Potato late blight|.94|.97|.95|
|Potato healthy|.92|.80|.86|

For our potato model our best accuracy was 99% for the training set and 95% for our validation set. This data set had a relatively good recall score (97%) for early blight; however, it should be noted that there were severe class imbalances. In this set there were only 152 healthy images compared to 1000 early blight images and 1000 late blight images. Because of this imbalance this model may not generalize well when presented with new data.


________________________________________________________________________

## Conclusion

Our model for tomatoes performs pretty well when measuring for accuracy; however, when measuring for recall the model suffers with correctly classifying tomato leaves with early blight. This is a significant issue because that can have detrimental effects on farmers if an disease is left untreated and spreads to other crops.

When evaluating our model for potatoes it had similar performances to out tomato model. The recall score is slightly higher when classifying potatoes with early blight (.96 against .78)