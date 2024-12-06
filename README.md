# Large language models (i.e., GPT-4) for Zero-shot Intent Classification in English (En), Japanese (Jp), Swahili (Sw) & Urdu (Ur)

This project explores the potential of deploying large language models (LLMs) such as GPT-4 for `zero-shot intent recognition`. We demonstrate that LLMs can perform intent classification through prompting. This aligns with the ongoing trend of exploiting the power of `in-context learning` in LLMs without the need for extensive fine-tuning. 

To test our hypothesis, we introduce a dataset to explore and analyze zero-shot intent classification further, providing a valuable resource for the research community.

The dataset consists of 8,453 sentences across 6 distinct intent classes: **pet, food, job, hobby, sport, drink**. 

### 🤖 🤖    Human-Robot Interaction (HRI)
We envision a scenario in which the human and the robot engage in discussion over a wide range of topics. For example:

<img src="/images/ICexampleChat.png" width="60%" alt="Results">

From the above illustration, we can deduce that the phrase `Cochinita Pibil for sure!` is related to the `intent` called `food` because the human is answering the question `what's your favorite cuisine?` 

## :card_file_box: The Dataset
In this dataset, we set out to defer from the conventional norm in which intent classification datasets are constructed.
For each sentence in the dataset, only a label identifying the intent label to which the sentence belongs is included. 

**No slot labels are added to the token inside each sentence.**
We aim to investigate if LLMs, such as Llama-2, GPT-4, Claude 3, etc., can correctly distinguish sentences that belong to different intent categories with **in context learning**, i.e., prompting. 
We do not conduct fine-tuning on this dataset. Our target domain is human-robot interaction (HRI).

We considered the following intent categories: pet, food, job, hobby, sport, and drink. 
This repository has one file corresponding to each of these categories.

The data files are provided in two categories.

**Category 1:**
*HRI_intent_1_pet.csv, HRI_intent_2_food.csv, HRI_intent_3_job.csv, HRI_intent_4_hobby.csv, HRI_intent_5_sport.csv, HRI_intent_6_drink.csv* 

The file named *HRI_TOTAL_data.csv* contains all of the data found in the 6 files *HRI_intent_\*.csv* 

**Category 2:**
On top of that, we have provided more specific data files corresponding to `four languages`; English (En), Japanese (Jp), Swahili (Sw), Urdu (Ur), and `six intent classes` such as `IntentRecognitionData_En_Intent_Sports.csv`

Feel free to use whichever data files you are interested in, from the `./data/` folder.
## :dizzy: The Data format
We have provided the data in tabular format with two columns. Column 1 contains the **Sentence** while column 2 contains the **Intent_label**. 

<table>
  <tr>
    <th>Sentence</th>
    <th>Intent_label</th>
  </tr>
  <tr>
    <td>Tracey Witch of Ware, was a female English Cocker Spaniel who won the title of Best In Show at Cruft's in both 1948 and 1950.</td>
    <td>pet</td>
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
Here are the prompts used in the experiments.

#### 1. Zero-shot Standard
This is our standard prompt under zero-shot settings.
```
We want to perform an intent classification task. 
That is, given a sentence, our goal is to predict to which intent class the sentence belongs.
We have 7 intent classes namely: pet, food, job, hobby, sport, drink, other.
Each sentence can only belong to one intent class.

Do not include explanations for the answer. 
Print out only the intent class per sentence. 
Tell me how many predictions you make in total.
```

#### 2. Few-shot Chain-of-Thought (Wei et al.)
This is the few-shot prompting introduced in the paper <b>Chain-of-thought prompting elicits reasoning in large language models</b>.

```
We want to perform an intent classification task. 
That is, given a sentence, our goal is to predict to which intent class the sentence belongs.
We have 7 intent classes namely: pet, food, job, hobby, sport, drink, other.
Each sentence can only belong to one intent class.

The intent classes are described as follows:
pet: this means the sentence contains pets and is talking about pets
food: this means the sentence contains foods and is talking about foods
job: this means the sentence contains jobs and is talking about jobs
hobby: this means the sentence contains hobbies and is talking about hobbies
sport: this means the sentence contains sports and is talking about sports
drink: this means the sentence contains drinks and is talking about drinks
Other: the sentence does not belong to any of the above intent classes

If the sentence belongs to none of the intent classes, that sentence is assigned the intent class "other".
Classify ALL the sentences in column 1 into one of the 7 intent classes namely: pet, food, job, hobby, sport, drink, other. 
Do not include explanations for the answer. 
Print out only the intent class per sentence. 
Tell me how many predictions you make in total.
```

