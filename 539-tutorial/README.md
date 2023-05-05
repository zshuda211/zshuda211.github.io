# Classical Language Toolkit
Zachary Shuda
### Introduction
Classical languages are languages that have a large amount of written works that date to an earlier time. Since many classical languages are earlier forms of modern languages, classical languages usually have different grammar, syntax, and phonology. CLTK offers the ability to tag a variety of classical languages for parts of speech and phonetics.
## Offered languages
CLTK uses 3 letter strings to refer to a language within the code. Some of the languages have less lexicon and less tools than other languages. Latin has the most functionality and resources and tutorials usually use Latin as the example language. In the demonstration, I will be using Old Norse as an example because I am very familiar with Old Norse grammar and phonology.

| Language  | Code |
| Akkadian  | "akk"  |
| Arabic  | "arb"  |
| Aramaic | "arc" |
| Classical Chinese | "lzh" |
| Coptic | "cop" |
| Gothic | "got" |
| Greek | "grc" |
| Hindi | "hin" |
| Latin | "lat" |
| Mid High German | "gmh" |
| Old English | "ang" |
| Mid English | "enm" |
| Old French | "fro" |
| Mid French | "frm" |
| Old Church Slavonic | "chu" |
| Old Norse | "non" |
| Pali | "pli" |
| Punjabi | "pan" |
| Sanskrit | "san" |

## Phonological Transcription and Syllabification
Old Norse text can be broken down into phonemes and syllables with the following code:

```
from cltk.core.data_types import Pipeline
from cltk.tokenizers.processes import OldNorseTokenizationProcess
from cltk.text.processes import OldNorsePunctuationRemovalProcess
from cltk.phonology.processes import OldNorsePhonologicalTranscriberProcess,OldNorseSyllabificationProcess
from cltk.languages.utils import get_lang
from cltk.nlp import NLP
pipe = Pipeline(description = "", processes = [OldNorseTokenizationProcess,OldNorsePunctuationRemovalProcess,OldNorsePhonologicalTranscriberProcess,OldNorseSyllabificationProcess], language = get_lang("non"))
nlp = NLP(language = "non", custom_pipeline = pipe, suppress_banner = True)
```

With that setup, we can take a string of text in Old Norse and convert into phonemes. My example text is from stanza 5 of the Hymiskviða:

```
string1 = "Býr fyr austan Élivága; hundvíss Hymir at himins enda; á minn faðir móðugr ketil; rúmbrugðinn hver, rastar djúpan."
doc = nlp.analyze(string1)
doc.words[3].phonetic_transcription
>>> eːlivaːɣa
```

We can also break the words into syllables, though the syllabification is simplistic and creates minor errors.

```
doc.words[4].syllables
>>> ['hund','víss']
doc.words[14].syllables  # proper syllabification would be ['rúm','brug','ðinn']
>>> ['rúmb','rug','ðinn']
```

## POS Tagging
Old Norse text can be tagged with a part of speech. Verbs and nouns have specified form and case information. Undetermined words are tagged as "Unk".

```
from cltk.tag.pos import *
p = POSTag(language="non")
tags = p.tag_tnt(string1)
tags[8]  # It is noun in genitive case
>>> ('himins','N-G')
tags[11]  # tag_tnt tagged this word as preposition which it sometimes is, but in this sentence, it is a verb
>>> ('á','P')
tags[14]  # tag_tnt decided it couldn't tag this word, but it is adjective
>>> ('móðugr','Unk')
```
## Conclusion
Different languages have different problems that arise from analysis. The largest problem with Old Norse is its highly fusional nature. In a language like Latin, most words can be broken into a root and an ending, where the root changes little or not at all as the endings change. In Old Norse, the root can change given different endings, meaning different forms of the root need be given for a parser to recognize the variants. In particular, the vowel or vowels of the root can change between two endings, even if the endings look the same. Arabic has a similar feature where the vowels of the root will change and an ending will be used to give a specific grammatical meaning. In Old Norse, this is mostly because the endings used to have vowels that caused the root vowel to harmonize and then the ending vowel disappeared or severly reduced.

fótr (a foot) fótar (of a foot) fœtr (feet)
hönd (a hand) handar (of a hand) hendr (hands)
helpr (one helps) hjalpa (they help) halp (one helped) hulpu (they helped)
