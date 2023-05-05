# Classical Language Toolkit
Zachary Shuda
### Introduction
Classical languages are languages that have a large amount of written works that date to an earlier time. Since many classical languages are earlier forms of modern languages, classical languages usually have different grammar, syntax, and phonology. CLTK offers the ability to tag a variety of classical languages for parts of speech and phonetics.
## Offered languages
CLTK uses 3 letter strings to refer to a language within the code. Some of the languages have less lexicon and less tools than other languages.
| Language  | Code |
| ---------- | ---------- |
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

In the demonstration, I will be using Old Norse "non" as an example because I am very familiar with Old Norse grammar and phonology.
## Phonological Transcription and Syllabification
Old Norse text can be broken down into phonemes and syllables with the following code:

```
from cltk.core.data_types import Pipeline
from cltk.tokenizers.processes import OldNorseTokenizationProcess
from cltk.text.processes import OldNorsePunctuationRemovalProcess
from cltk.phonology.processes import OldNorsePhonologicalTranscriberProcess,OldNorseSyllabificationProcess
from cltk.languages.utils import get_lang
pipe = Pipeline(description = "", processes = [OldNorseTokenizationProcess,OldNorsePunctuationRemovalProcess,OldNorsePhonologicalTranscriberProcess,OldNorseSyllabificationProcess], language = get_lang("non"))
nlp = NLP(language = "non", custom_pipeline = pipe, suppress_banner = True)
```

With that setup, we can take a string of text in Old Norse and convert into phonemes. My example text is from stanza 5 of the Hymiskviða:

```
string1 = "Býr fyr austan Élivága; hundvíss Hymir at himins enda; á minn faðir móðugr ketil; rúmbrugðinn hver, rastar djúpan."
doc = nlp.analyze(string1)
```