#### 3. Zero-shot Chain-of-Thought (Kojima et al.)
The paper introduced this technique <b>Large language models are zero-shot reasoners</b>.

```
We want to perform an intent classification task. 
That is, given a sentence, our goal is to predict to which intent class the sentence belongs.
We have 7 intent classes namely: pet, food, job, hobby, sport, drink, other.
Each sentence can only belong to one intent class.

Let’s think step by step.

Print out only the intent class per sentence and do not include explanations for the answer.
Tell me how many predictions you make in total.
```

#### 4&5. ExpertPrompting
Our study uses two ExpertPrompting methods: <b>Expert-General</b> and <b>Expert-Specific</b>.
ExpertPrompting was introduced in the paper <b>Expertprompting: Instructing large language models to be distinguished experts</b>.

``` 
[4. Expert-General]

You are an expert that helps people accomplish sophisticated tasks. 
Please follow the provided instructions and answer the question accordingly. 

We want to perform an intent classification task. 
That is, given a sentence, our goal is to predict to which intent class the sentence belongs.
We have 7 intent classes namely: pet, food, job, hobby, sport, drink, other.
Each sentence can only belong to one intent class.
If the sentence belongs to none of the intent classes, that sentence is assigned the intent class "other".

Classify ALL the sentences in column 1 into one of the 7 intent classes namely: pet, food, job, hobby, sport, drink, other. 
Do not include explanations for the answer.  
Each sentence can only belong to one intent class, so carefully analyze the provided information to determine the most accurate and appropriate response. 
Print out only the intent class per sentence. 

Tell me how many predictions you make in total.
Print out the list of answers for downloading. 
```

And...

``` 
[5. Expert-Specific]
As a Social AI Specialist designing a conversational AI for a social robot in a coffee shop setting, analyze user queries to categorize their intent 
into one of seven categories: pet, food, job, hobby, sport, drink, or other. 
Consider the user's query itself, the casual social context, sentence structure (open-ended vs. specific), and any social cues (formality, emojis) to 
identify the main topic (e.g.,  "hey, what are fun puppy tricks?" classified as "pet"). 
Utilize non-verbal cues (if applicable) and past interactions (if any) for a more nuanced understanding. 
Classify any queries not fitting the predefined categories as "other." 

Classify ALL the sentences in column 1 into one of the 7 intent classes namely: pet, food, job, hobby, sport, drink, other. 
Do not include explanations for the answer.  
Each sentence can only belong to one intent class, so carefully analyze the provided information to determine the most accurate and appropriate response. 
Print out only the intent class per sentence. 

Tell me how many predictions you make in total.
Print out the list of answers for downloading. 

```

#### 6. Multi-Persona 
Introduced in the paper <b>Unleashing the emergent cognitive synergy in large language models: A task-solving agent through multi-persona self-collaboration</b>.

```
Multi-Persona Prompting for Intent Classification (7 Classes)
Participants:

AI Assistant (You): A large language model with access to a vast amount of text data and capable of understanding natural language.
Topic Classifier: An NLP specialist focused on identifying the main subject or theme of a user query.
Intent Specialist: An expert in understanding the user's goal or desired outcome within a conversation.
Clarification Specialist: An expert in understanding user intent by asking clarifying questions or analyzing conversational context.
Profiles:

AI Assistant (You): You can process user queries and identify keywords, but may struggle to determine the user's ultimate goal or the specific topic of interest.
Topic Classifier: This persona analyzes the query to identify the main subject matter.
Intent Specialist: This persona analyzes the user's phrasing and context to understand their desired outcome (e.g., information, action, social interaction).
Clarification Specialist: This persona identifies ambiguities and can ask clarifying questions or consider the surrounding conversation to pinpoint user intent.
Task: Analyze the following user query and classify its intent into one of the following categories:

Pet: User query relates to pets (e.g., care, training, adoption)
Food: User query relates to food (e.g., recipes, recommendations, preferences)
Job: User query relates to jobs (e.g., searching, applications, careers)
Hobby: User query relates to hobbies (e.g., finding new hobbies, discussing existing hobbies)
Sport: User query relates to sports (e.g., following teams, playing sports, rules)
Drink: User query relates to drinks (e.g., recipes, recommendations, preferences)
Other: User query doesn't fit neatly into the predefined categories.
Collaboration:

AI Assistant (You): The user asks: "What are some fun tricks I can teach my new puppy?"
Topic Classifier: This query focuses on "puppy" and "tricks," suggesting the topic is pets.
Intent Specialist: The user asks about "teaching tricks," indicating they want information on pet training. Their intent is likely Pet.
Clarification Specialist: While the intent seems clear, we could consider asking, "Are you looking for beginner tricks or more advanced ones?" for further refinement.
AI Assistant (You): Based on the combined analysis, the user's intent is classified as Pet. We can incorporate the suggestion from the Clarification Specialist to tailor the response further.
Final Answer:

"Pet" <<

Explanation:

By collaborating with all four personas, you were able to leverage their expertise and achieve accurate intent classification.  The Topic Classifier identified the main subject as pets.  The Intent Specialist confirmed the user's goal as seeking information related to pet training.  The Clarification Specialist offered an optional step for additional refinement.  This multi-faceted approach ensures a robust intent classification system for your dataset.

Note: Remember to adapt the user query and expected intent category throughout your actual application based on your specific dataset.

Each sentence can only belong to one intent class.
Do not include explanations for the answer. 
Print out only the intent class per sentence. 
Tell me how many predictions you make in total.d
```

