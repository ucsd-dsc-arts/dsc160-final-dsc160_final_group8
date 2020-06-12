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

Every president in the US history has their own distinct ideology and personality, evident from and propagated through their rhetoric and styles in their presidential speeches. The concepts for our generative art project are 1) to experiment with fusing various narratives of presidents into making one coherent but relatively contextless speech, 2) to explore what happens when we force a narrative of a previous president into a distinct context of contemporary social-political matters, and 3) analyze what constitutes as the essence of the characteristics of a president's speech. To realize concept 1 we created a joint speech where we started off with a generic and contextless prefix, and then input into every model successively, ordered by their corresponding presidents chronologically, the joined output of the previous model. To realize concept 2 we aim to let multiple previous presidents finish a speech started by Donald Trump. For concept 3 - focusing our experiment on Trump alone - we decided to gradually increase the temperature of a generated text under a fixed prompt of what Trump once said and see what is the last to be lost before the text devolves into non-sensical gibberish. We plan on using OpenAI's GPT-2 text models in order to generate our text. We will be training different models for a few select presidents who we consider to stand out in terms of their speech. For our training data, we will use data from presidential speeches. We will train 124M models, which are named to represent the number of parameters used in the model, on speeches given by selected preisdents, training a model to each president. From here, we will use the GPT-2 model along with inputted prefixes such as phrases, sentences, or paragraphs in order to see how each president would complete a certain speech based on its intro. We hope that our system will produce speeches that, from inputted keywords, produce speeches that can mimic diplomatic and political language while being based around the keywords. We hope to be able to compare how different presidents will produce speeches and each of the models will be able to embody the speech style of a certain president. Our output will be presented by the model in text form, and we hope to present some examples in a creative manner such as spoken form. 

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

