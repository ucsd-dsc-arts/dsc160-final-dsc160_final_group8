# Presidential Speechwriting with GPT-2

DSC160 Data Science and the Arts - Final Project - Generative Arts - Spring 2020

Project Team Members: 
- Rakesh Senthilvelan, rsenthil@ucsd.edu
- Mizuki Kadowaki, mikadowa@ucsd.edu
- Anurag Pamuru, anpamuru@ucsd.edu
- Praveen Nair, prnair@ucsd.edu
- Shutong Li, shl636@ucsd.edu

## Abstract

(10 points) 

For the project proposal, please write a short abstract addressing the questions below. You need to replace the entire contents of this section with one to two paragraphs addressing the following:

- What is your concept for a generative art project?
- What methods/networks/techniques will you employ (include links to technical precedents/code bases)
- What training data (if any) will you use for your project?
- What kind of results do you hope that your system will produce?
- How will you present your result/what form will your output take?
- What if any challenges to you think may arise as you are working with this?
- How are you expanding on topics we have covered in class?
- Why is it interesting? (personally, culturally, politically, other)
- List three papers / art projects that are references for this work.

The concept for our generative art project is to look into various speeches and addresses, both verbally and written, given by different presidents of the United States of America in order to generate speeches that will be based off of an inputted keyword or phrase. We plan on using OpenAI's GPT-2 text models in order to generate our text. We will be training different models for a few select presidents who we consider to stand out in terms of their speech. For our training data, we will use data from presidential speeches. We will train 124M models, which are named to represent the number of parameters used in the model, on speeches given by selected preisdents, training a model to each president. From here, we will use the GPT-2 model along with inputted prefixes such as phrases, sentences, or paragraphs in order to see how each president would complete a certain speech based on its intro. We hope that our system will produce speeches that, from inputted keywords, produce speeches that can mimic diplomatic and political language while being based around the keywords. We hope to be able to compare how different presidents will produce speeches and each of the models will be able to embody the speech style of a certain president. Our output will be presented by the model in text form, and we hope to present some examples in a creative manner such as spoken form. 


Some challenges we believe may be faced can be thematic issues in produced speeches, which we believe may come up due to models potentially not understanding the meanings of the words it is putting into its output. Also, broad and non-specific keywords may produce speeches that might not have any direction. We will be expanding upon concepts covered in the class such as generative art text, as seen in Lecture 9, utilizing generative systems. We find this interesting culturally, and politically, since it reflects trends in presidents' political speech over time and between varying kinds of administration. It will be interesting to see how different keywords yield different word choices used in the outputs and whether certain keyword inputs relate to certain time periods and therefore certain language choices. It will also be interesting politically to see the word choices of heads of states and to see what sorts of language are common amongst all the different speeches within the dataset. 

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

