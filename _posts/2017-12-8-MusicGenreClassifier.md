---
layout: post
title: Classifying Songs by Genre with the Million Song Dataset
---

A few weeks into my [Metis bootcamp](http://www.thisismetis.com/assets/files/Metis-Bootcamp-Curriculum-52f9979f4f638857bc185b0b788d6d832efb7f34d3b240e199dc6d3f2eef40ed.pdf), we were tasked to identify a classification problem to attack with machine learning. My immediate thought was to turn to music. If you’re like me, you spent a significant amount of brainpower in your teens obsessing over the correct classification and sub-classification of music (In my case, this revolved mostly around heavy metal, which is blessed/cursed with an [overwhelming number of sub-genres](https://en.wikipedia.org/wiki/Heavy_metal_genres)). The [Million Song Dataset (MSD)](https://labrosa.ee.columbia.edu/millionsong/) provided me with plenty of data to turn my attention to for this problem.

The MSD is exactly what it says it is: a collection of information pertaining to one million songs. The the dataset includes such information for a song as artist name, song title, release year, as well as data regarding the song itself: Number of bars, time to end of fade in, tempo, etc. Also included in the data are tags supplied by [Musicbrainz](https://musicbrainz.org/), an online music encyclopedia. These tags identified the musical genre(s) or sub-genre(s) that would apply to a song. My task would be to build a model that would be able to classify a song by its musical genre.

**Initial Obstacles**

I limited myself to six genres. The six genres I chose to focus on were ‘pop’, ‘rock’, ‘country’, ‘jazz’, ‘metal’, ‘hip-hop’, and ‘electronic’. I settled on these because they, or similar tags, were used often enough to ensure I had enough data for for training and testing. Also, they represented six styles that would cover the vast majority of modern recorded music.

The first issue was that not every song in the MSD had any tag at all. Luckily there were plenty of songs which were tagged, certainly enough to train a model. A more relevant problem was that songs were tagged with multiple labels and those labels were not mutually exclusive. For instance, any song by the Beatles had many different tags including both ‘pop’ and ‘rock’. In order to frame this as a classification problem I had to make some choices about which tag applied to a song would serve as my class label. In general, where applicable, I chose the more specific tag: songs tagged both ‘metal’ and ‘rock’ would therefore be labeled ‘metal’ for the purposes of classification. Songs tagged as both ‘pop’ and rock would be labeled as ‘rock’

**Feature selection**

The MSD provided a plethora of data on each song. This included the [Mel-Frequency Cepstral Coefficients (MFCCs)](https://en.wikipedia.org/wiki/Mel-frequency_cepstrum) for the song. Basically, MFCCs quantify the sonic qualities of an instant of a song. Every ⅓ of a second is captured and its pitch and timbre are each described with 12 numbers. The pitch data describes the the melodic and harmonic qualities of that segment of the song while the timbre describes the tonal quality. In other words, the timbre data would tell us whether a note or chord is being produced by a piano or a guitar. Since this is essentially the information that a listener would use to determine a song’s genre, this is what I would build my model on rather than other information even though it might improve accuracy (Knowing a song is released in 1967 would certainly eliminate ‘hip-hop’ and ‘electronica’ as potential genres). 

Since songs to be evaluated were of varying length, I determined I would use the first 100 seconds of the song in training my model. (In later tests, I used more time, or used 100 seconds from the middle of a song rather than the beginning. Neither variation improved results. Results diminished with less time)

**Dimension reduction**

With 24 MFCCs for every ⅓ of a second, using 100 seconds worth of a song meant 7200 dimensions in the feature space. I used Principal Component Analysis to reduce this to 60 dimensions. The number of dimensions was determined by performing a grid-search over the number of dimensions on a logistic regression classifier to identify the optimum number.

**Model Building**

At this point I trained a number of classifiers using Sklearn and compared the results. Logistic Regression, SVM, and Random Forrest all performed relatively similarly (Decision trees were the clear trailer). The main issue at this point was that because the classes in my dataset were unbalanced, each classifier over predicted the more prevalent classes. To account for this, I used random undersampling so that each class was represented the same number of times in my training set as the smallest class. After this adjustment each of the classifiers performed with between 40 and 55 percent accuracy on validation data. 

Throughout the process of building my model, I observed that the fewer number of class labels I was trying to predict, the better off any classifier performed. When a classifier was trained on only two possible genres, the accuracy was around 90%. At the same time, when I looked at the predicted probabilities for each class from a logistic regression classifier, there was rarely a clear choice with a greater than 50% probability. Often, the class with the second highest predicted probability was, in fact, the correct genre. 

**Ensemble Model**

With those observations in mind, I trained 15 separate SVMs, each one would distinguish between two possible genres (For example, one was trained only on songs labeled ‘rock’ or ‘pop’. Another was trained only on ‘rock’ and ‘hip-hop’, etc.). Going forward my approach would be to identify the two most likely genres for a song using a logistic regression classifier, and then use an appropriately trained SVM classifier to make the final determination.

The improvement in combining the multiple classifiers was dramatic. Accuracy jumped to 70% on the validation set. Improvements in precision and recall over using a single classifier also resulted.

**Reflection**

I completed this music genre classification project in July, though only now five months later, have I had the opportunity to write it up. For the most part, I think my process hold up. In fact the ensemble model achieved even better results on holdout test data (75% accuracy). Perhaps some more work could have been done in parameter tuning. The most relevant change I would make at this point would be to use more powerful boosted classifier algorithms 


*Thierry Bertin-Mahieux, Daniel P.W. Ellis, Brian Whitman, and Paul Lamere.  The Million Song Dataset. In Proceedings of the 12th International Society for Music Information Retrieval Conference (ISMIR 2011), 2011*