The dataset comes from Kaggle, as created and uploaded by Joseph Lilleberg. ([link here](https://www.kaggle.com/littleotter/united-states-presidential-speeches?select=corpus.csv)). The dataset was initially scraped from [the Miller Center of Public Affairs at the University of Virginia](https://millercenter.org/the-presidency/presidential-speeches), which maintains transcripts of notable speeches from every American president to date. For obvious reasons, such as differences in presidency length and the smaller number of remaining speeches from early presidents, the amount of data for each president varies.

We will be using OpenAI's gpt2-small model (the one with 124M parameters) to finetune a model for every president based on the speeches they made. The gpt2 model code can be found [here](https://github.com/openai/gpt-2), and an article explaining its origins and implementation [is here](https://openai.com/blog/better-language-models/). The model is trained on 40 GB of Internet text using 8 million webpages linked from Reddit, yielding a model with (in the most advanced implementation) 1.5 billion parameters. Most importantly, we have the tools available to finetune the GPT-2 models in order to make them resemble input sample text. In order to work more easily with the model, we used Max Woolf's [gpt-2-simple Python package](https://github.com/minimaxir/gpt-2-simple), which implements many of the functions necessary to do text generation using GPT-2 models.

## Code

(20 points)

The code for preprocessing the presidential speech data from the kaggle dataset, training the model, and generating text is present in both the notebook for [narrative fusion](./code/gpt2.ipynb) and the one for [forcing narratives and speech essence analysis](./code/speech_sim.ipynb).  The former deals with concept 1 in the abstract while the latter deals with concept 2 and 3. As mentioned above, the dataset for the presidential speeches was initially taken from Kaggle. The speeches in the dataset are then isolated out and stored in individual .txt files to provide fine-tuning on the gpt2 model. For each text file, a fresh model is trained with maximum of 750 steps and with other hyperparameters set as default. Even though increasing batch_size is considered to increase training efficiency, the idea is eventually given up when leveraged against VRAM usage when training with GPU. While training with CPU does not have such concern, the training time for one model under CPU-support ended up taking hours on end. Considering we many models to train, runtime speedup is extremely precious to us. Therefore we decides to use tf-gpu to speed up the training process despite the memory limitation that prevents us from optimizing training result.

The specific presidents chosen to have gpt2 models finetuned over their speeches are:

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

These presidents are considered either for their historical importance or recency.


## Results

(30 points) 

- The output of the joint simulated speech given the prompt "My fellow americans, " is recorded in this [document](https://docs.google.com/document/d/1uqdmB1EyV2X_JCb5v0Z3M82cty0TxXzsgPxfxc4jo1A/edit?fbclid=IwAR0N-LUlHdfOig7Aq7d_p-YvIjDx8gMfolDy_T81vC6VhYkjuGTkKOEAtnY). Most of the time, we just selected the first output that the model generated unless under rare occasions the sampled text suffers from extreme lack of coherency due to errors such as encoding problems, over-repetition of phrases etc, in which case we simply re-run the model to generate a different sample. The generated speeches are mostly logically coherent *within each president's section* and seems like it could be a real, abeit disjointed, presidential speech. You can read the generated speech [here](https://docs.google.com/document/d/1uqdmB1EyV2X_JCb5v0Z3M82cty0TxXzsgPxfxc4jo1A/edit?fbclid=IwAR0N-LUlHdfOig7Aq7d_p-YvIjDx8gMfolDy_T81vC6VhYkjuGTkKOEAtnY).

- The output of the integrate narrative, namely having Trump's speech finished in the style of other presidents is documented [here](https://docs.google.com/document/d/18HwZG9Am-g-p1L4gTJs10BPZwvPtNSPnSR_GMh6OOpA/edit). We can see that the further back time in history that we are deploying as the style for the text generation, the more incoherent it gets with respect to the original.

- The output of Trump's simulated speech under increasing temperature is documented [here](https://docs.google.com/document/d/1t1U0tmrGFVRuhYkrHydbMnJAXf4kjhEed2wcpBzog7o/edit). The prefix was an excerpt from Trump's 2017 inaugural address. The increasing temperature appear to blur the context of the speech but the nationalist sentiment in the speeches never seem to dwindle. 

In addition, in the [/results/samples](./results/samples) folder, we have included the successive samples at each 100th training step milestone that gpt-2-simple automatically outputs. Here, you can see random (unseeded) text from the models of each president at different stages of training. 

## Discussion

(30 points, three to five paragraphs)

The outputs of the jointed presidential speech capture the rhetoric of each president fairly well. For instance, President Trump's speech consists of fairly simple wording about American exceptionalism and military supremacy as well as his iconic "Make America Great Again" catchphrase; President Obama's speech mimics his more professional speech structure with repetition. Meanwhile, earlier presidents produce more formal language, as was common in political speeches of the time. In addition, the content of the speeches reflects what we'd expect from these presidents fairly well. Once again, we can look to  Trump and Obama for examples. The simulated speech from Trump promotes strong nationalism, American exceptionalism, and militarism, while the one from the latter promotes international trade, multilateralism, and the rhetoric of recovery from the Great Recession that President Obama sought to highlight. There are other examples: we see Franklin Roosevelt, widely considered the most economically progressive president in American history, mention labor issues; we see John F. Kennedy mention anti-poverty programs, which he and his successor Lyndon B. Johnson introduced in the 1960s; we also see George W. Bush, a pro-business president who instituted widespread tax cuts, mention the economy and consumer behavior as vital to American security and welfare. In short, the simulated speeches seem to track the rough ideology behind each president, even in these short samples. However, the joint speech suffers from an incoherent context across presidents. 

Regarding outputs for concept 2, we utilizes President Trump's comment on the nation-wide protests on George Floyd's death. Trump in his original speech uses the selected quote as a reasoning behind his stance against the protestors. However, using the selected quote as a prefix for generating speeches using other presidents' styles, we somewhat bring in previous presidents' perspectives on the similar events and issues in their own times. The generated text under Obama serves as a good example as the stance towards the protests, both peaceful and violent alike, similar to what he might have said in real life (being cautious but tolerant). Another thing to note is that the perspective from presidents further back into the past seem to be much less relevant, this is probably due to the fact that different eras give drastically different context in their speech, rendering the generated text seemingly out of place.

For outputs for conecpt 3, we see that despite the generated Trump speeches losing semantic meaningfulness as temperature increases, the nationalist sentiment and the notion of exceptionalism persists until the temperature goes way beyond a reasonable threshold (>= 1.8). At temperature = 1.7 the generated text still contains phrases like "I want America to be admired by all races, creeds and creeds of the earth." We believe that since the exceptionalist sentiment is the last visible trace of Trump's characteristics during the increase of temperature, this aspect might be considered the most defining feature of Trump's speeches. 

The generative nature of this project means that it differs from most examinations of presidential speech, quantitative or qualitative, since those tend to be mostly descriptive rather than productive. But at the same time, the result of training a text model on a president is also descriptive in that it tells us something about the way that that president speaks, and removing those speeches from context and using new parameters and prefixes allow us to, in a more understandable way, understand the form of presidential speech. We believe this project has cultural value because it allows us to interact with presidential speeches in a new way, especially for presidents who we have never seen speak in videos or on television. Although these models shouldn't be used to tell us what previous presidents would have thought about modern political issues, they can show us the ways in which they made certain political statements so that we can understand why presidents we've never seen speak were considered great orators. The project also has some political relevancy, as many people in recent years have bemoaned a perceived coarsening of political discourse, with less poetic prose and more apparently vulgar content. The presidential speech models that this project examines could theoretically be used to make this case; but there's an equal argument to be made that presidential speech is getting easier to understand and more like everyday speech, especially as the electorate has grown from the landed, wealthy elite in George Washington's presidency to the universal suffrage we have today.

The ethical concerns behind this project, relative to many other generative data forms trained on political figures, are fairly low. However, we could still imagine an instance where someone might train a GPT-2 model on President Trump or his challenger, Joe Biden, and manipulating our knowledge of both men's speaking patterns in order to convince the public that a statement came from them. Of course, such a claim could be easily fact-checked, but the rapid speed of the spread of false information that social media has enabled will mean that many people, especially those with existing grudges against either politician, might believe that the statement was genuine. But it's hard to see this being a very popular vector for misinformation, as it is harder to get people to believe that someone said a given text statement than it is to get them to believe an image, audio sample, or video is genuine; these other, audiovisual forms of data are likely far better methods for misinformation (and, at a glance, far more common.) [In the release of their 1.5-billion parameter model](https://openai.com/blog/gpt-2-1-5b-release/), OpenAI did indicate that GPT-2 could theoretically be used for the creation of political propaganda, citing a study where the model was able to synthetically generate propaganda for white supremacy, Marxism, jihadist Islamism, and anarchism, with detection of fakes being fairly difficult. But the same blog post indicates that the misuse of the model has been rare since the initial release of GPT-2. This is likely because rapidly generating political text is not very useful for misinformation or propaganda campaigns, as targeted misinformation by human writers that plays on current events and confirmation bias is, for now, a much more effective method.

One way we might expand on this project is to generate more context-sensitive text by selecting specific types of speeches to train on. In this project, we just threw all of a president's speeches from the Miller Center into the model. But in theory, we could instead have separated the models based on specific types of speech -- State of the Union, National Prayer Breakfast, inaugural addresses, and so on. In this way, we might be able to match the differences in speaking style that speeches at these different events might contain, making even more convincing versions of real speeches. One could also combine this project with a speech synthesis model trained on any of the presidents with enough available audio samples in order to create a genuine-sounding audio speech, which would be a more engaging way of utilizing our text models. 

## Team Roles

Provide an account of individual members and their efforts/contributions to the specific tasks you accomplished.

Rakesh - Abstract, write-up, presentation

Anurag - Abstract

Praveen - Trained presidential models, generated joint presidential speech

Mizuki - Write up, presentation

Shutong - Write up, experiment of forcing narrative and analyzing defining features (essence) of Trump's speech

## Technical Notes and Dependencies

We used [Max Woolf's gpt-2-simple Python package](https://github.com/minimaxir/gpt-2-simple) as the basis for this project, which itself uses tensorflow, regex, requests, tqdm, numpy, and toposort. We also used pandas and os for small tasks to extract the data. The code all runs on Datahub, by far most efficiently on GPU-enabled servers.

## Reference

All references to papers, techniques, previous work, repositories you used should be collected at the bottom:
- [GPT-2 explanation](https://openai.com/blog/better-language-models/) and [code](https://github.com/openai/gpt-2)
- [gpt-2-simple](https://github.com/minimaxir/gpt-2-simple)
- [Kaggle data source](https://www.kaggle.com/littleotter/united-states-presidential-speeches?select=corpus.csv)
- [Miller Center Presidential Speech Archive](https://millercenter.org/the-presidency/presidential-speeches)
