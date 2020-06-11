# Project Title

DSC160 Data Science and the Arts - Final Project - Generative Arts - Spring 2020

Project Team Members: 
- Rakesh Senthilvelan, rsenthil@ucsd.edu
- Mizuki Kadowaki, mikadowa@ucsd.edu
- Anurag Pamuru, anpamuru@ucsd.edu
- Praveen Nair, prnair@ucsd.edu
- Shutong Li, shl636@ucsd.edu

## Abstract

(10 points) 

For the project proposal, please write a short abstact addressing the questions below. You need to replace the entire contents of this section with one to two paragraphs addressing the following:

- What is your concept for a generative art project?
- What methods/networks/techniques will you employ (include links to technical precedents/code bases)
- What training data (if any) will you use for your project?
- What kind of results do you hope that your system will produce?
- How will you present your result/what form will your output take?
- What if any challenges to you think may arise as you are working with this?
- How are you expanding on topics we have covered in class?
- Why is it interesting? (personally, culturally, politically, other)
- List three papers / art projects that are references for this work.

The concept for our generative art project is to simulate every president's attitude and ideology through mimicking their speech so that we can explore concepts such as the interaction between one president's narrative and another as well as what constitutes the core essence of a president's speech. The technical aspects required towards realizing this idea is looking into various speeches and addresses, both verbally and written, given by presidents of the United States of America in order to generate speeches that will be based off of specified inputted keyword. The model we will be using for text generation is OpenAI's GPT-2 text models. We will train one model per president based on the collection of speeches of that corresponding president. By testing the output of every president model under one unanimous prefix, we find out that the model is exceptional at capturing the rhetorics as well as the ideology from the presidents. 

With the trained models we will be able to explore the concepts mentioned above. To examine the interaction between different narratives we wouuld prefix the output of the speech model for one president with speeches of another; To examine the essence of a president's speech, we would increase temperature to see what aspect of the speech is first lost during the increase of the originality of the speech. 

Below are some of the papers and art projects we used as references for this work:
- Political Speech Generation by Valentin Kassarnig

https://arxiv.org/abs/1601.03313

https://github.com/valentin012/conspeech

- Obama RNN by samim

https://medium.com/@samim/obama-rnn-machine-generated-political-speeches-c8abd18a2ea0

https://github.com/samim23/obama-rnn/

- Automated Speech Generation from UN General Assembly Statements: Mapping Risks in AI Generated Texts by Joseph Bullock and Miguel Luengo-Oroz

https://arxiv.org/pdf/1906.01946.pdf

## Data and Model

(10 points) 

We will be using the gpt2-small model (the one with 124M parameters) to finetune a model for every president based on the speeches they made. After training we would let every model generate a passage following the given prompt "My fellow americans". 
- gpt2 Model
  - [code](https://github.com/openai/gpt-2)
  - [More about gpt2 model from OpenAI](https://openai.com/blog/better-language-models/). 
- Dataset description 
  - The dataset comes from kaggle ([link here](https://www.kaggle.com/littleotter/united-states-presidential-speeches?select=sixth_party_corpus.csv&fbclid=IwAR2Wl6dWgOppG3TRBsktnf62jwkEmjzBl57NUj3rPnVsr77LZ5MInSCJrbI)). The dataset is a condensed collection of all the presidential speeches made by every president. The dataset was initially scraped from [here](https://millercenter.org/the-presidency/presidential-speeches)

## Code

(20 points)
The code for preprocessing/generating training data from the kaggle dataset and the training/generating process is [here](./code/gpt2.ipynb) or [here](./code/speech_sim.ipynb). Both notebook incorporate all the preprocessing/training/generating in one file. The former contains text generation for all presidents under the unanimous prompt of "My fellow Americans", the latter contains the experiment of exploring Trump's rhetorics in his speeches, including letting other presidents finish speeches that are started by Trump and tuning the temperature model . 
As mentioned above, the dataset for the presidential speeches was initially taken from Kaggle. The speeches in the dataset are then isolated out and stored in individual txt files for doing transfer-learning on the gpt2 model. For each training set, a fresh model is trained with maximum of 750 steps and with other hyperparameters set as default. Even though increasing batch_size is considered to increase training efficiency, the idea is eventually given up when leveraged against VRAM usage(discussed in the following paragraph). 
The training time for one model under CPU-support ended up taking quite a while. The runtime concern is exacerbated by the fact that we have to train **44** gpt2 models altogether, each for one president. Utilizing tf-gpu speeds up the process considerably but requires large VRAMS, therefore we have to rely on datahub to process the workload. Leveraging training time with training efficacy, we used the minimal amount of batch-size and trains under GPU support.  

Link each of these items to your .ipynb or .py files within this seection, and provide a brief explanation of what the code does. Reading this section we should have a sense of how to run your code.

## Results

(30 points) 

This section should summarize your results and will embed links to documentation to significant outputs. This should document both process and show artistic results. This can include figures, sound files, videos, bitmaps, as appropriate to your generative art idea. Each result should include a brief textual description, and all should be listed below: 

- The output of the simulated speech given the prompt "My fellow americans, " is recorded in this [document](https://docs.google.com/document/d/1uqdmB1EyV2X_JCb5v0Z3M82cty0TxXzsgPxfxc4jo1A/edit?fbclid=IwAR0N-LUlHdfOig7Aq7d_p-YvIjDx8gMfolDy_T81vC6VhYkjuGTkKOEAtnY). The outcome is impressive, every speech looks reasonable and authentic.
- The output of the speeches given


## Discussion

(30 points, three to five paragraphs)

The outputs captures the rhetorics of each presidents extremely well. For instance, Trump's speech consists of unassuming wording and structure as well as his iconic MAGA phrase; Obama's speech mimics his crips speech structure with the strong and effective repetition. In addition, the semantics are well-captured as well. Trump and Obama again are the two good examples. The simulated speech from the former promotes strong nationalism and almost militarism while the one from the latter promotes general welfare for the country. In short, the simulated speeches understands the rough ideology behind each president. Aside from the capture of the semantics and the rhetorics, the interesting thing is that the historical period in which each president makes their speech largely defines the tone and the subcontext of each simulated speech. 


The subsequent paragraphs could address questions including:
- Why is this culturally innovative?
- How does your generative computational approach differ from traditional art/music/cultural production? 
- How do your results relate to broader social, cultural, economic political, etc., issues? 
- What are the ethical concerns for this form of generative art? 
- In what future directions could you expand this work?

## Team Roles

Provide an account of individual members and their efforts/contributions to the specific tasks you accomplished.

Rakesh - Abstract
Anurag - Abstract

## Technical Notes and Dependencies

Any implementation details or notes we need to repeat your work. 
- Additional libraries you are using for this project
- Does this code require other pip packages, software, etc?
- Does this code need to run on some other (non-datahub) platform? (CoLab, etc.)

## Reference

All references to papers, techniques, previous work, repositories you used should be collected at the bottom:
- Papers
- Repositories
- Blog posts