The dataset comes from Kaggle, as uploaded by Joseph Lilleberg. ([link here](https://www.kaggle.com/littleotter/united-states-presidential-speeches?select=corpus.csv)). The dataset was initially scraped from [the Miller Center of Public Affairs at the University of Virginia](https://millercenter.org/the-presidency/presidential-speeches), which maintains transcripts of notable speeches from every American president to date. For obvious reasons, such as differences in presidency length and the smaller number of remaining speeches from early presidents, the amount of data for each president varies.

We will be using OpenAI's gpt2-small model (the one with 124M parameters) to finetune a model for every president based on the speeches they made. The gpt2 model code can be found [here](https://github.com/openai/gpt-2), and an article explaining its origins and implementation [is here](https://openai.com/blog/better-language-models/). The model is trained on 40 GB of Internet text using 8 million webpages linked from Reddit, yielding a model with (in the most advanced implementation) 1.5 billion parameters. Most importantly, we have the tools available to finetune the GPT-2 models in order to make them resemble input sample text. In order to work more easily with the model, we used Max Woolf's [gpt-2-simple Python package](https://github.com/minimaxir/gpt-2-simple), which implements many of the functions necessary to do text generation using GPT-2 models.

## Code

(20 points)

The majority of the code for this project was run on UCSD's [Datahub platform](https://datahub.ucsd.edu), due to the availability of CPU, RAM, and especially GPU resources that are largely unavailable to most users. This does mean that folder and file references might not be consistent between notebooks, since they were run on personal instances of the Datahub.
The code for preprocessing the presidential speech data from the kaggle dataset, training the model, and generating samples process is [here](./code/gpt2.ipynb). In this notebook, the cells for training and generating data were run repeatedly on different data/different models, which is why the notebook is so short. This is because, unfortunately, the Python session needs to be restarted in order to train a new model or generate a new text sample, so there is no use to doing this process iteratively or in order, As mentioned above, the dataset for the presidential speeches was initially taken from Kaggle. The speeches in the dataset are then isolated out and stored in individual txt files for the gpt2 models to be trained on. For each training set, the model is trained with 750 steps and with other hyperparameters set as default. Even with the ample resources and GPU clusters provided by Datahub, the training process of the model took around 20 minutes on average (this means it's probably not the best idea to run these notebooks); text generation, on the other hand, only took a couple dozen seconds or so for short samples.
We trained models for thirteen presidents that we considered most notable either for their historical importance or recency:

- George Washington
- Thomas Jefferson
- Andrew Jackson
- Abraham Lincoln
- Theodore Roosevelt
- Franklin D. Roosevelt
- John F. Kennedy
- Richard Nixon
- Ronald Reagan
- Bill Clinton
- George W. Bush
- Barack Obama
- Donald Trump

Using the text files we extracted from the dataset, we trained models on the speeches of these presidents to create a GPT-2 model for each. Each 124M GPT-2 model, due to the massive number of parameters, is 500MB, meaning that it is very expensive to transfer them (and impossible to host them normally on Github).

## Results

(30 points) 

This section should summarize your results and will embed links to documentation to significant outputs. This should document both process and show artistic results. This can include figures, sound files, videos, bitmaps, as appropriate to your generative art idea. Each result should include a brief textual description, and all should be listed below: 

Although there are a multitude of ways in which one could generate results from this data, one approach we used was to create a joint speech from all of the above presidents in chronological order, seeded with the prefix text of "My fellow Americans," a traditional beginning for a presidential speech. We passed this prefix into the model for George Washington, then using the generated text from that model, we passed the entire speech to that point into the next model, and so on. In other words, each generated sample of text was seeded with the statements of all previous statements as a prefix. Although most of the time, we just selected the first output that the model generated, in a few instances where there was excessive repetition or where the text was not at all coherent, we reran the model to get more understandable results -- but on the most part the speech still represents the model's first try. There are still slight issues with repetition (as you can see in the text from Trump and Obama), but for the most part it is logically coherent and seems like it could be a real, abeit disjointed, presidential speech. You can read the generated speech [here](https://docs.google.com/document/d/1uqdmB1EyV2X_JCb5v0Z3M82cty0TxXzsgPxfxc4jo1A/edit?fbclid=IwAR0N-LUlHdfOig7Aq7d_p-YvIjDx8gMfolDy_T81vC6VhYkjuGTkKOEAtnY).

In addition, in the [/results/samples](https://github.com/ucsd-dsc-arts/dsc160-final-dsc160_final_group8/tree/master/results/samples) folder, we have included the successive samples at each 100th training step milestone that gpt-2-simple automatically outputs. Here, you can see random (unseeded) text from the models of each president at different stages of training. 

## Discussion

(30 points, three to five paragraphs)

The outputs capture the rhetoric of each president fairly well. For instance, President Trump's speech consists of fairly simple wording about American exceptionalism and military supremacy as well as his iconic "Make America Great Again" catchphrase; President Obama's speech mimics his more professional speech structure with repetition. Meanwhile, earlier presidents produce more formal language, as was common in political speeches of the time. In addition, the content of the speeches reflects what we'd expect from these presidents fairly well. Once again, we can look to  Trump and Obama for examples. The simulated speech from Trump promotes strong nationalism, American exceptionalism, and militarism, while the one from the latter promotes international trade, multilateralism, and the rhetoric of recovery from the Great Recession that President Obama sought to highlight. There are other examples: we see Franklin Roosevelt, widely considered the most economically progressive president in American history, mention labor issues; we see John F. Kennedy mention anti-poverty programs, which he and his successor Lyndon B. Johnson introduced in the 1960s; we also see George W. Bush, a pro-business president who instituted widespread tax cuts, mention the economy and consumer behavior as vital to American security and welfare. In short, the simulated speeches seem to track the rough ideology behind each president, even in these short samples. Aside from the capture of the semantics and the rhetorics, the interesting thing is that the historical period in which each president makes their speech largely defines the tone and the subcontext of each simulated speech. 

The ethical concerns behind this project, relative to many other generative data forms trained on political figures, are fairly low. However, we could still imagine an instance where someone might train a GPT-2 model on President Trump or his challenger, Joe Biden, and manipulating our knowledge of both men's speaking patterns in order to convince the public that a statement came from them. Of course, such a claim could be easily fact-checked, but the rapid speed of the spread of false information that social media has enabled will mean that many people, especially those with existing grudges against either politician, might believe that the statement was genuine. But it's hard to see this being a very popular vector for misinformation, as it is harder to get people to believe that someone said a given text statement than it is to get them to believe an image, audio sample, or video is genuine; these other, audiovisual forms of data are likely far better methods for misinformation (and, at a glance, far more common.) [In the release of their 1.5-billion parameter model](https://openai.com/blog/gpt-2-1-5b-release/), OpenAI did indicate that GPT-2 could theoretically be used for the creation of political propaganda, citing a study where the model was able to synthetically generate propaganda for white supremacy, Marxism, jihadist Islamism, and anarchism, with detection of fakes being fairly difficult. But the same blog post indicates that the misuse of the model has been rare since the initial release of GPT-2. This is likely because rapidly generating political text is not very useful for misinformation or propaganda campaigns, as targeted misinformation by human writers that plays on current events and confirmation bias is, for now, a much more effective method.

One way we might expand on this project is to generate more context-sensitive text by selecting specific types of speeches to train on. In this project, we just threw all of a president's speeches from the Miller Center into the model. But in theory, we could instead have separated the models based on specific types of speech -- State of the Union, National Prayer Breakfast, inaugural addresses, and so on. In this way, we might be able to match the differences in speaking style that speeches at these different events might contain, making even more convincing versions of real speeches.

The subsequent paragraphs could address questions including:
- Why is this culturally innovative?
- How does your generative computational approach differ from traditional art/music/cultural production? 
- How do your results relate to broader social, cultural, economic political, etc., issues? 
- What are the ethical concerns for this form of generative art? 
- In what future directions could you expand this work?

## Team Roles

Provide an account of individual members and their efforts/contributions to the specific tasks you accomplished.

Rakesh - Abstract, write-up, presentation

Anurag - Abstract
Praveen - Trained presidential models, generated joint presidential speech
Mizuki - Write up, presentation
Shutong - 



Praveen - Trained presidential models, generated joint presidential speech

## Technical Notes and Dependencies

Any implementation details or notes we need to repeat your work. 
- Additional libraries you are using for this project
- Does this code require other pip packages, software, etc?
- Does this code need to run on some other (non-datahub) platform? (CoLab, etc.)

We used [Max Woolf's gpt-2-simple Python package](https://github.com/minimaxir/gpt-2-simple) as the basis for this project, which itself uses tensorflow, regex, requests, tqdm, numpy, and toposort. We also used pandas and os for small tasks to extract the data. The code all runs on Datahub, by far most efficiently on GPU-enabled servers.
## Reference

All references to papers, techniques, previous work, repositories you used should be collected at the bottom:
- [GPT-2 explanation](https://openai.com/blog/better-language-models/) and [code](https://github.com/openai/gpt-2)
- [gpt-2-simple](https://github.com/minimaxir/gpt-2-simple)
