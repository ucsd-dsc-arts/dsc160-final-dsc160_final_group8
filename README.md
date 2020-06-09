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

The concept for our generative art project is to look into various speeches and addresses, both verbally and written, given by presidents of the United States of America in order to generate speeches that will be based off of an inputted keyword. We plan on using OpenAI's GPT-2 text models in order to generate our text. For our training data, we will use data from presidential speeches. We hope that our system will produce speeches that, from inputted keywords, produce speeches that can mimic diplomatic and political language while being based around the keywords. Our output will be presented by the model in text form, and we hope to present some examples in a creative manner such as spoken form. 

The first matter on the table is the pre-processing of this data. For this matter, we hope to employ the sk-learn's n-grams and POS Taggers to determine and classify words of interest. From then on, we will use an RNN much like Stanford's char-rnn (https://github.com/karpathy/char-rnn) to generate the text based on given keywords. We can also use latent Dirichlet allocation along the lines of Valentin Kassarnig to better judge what groups of words belong to certain topics. The final matter of concern is the training of our AI. We plan to use an AWS' EC2 compute instances to cost-effectively train our model.

Some challenges we believe may be faced can be thematic issues in produced speeches, which we believe may come up due to models potentially not understanding the meanings of the words it is putting into its output. Also, broad and non-specific keywords may produce speeches that might not have any direction. We will be expanding upon concepts covered in the class such as generative art text, as seen in Lecture 9, utilizing generative systems. We find this interesting personally, culturally, and politically. It will be interesting to see how different keywords yield different word choices used in the outputs and whether certain keyword inputs relate to certain time periods and therefore certain language choices. It will also be interesting politically to see the word choices of heads of states and to see what sorts of language are common amongst all the different speeches within the dataset. 

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
The code for preprocessing/generating training data from the kaggle dataset and the training/generating process is [here](./code/gpt2.ipynb).
As mentioned above, the dataset for the presidential speeches was initially taken from Kaggle. The speeches in the dataset are then isolated out and stored in individual txt files for the gpt2 models to be trained on. For each training set, the model is training with maximum of 750 steps and with other hyperparameters set as default. The training time ended up taking quite a while, some methods of early stop can be considered using to minimize training time. 

Link each of these items to your .ipynb or .py files within this seection, and provide a brief explanation of what the code does. Reading this section we should have a sense of how to run your code.

## Results

(30 points) 

This section should summarize your results and will embed links to documentation to significant outputs. This should document both process and show artistic results. This can include figures, sound files, videos, bitmaps, as appropriate to your generative art idea. Each result should include a brief textual description, and all should be listed below: 

- The output of the simulated speech given the prompt "My fellow americans, " is recorded in this [document](https://docs.google.com/document/d/1uqdmB1EyV2X_JCb5v0Z3M82cty0TxXzsgPxfxc4jo1A/edit?fbclid=IwAR0N-LUlHdfOig7Aq7d_p-YvIjDx8gMfolDy_T81vC6VhYkjuGTkKOEAtnY).


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