The prompts above facilitated our **zero-shot** intent classification analysis.
## :sparkles: Evaluation
We conducted experiments with data sizes per intent class of `200`, `500`, and `all data`. Moreover, we used the three models: `Gemma`, `Claude-3-Opus`, and `GPT-4-turbo`.
<!--
🚧 **Currently under construction....** 🚧
-->
<table>
  <caption>
    <b>1. Standard Prompting results for English (En), Japanese (Jp), Swahili (Sw), Urdu (Ur). </b>
  </caption>
  <thead>
    <tr>
      <th></th>
      <th colspan="4">200 samples</th>
      <th colspan="4">500 samples</th>
      <th colspan="4">All Data</th>
    </tr>
    <tr>
      <th></th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Gemma</td>
      <td> 39 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 44 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 44 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
    </tr>
    <tr>
      <td>Claude 3 Opus</td>
      <td> 63 </td>
      <td> 71 </td>
      <td> 55 </td>
      <td> 78 </td>
      <td> 85 </td>
      <td> 84 </td>
      <td> 87 </td>
      <td> 87 </td>
      <td> 94 </td>
      <td> 92 </td>
      <td> 89 </td>
      <td> 86 </td>
    </tr>
    <tr>
      <td>GPT 4 Turbo</td>
      <td> 96 </td>
      <td> 97 </td>
      <td> 97 </td>
      <td> 92 </td>
      <td> 98 </td>
      <td> 99 </td>
      <td> 98 </td>
      <td> 100 </td>
      <td> 75 </td>
      <td> 82 </td>
      <td> 68 </td>
      <td> 74 </td>
    </tr>
  </tbody>
</table>

<table>
  <caption>
    <b>2. Few-shot Prompting (Wei et al.) results for En, Jp, Sw, Ur. </b>
  </caption>
  <thead>
    <tr>
      <th></th>
      <th colspan="4">200 samples</th>
      <th colspan="4">500 samples</th>
      <th colspan="4">All Data</th>
    </tr>
    <tr>
      <th></th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Gemma</td>
      <td> 49 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 42 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 38 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
    </tr>
    <tr>
      <td>Claude 3 Opus</td>
      <td> 99 </td>
      <td> 96 </td>
      <td> 98 </td>
      <td> 98 </td>
      <td> 94 </td>
      <td> 95 </td>
      <td> 98 </td>
      <td> 96 </td>
      <td> 85 </td>
      <td> 80 </td>
      <td> 88 </td>
      <td> 82 </td>
    </tr>
    <tr>
      <td>GPT 4 Turbo</td>
      <td> 98 </td>
      <td> 97 </td>
      <td> 97 </td>
      <td> 99 </td>
      <td> 95 </td>
      <td> 95 </td>
      <td> 98 </td>
      <td> 91 </td>
      <td> 87 </td>
      <td> 92 </td>
      <td> 79 </td>
      <td> 84 </td>
    </tr>
  </tbody>
</table>

<table>
  <caption>
    <b>3. Zero-shot Prompting (Kojima et al.) results for En, Jp, Sw, Ur. </b>
  </caption>
  <thead>
    <tr>
      <th></th>
      <th colspan="4">200 samples</th>
      <th colspan="4">500 samples</th>
      <th colspan="4">All Data</th>
    </tr>
    <tr>
      <th></th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Gemma</td>
      <td> 65 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 52 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 55 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
    </tr>
    <tr>
      <td>Claude 3 Opus</td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 98 </td>
      <td> 99 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 98 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 96 </td>
      <td> 99 </td>
    </tr>
    <tr>
      <td>GPT 4 Turbo</td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
    </tr>
  </tbody>
</table>

