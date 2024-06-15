# Large language models (i.e., GPT-4) for Zero-shot Intent Classification in English (En), Swahili (Sw), Japanese (Jp) & Urdu (Ur)

This project explored the potential of deploying large language models (LLMs) such as GPT-4, to perform zero-shot intent classification. 
By introducing a new dataset of 8,453 sentences across 6 distinct intent classes, namely: **pets, food, job, hobby, sport, drink**; our work made two main contributions. 

First of all, we demonstrated that LLMs can indeed perform intent classification tasks through prompting. This aligns with the current trend which aims to exploit the power of in-context learning in LLMs, without the need for for additional fine-tuning. 

Secondly, to test our hypothesis, we introduced a unique dataset that was used to further explore and analyze zero-shot intent classification, providing a valuable resource for the research community.
### 🤖 🤖    Human-Robot Interaction
We envision a scenario in which the human and the robot engage in discussion over a wide range of topics. For example:

![Results](/images/ICexampleChat.png)

From the above illustration, we can deduce that the phrase `Cochinita Pibil for sure!` is related to the `intent` called `food` because the human is answering the question `what's your favorite cuisine?` 

## :card_file_box: The Dataset
In this dataset, we set out to defer from the conventional norm in which intent classification datasets are constructed.
For each sentence in the dataset, only a label which identifies the intent label to which the sentence belongs is included. 

**No slot labels are added to the token inside each sentence.**
Our goal is to investigate if LLM such as Llama-2, GPT-4 can distinguish correctly sentences which belong to different intent categories, with **incontext learning**, i.e., prompting. 

We do not intend to do conduct fine-tuning on this dataset. Our target domain is human-robot interaction (HRI).

We considered the following intent categories: pets, food, job, hobby, sport, drink. There is one file corresponding to each of these categories in this repository.

The data files are:

*HRI_intent_1_pet.csv, HRI_intent_2_food.csv, HRI_intent_3_job.csv, HRI_intent_4_hobby.csv, HRI_intent_5_sport.csv, HRI_intent_6_drink.csv* 

The file named *HRI_TOTAL_data.csv* contains all of the data found in the 6 files *HRI_intent*.csv* 
## :dizzy: The Data format
We have provided the data in tabular format with two columns. Column 1 contains the **Sentence** while column 2 contains the **Intent_label**. 

<table>
  <tr>
    <th>Sentence</th>
    <th>Intent_label</th>
  </tr>
  <tr>
    <td>Tracey Witch of Ware, was a female English Cocker Spaniel who won the title of Best In Show at Cruft's in both 1948 and 1950.</td>
    <td>pets</td>
  </tr>
  <tr>
    <td>A teller is a person who counts the votes in an election, vote, referendum or poll.</td>
    <td>job</td>
  </tr>
  <tr>
    <td>Kya zan hinga is a grass noodle in chicken consommé dish in Burmese cuisine and it's made with mushrooms, bean, curd skin , lily stems, shrimp, garlic, pepper and sometimes fish balls.</td>
    <td>food</td>
  </tr>
   <tr>
    <td>People who deliberately tan their skin by exposure to the sun engage in a passive recreational activity of sun bathing.</td>
    <td>hobby</td>
   </tr>
  <tr>
    <td>Judo influenced other combat styles such as close quarters combat, mixed martial arts, shoot wrestling and submission wrestling.</td>
    <td>sport</td>
  </tr>
  <tr>
    <td>Hibiscus tea is a herbal tea made as an infusion from crimson or deep magenta colored calyces of the roselle flower.</td>
    <td>drink</td>
  </tr>
</table>

## :mechanical_arm: The Prompts are shown below.
This is an example of one of the prompts which we used.
```
Under construction...
```
The prompt above facilitated our **zero-shot** intent classification analysis.
## :sparkles: Evaluation
```
Under construction...
```
<!-- 
We conducted some preliminary analysis under two settings: (1) zero-shot intent classification (2) few-shot intent classification. In both settings, we curated prompts to accomplish the task. Under few-shot setting, we compared **standard** vs **chain-of-thought (CoT)** prompting. The results are summarized below:
-->
<!-- 
![Results](/images/ZeroshotGPT4.png)

We can deduce that LLMs are capable of zero-shot intent classificaiton. With more advanced prompting techniques, we can signifcicantly improve the accuracy on predicting the intent of any texts. 
-->

## Citation
Please cite as follows
```
Under construction...
```
