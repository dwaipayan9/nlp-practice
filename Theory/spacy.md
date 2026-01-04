The code you wrote (repeated)
import pandas as pd

pos_data = []

for token in doc:
    pos_data.append(
        (token.text, token.pos_, token.tag_, token.dep_,
         token.shape_, token.is_alpha, token.is_stop)
    )

pos_df = pd.DataFrame(
    pos_data,
    columns=['Token', 'POS', 'Tag', 'Dep', 'Shape', 'Is Alpha', 'Is Stop']
)

pos_df

First: what is doc?
doc = nlp(text)


doc is a spaCy Doc object.

Think of it as:

A container holding the entire linguistic analysis of the text.

When you do:

for token in doc:


You are iterating over tokens, not characters, not words as strings.

Each token is an object with dozens of attributes.

Line-by-line explanation
1️⃣ pos_data = []

You create an empty list to store rows.

Each row = information about one token.

2️⃣ for token in doc:

You loop through the document token by token.

Example tokens:

Brexit | is | the | impending | withdrawal | ...


Each token is a spaCy Token object.

3️⃣ pos_data.append(...)

You append a tuple with selected attributes:

(
 token.text,
 token.pos_,
 token.tag_,
 token.dep_,
 token.shape_,
 token.is_alpha,
 token.is_stop
)


So every token becomes one row.

Now the important part: what does each attribute mean?

Let’s go column by column.

🧱 Token
token.text


The original text of the token.

Example:

Brexit


Nothing fancy here.

🧠 POS (Universal POS tag)
token.pos_


This is the coarse-grained part-of-speech tag.

Based on Universal POS Tags (cross-language).

Examples:

NOUN

VERB

PROPN

ADJ

AUX

In your table:

Brexit → PROPN


Meaning: proper noun

🔍 Tag (Fine-grained POS tag)
token.tag_


This is language-specific, more detailed.

English uses Penn Treebank tags.

Examples:

NN → noun

NNP → proper noun

VBZ → verb, 3rd person singular

DT → determiner

So:

Brexit → POS=PROPN, Tag=NNP


Think of:

POS = category

Tag = precise form

🔗 Dep (Dependency label)
token.dep_


This tells how the word relates grammatically to others.

Example:

Brexit → nsubj


Meaning:

“Brexit” is the nominal subject of the sentence

Other examples:

ROOT → main verb

det → determiner

amod → adjective modifier

This comes from dependency parsing.

🔤 Shape
token.shape_


This describes the orthographic pattern of the word.

Examples:

Xxxxx → Capitalized word

xxxx → lowercase

dd → digits

XxXx → mixed case

For:

Brexit → Xxxxx


This is very useful for:

NER

rule-based features

ML heuristics

🔠 Is Alpha
token.is_alpha


Boolean:

True → contains only letters

False → contains digits / punctuation

Example:

Brexit → True


Useful for filtering tokens.

🚫 Is Stop
token.is_stop


Boolean:

True → common stopword

False → content word

Example:

the → True
Brexit → False


spaCy uses language-specific stopword lists.

Why convert this into a pandas DataFrame?

Because:

Tables are easier to inspect

You can filter, group, analyze

This mirrors how NLP features are fed into ML

Example:

pos_df[pos_df["Is Stop"] == False]

Big picture: what you just built

You created a structured linguistic representation of raw text.

You transformed:

Raw text → Tokens → Linguistic features → Table


This is exactly how NLP feeds ML models.

Why this matters later (very important)

When you do ML:

tokens → features

POS tags → signals

dependency roles → context

stopwords → filtered

spaCy is doing the hard linguistic work, pandas makes it inspectable.

Mental model (lock this in)

spaCy = linguistic analysis engine
pandas = inspection + feature engineering

Together → NLP pipeline.

NLTK → data / learning
spaCy → preprocessing / linguistic features
scikit-learn → classical ML
transformers → deep NLP (later)
