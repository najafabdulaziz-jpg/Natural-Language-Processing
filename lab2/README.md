***task 2:***

**re.compile()**

`re.compile()` takes a regular-expression pattern string and turns it into a reusable `Pattern` object. once compiled, that object exposes methods directly like `.match()`, `.search()`, `.findall()`, `.split()`, `.load()`, `.sub()`, etc. 

it is useful because:
- if the same pattern will be used many times (e.g., inside a loop over many documents), compiling it once and reusing the compiled object.
- it makes code more readable and maintainable, since the pattern gets a descriptive variable name (e.g., `pattern`, `hashtag_pattern`).

***task 3:***

**re.split()**

`re.split()` divides a string wherever a regular-expression pattern is found, and returns the pieces as a list from between the matches. 

***task 4:***

**spacy.load()**

`spacy.load()` loads an installed spaCy language pipeline, such as `en_core_web_sm`, and returns an `nlp` object. 
you then pass text to this object to create a processed spaCy Doc.

**spaCy and NLTK tokenization:**

For the sentence both tokenizers produce the same tokens: `I`, `'m`, `enjoying`, `the`, `NLP`, `course`, `!`, both correctly split the contraction `I'm` into `I` and `'m` and separate the trailing `!` as its own token. 
In general, though, the two libraries use different underlying rules: spaCy uses language-specific tokenization rules and exception lists as part of a full NLP pipeline, which returns token objects rather than plain strings, while NLTK's `word_tokenize` is based on the Penn Treebank tokenizer conventions, which primarily returns word and punctuation tokens using its recommended tokenizer.

the main difference is that NLTK focuses on tokenization, while spaCy tokenization is part of a complete NLP pipeline that can also analyze grammar, lemmas, and entities. spaCy’s Doc contains Token objects and the loaded pipeline’s linguistic data.