<table>
  <caption>
    <b>4. Expert-general Prompting results for En, Jp, Sw, Ur. </b>
  </caption>
  <thead>
    <tr>
      <th></th>
      <th colspan="4">200 samples</th>
      <th colspan="4">500 samples</th>
      <th colspan="4">All Data</th>
    </tr>
    <tr>
      <th></th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Gemma</td>
      <td> 77 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 61 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 59 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
    </tr>
    <tr>
      <td>Claude 3 Opus</td>
      <td> 99 </td>
      <td> 96 </td>
      <td> 99 </td>
      <td> 99 </td>
      <td> 91 </td>
      <td> 96 </td>
      <td> 97 </td>
      <td> 89 </td>
      <td> 94 </td>
      <td> 93 </td>
      <td> 94 </td>
      <td> 96 </td>
    </tr>
    <tr>
      <td>GPT 4 Turbo</td>
      <td> 100 </td>
      <td> 99 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 100 </td>
      <td> 93 </td>
      <td> 97 </td>
      <td> 96 </td>
      <td> 85 </td>
      <td> 93 </td>
      <td> 96 </td>
      <td> 98 </td>
    </tr>
  </tbody>
</table>

<table>
  <caption>
    <b>5. Expert-specific Prompting results for En, Jp, Sw, Ur. </b>
  </caption>
  <thead>
    <tr>
      <th></th>
      <th colspan="4">200 samples</th>
      <th colspan="4">500 samples</th>
      <th colspan="4">All Data</th>
    </tr>
    <tr>
      <th></th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Gemma</td>
      <td> 68 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 71 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 48 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
    </tr>
    <tr>
      <td>Claude 3 Opus</td>
      <td> 99 </td>
      <td> 95 </td>
      <td> 95 </td>
      <td> 96 </td>
      <td> 97 </td>
      <td> 95 </td>
      <td> 94 </td>
      <td> 97 </td>
      <td> 92 </td>
      <td> 93 </td>
      <td> 95 </td>
      <td> 97 </td>
    </tr>
    <tr>
      <td>GPT 4 Turbo</td>
      <td> 98 </td>
      <td> 97 </td>
      <td> 99 </td>
      <td> 99 </td>
      <td> 99 </td>
      <td> 98 </td>
      <td> 96 </td>
      <td> 97 </td>
      <td> 94 </td>
      <td> 96 </td>
      <td> 93 </td>
      <td> 95 </td>
    </tr>
  </tbody>
</table>

<table>
  <caption>
    <b>6. Multi-persona Prompting results for En, Jp, Sw, Ur. </b>
  </caption>
  <thead>
    <tr>
      <th></th>
      <th colspan="4">200 samples</th>
      <th colspan="4">500 samples</th>
      <th colspan="4">All Data</th>
    </tr>
    <tr>
      <th></th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
      <th>En</th>
      <th>Jp</th>
      <th>Sw</th>
      <th>Ur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Gemma</td>
      <td> 76 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 62 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> 55 </td>
      <td> n/a </td>
      <td> n/a </td>
      <td> n/a </td>
    </tr>
    <tr>
      <td>Claude 3 Opus</td>
      <td> 100 </td>
      <td> 97 </td>
      <td> 98 </td>
      <td> 99 </td>
      <td> 100 </td>
      <td> 95 </td>
      <td> 96 </td>
      <td> 99 </td>
      <td> 100 </td>
      <td> 95 </td>
      <td> 96 </td>
      <td> 97 </td>
    </tr>
    <tr>
      <td>GPT 4 Turbo</td>
      <td> 99 </td>
      <td> 97 </td>
      <td> 92 </td>
      <td> 99 </td>
      <td> 99 </td>
      <td> 99 </td>
      <td> 98 </td>
      <td> 91 </td>
      <td> 100 </td>
      <td> 95 </td>
      <td> 97 </td>
      <td> 92 </td>
    </tr>
  </tbody>
</table>

<!-- 
We conducted some preliminary analysis under two settings: (1) zero-shot intent classification (2) few-shot intent classification. In both settings, we curated prompts to accomplish the task. Under few-shot setting, we compared **standard** vs **chain-of-thought (CoT)** prompting. The results are summarized below:
-->
<!-- 
![Results](/images/ZeroshotGPT4.png)

We can deduce that LLMs are capable of zero-shot intent classification. With more advanced prompting techniques, we can significantly improve the accuracy of predicting the intent of any text. 
-->

## Citation

Please cite as follows
```bibtex
        @inproceedings{inproceedings,
        author = {Atuhurra, Jesse},
        year = {2024},
        month = {06},
        title = {Zero-shot Retrieval of User Intent in Human-Robot Interaction with Large Language Models}
    }
