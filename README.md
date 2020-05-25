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

- What is your concept for a generative art project? DONE
- What methods/networks/techniques will you employ (include links to technical precedents/code bases)NEEDS WORK
- What training data (if any) will you use for your project? DONE
- What kind of results do you hope that your system will produce? DONE
- How will you present your result/what form will your output take? DONE
- What if any challenges to you think may arise as you are working with this? DONE
- How are you expanding on topics we have covered in class? DONE, MAY NEED WORK
- Why is it interesting? (personally, culturally, politically, other) DONE
- List three papers / art projects that are references for this work. DONE

The concept for our generative art project is to look into various speeches and addresses, both verbally and written, given by the heads of states of the United States of America, Canada, and the United Kingdom in order to generate speeches that will be based off of an inputted keyword. For our training data, we will use data from the United States' State of the Union addresses from a dataset sourced from Kaggle, Canadian parliamentary speeches sourced from the Library and Archives of Canada, and British Parliamentary speeches sourced from the ParlSpeech V2 data set from Harvard University's Dataverse. We hope that our system will produce speeches that, from inputted keywords, produce speeches that can mimic diplomatic and political language while being based around the keywords. Our output will be presented by the model in text form, and we hope to present some examples in a creative manner such as spoken form. 

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

In the final submission, this section will describe both the data you use for this project and any pre-existing models/neural nets. For each you should provide the name, a textual description, and a link. If there is a paper (for neural net) link that as well.
- Such and such Neural Net. The short description of this neural net. 
  - [link to code]().
  - [Title of Paper with Link](). 
- Training data. Short description of training data including bibliographic info. [link to data]().

## Code

(20 points)

This section will link to the various code for your project (stored within this repository). Your code should be executable on datahub, should we choose to replicate your result. This includes code for: 

- code for data acquisition/scraping
- code for preprocessing
- training code (if appropriate)
- generative methods

Link each of these items to your .ipynb or .py files within this seection, and provide a brief explanation of what the code does. Reading this section we should have a sense of how to run your code.

## Results

(30 points) 

This section should summarize your results and will embed links to documentation to significant outputs. This should document both process and show artistic results. This can include figures, sound files, videos, bitmaps, as appropriate to your generative art idea. Each result should include a brief textual description, and all should be listed below: 

- image files (`.jpg`, `.png` or whatever else is appropriate)
- audio files (`.wav`, `.mp3`)
- written text as `.pdf`

## Discussion

(30 points, three to five paragraphs)

The first paragraph should be a short summary describing your results.

The subsequent paragraphs could address questions including:
- Why is this culturally innovative?
- How does your generative computational approach differ from traditional art/music/cultural production? 
- How do your results relate to broader social, cultural, economic political, etc., issues? 
- What are the ethical concerns for this form of generative art? 
- In what future directions could you expand this work?

## Team Roles

Provide an account of individual members and their efforts/contributions to the specific tasks you accomplished.

Rakesh - Abstract

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
