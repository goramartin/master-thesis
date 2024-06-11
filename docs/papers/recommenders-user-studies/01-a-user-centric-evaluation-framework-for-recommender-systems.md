# A user-centric evaluation framework for recommender systems

[Link](https://dl.acm.org/doi/10.1145/2043932.2043962) (2013)

## Intro

This research was motivated by our interest in understanding the criteria for measuring the success of a recommender system from users’ point view.
They propose a framework for evaluating recs systems.
It contains questions and constructs to use on the users.

Previously works focused on algorithm accuracy [1] and prediction accuracy [9].
Recently research focused on issues related to users' subjective opinions and developing additional criteria.
A user satisfaction does not correlate with high recommender accuracy.

## Model deployment

A questionnaire consists of a set of constructs, participating questions for each construct and hypothesis relating the constructs.

The starting point is to delimit the domain of the construcs and generate sample questions representing concepts under consideration for each construct.

They observed key user variables as the main construct.

Then a work is done to match the question and semantic menaing of the construct which will be clear to the users.

- They used TAM - a technology acceptance model which seeks to understand a set of perceived qualities of a system and users' intention to adopt the system as the result of these qualities but also users' motivation.
    - the main three points
        - perceived ease of use
        - usefulness of the system
        - intention of the user to use the system
    -  it was critised because of simplicisity
  - Updated version of TAM - unified theory of accepance and use of technology
    - 4 construcs
      - perfomance expectancy
      - effort expectancy
      - social influence 
      - and faciliating conditions
- SUMI - software usability measurement inventoy
  - psychometric evaluation model to measure quality of software from end users
  - 5 constructs
    - efficiency
    - affect
    - helpfulness
    - control
    - learnability
  - used for desiners and developers to assess the quality of use of a sofrware product or prototy

They did not generate linear model of sample questions but structured the questions into four layers of higher level constructs crossing four dimension:
- perceived system qualitiees
- users beliefs as a result of these qualities
- subjective attitude
- behavioral intentions
This can more clearly explicate how usrs' perception of the physical features of a system influecnes their beliefs, atitudes and behaviours.

They eventually created 15 construcs and forty three questions.


## A perceived system qualities

Refers to users perception of the objective characteristis (functional, informationnal capabilities) of recs.
- Quality of recommendations
- interaction adequacy
- interface adequacy

1. quality of recommendations
   - a primary task is to suggest items of interest, in literature the most critical in success of the system
   - they found correlation between 4 qualities of items to users intention to use the system
     1. perceived accuracy
        - MYSLIM SI, ZE TO  DAVA VECI CO BYCH CHTEL 
        - degree to which users feel recommendations match their interest and prefernces
        - easier to obtain then objective measure
        - if they respond in a good way, it usually correlate to objective accuracy
     2. novelty
        - extent to which users receive new and interesting recommendations
        - it is related to systems ability to educate users and help them discover new items
        - a similar term serendipity - mira prekvapeni - tohle bych chtel
        - but novelty covers new but serendipity new but surprising
        - but it is confusin so they use novelty and discovery
     3. attractiveness
        - whether the recs items are capable of stimulating users imagination and evoking positive emotion
        - different from accurate and novel - since it does not need to ensure positive emotion in the user
     4. diversity
        - diversity of items
     5. context compatibility
        - whether or not the recs consider general or personal context requirements
        - a users mood at the time, occasion
2. interface adequacy
   - most of the works are how to optimize the layout to achieve the maximum visibility
   - whether to use the image text or combination
   - in this framework they evaluate users subjective evals of interface of:
     - information sufficiency
     - interfacae label 
     - layout adequacy and clarity
3. interaction adequacy
   - systems ability to elicit user preferences, allow user feedback and explain reasons why recommendations facilitate purchasing decision also weights hevaily on users overall perception of a recommender
     - preference elicication
     - preference revision
     - and system ability to explain its results
   -  behavioral system collect information from past activities
   -  for rating based system needs to collect the ratings
      -  eg good or bad
      -  desire or values they offer
      -  popularity
4. information sufficiency and explicability
   - a systems ability to display price, quantity, image, users reviews ...
   - any information of the item that would help users with making decision
   - or more specific why items are suggested to the active user

### Beliefs 

A higher level of user perception.
Influenced by perceived qualities.
**How well and how efficiently the system helps them accomplish their task.**
    - decision support and nature of interactions

<br>

1. Perceived usefulness
   - to which extend the usage would imporover users performance
   - compared without the help of the recommender
   - questoin whether the system is usefull to them
   - they divide it into 
     - decision support
     - decision quality
   - objective of decision is to overcome the limit of users rationality and help them make more satisfying decisions with minimal amount of effor.
   - decision support
     - how much the user feels assisted by the recommender
   - decision quality
     - belief that the users ceertainty in believeing that he made a correct choice
2. perceived ease of use
   - users ability to quicly and correctly accomplish tasks with ease and without frustratoin
   - a task completion time and learning time can be measured objectively, it can be difficult to distinguish the actual task completion time from measured task time
     - users can be exploring   
   - it might be better to measure this than how fast the user accomplished it
3. control and transparency
   - user control
     - if the user felt in control with interaction
   - transparency
     - whether it allows a user to understand the systems logic
     - whehter the user sees the correspondnce between the preferences expressed in measurement process and recommendations presented

### Attitude

Overrall feeling towards the system
Which is derived from the experience as he interacts with the system.

- Overall satisfaction
  - determines what users think and feel while using the system
  - it gives users opportunity to express their preferences and opinitons about the system
- confidence inspiring 
  - convince users of the information or products recommended
- trust
  - whether or not the user found the system trustworthy

### Behavioral intentions

Whether or not the system is able to influence users decision to use the system and purchase some of the recommended results.

Eg. ecommerce wants royalty and stimulate users future visits.
- agreement to use the system
- user acceptance of the recs items
- user retention
- intention to introduce the system to friends

## Hypotheses

They hypothese the direction and connectin between the constructs.
**They say at least 5 people should be used on item.**

**They asked the question before filing the questionare to fill up the memory of the user.**

- they looked for users that give false answers
  - same rating on all - on page, on entire set, contradict reverse questions
  - they removed it from the outlier
- they used factor analysis, structural equation modeling and other techniques from [15]
- they computed internal consistency and reliability of the model using cronbach's alpha and item to tal correlations.
- This validation process is intended to reveal internal consistencies of given construct as well as identifying the clusters of related variables.