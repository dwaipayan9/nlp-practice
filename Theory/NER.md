What you did = Named Entity Recognition (NER)

This line is the key:

for ent in doc.ents:


doc.ents exists only because spaCy’s NER model ran.

So your code is:

Running an NER model → extracting its predictions → structuring them

That is textbook Named Entity Recognition.

What counts as NER (conceptually)

NER answers the question:

“Which spans of text refer to real-world entities, and what type are they?”

Examples:

Brexit → EVENT

United Kingdom → GPE

UK → GPE

2016 → DATE

That’s exactly what you’re seeing.

What spaCy did behind the scenes

When you ran:

doc = nlp(text)


spaCy executed this pipeline (simplified):

Tokenizer
 → Tagger
 → Parser
 → NER


NER is not a separate function call — it’s part of the pipeline.

Why NER is different from POS tagging
Task	Question it answers
POS tagging	What grammatical role does this word play?
NER	Is this word (or phrase) a real-world entity?

Example:

Word	POS	NER
Brexit	PROPN	EVENT
is	AUX	—
United	PROPN	GPE
Kingdom	PROPN	GPE

NER works on spans, not just single tokens.

Why your DataFrame matters

Your DataFrame is:

a clean representation of NER output

suitable for analytics, ML, indexing

exactly how NER is consumed in real systems

Search engines, document analysis, compliance tools — they all do this.

One sentence you should remember

NER = finding and labeling names of things in text.


What does GPE mean?

GPE = Geo-Political Entity

In spaCy (and most NLP systems), a GPE is:

A location that has a government or political identity


How GPE is different from similar labels

This is where people get confused, so let’s contrast them.

🗺️ GPE vs LOC vs ORG
Label	Meaning	Examples
GPE	Political entity	India, UK, EU
LOC	Physical location	Mount Everest, Pacific Ocean
ORG	Organization	Google, UN, NATO


Another useful one you’ll see: NORP

You might see:

NORP

It means:

Nationalities, Religious or Political groups

Examples:

British
Indian
American
Democrats

