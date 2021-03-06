---
layout: base
title:  'Simple Noun Phrases'
udver: '2'
---

# Simple Noun Phrases

Noun phrases are a fundamental type of linguistic structure that we expect to find in all languages. Noun phrases occur as core arguments of predicates and typically refer to objects (in a wide sense), but they have a range of other functions as well (including predicative uses). This chapter focuses on noun phrases headed by a noun or pronoun, possibly accompanied by grammatical markers and modifier phrases. Later chapters will cover more complex and atypical types of noun phrases:

* Noun phrases with clausal modifiers
* Apposition and flat structures in noun phrases (names, titles)
* Elliptical noun phrases 

<span style="color: blue">**TO DO:** Decide on groupings and provide links to later chapters (above).</span>

This chapter is structured as follows:

* [Nominal Heads](#nominal-heads)
* [Case Markers](#case-markers)
* [Determiners](#determiners)
* [Numerals](#numerals)
* [Classifiers](#classifiers)
* [Nominal Modifiers](#nominal-modifiers)
* [Adjectival Modifiers](#adjectival-modifiers)


## Nominal Heads

In the simplest case, a noun phrase consists of a single head word, which is typically a noun, proper noun or pronoun.

~~~ sdparse
hon/PRON såg/VERB filmen/NOUN \n she saw the-film
nsubj(såg, hon)
obj(såg, filmen)
~~~
~~~ sdparse
hon/PRON såg/VERB Batman/PROPN \n she saw Batman
nsubj(såg, hon)
obj(såg, Batman)
~~~
~~~ sdparse
hon/PRON såg/VERB den/PRON \n she saw it
nsubj(såg, hon)
obj(såg, den)
~~~

In all of the Swedish examples above, the subject is the pronoun "hon" (she), while the object is respectively the noun "filmen" (the-movie), the proper noun "Batman", and the pronoun "den" (it). 

### Morphological Annotation of Nominal Heads

Nominal head words should normally be tagged [NOUN](), [PROPN](), or [PRON](). 

Depending on the language, nominal head words may in addition carry a number of morphological features, of which the most common are: 

* For NOUN: [Case](), [Definite](), [Gender](), [Number]()
* For PRON: [Case](), [Definite](), [Gender](), [Number](), [Person](), [Poss](), [PronType](), [Reflex]()

For example, in the Swedish examples above, we find the following morphological analyses:

* For "filmen" (the-movie): <span style="color: blue">NOUN + Case=Nom\|Definite=Yes\|Gender=Com\|Number=Sing</span>
* For "Batman" (the-movie): <span style="color: blue">NOUN + Case=Nom</span>
* For "den": <span style="color: blue">PRON + Definite=Yes\|Gender=Com\|Number=Sing\|Person=3\|PronType=Prs</span>

## Case Markers

Case marking is one of the strategies that languages use to encode the grammatical function of a noun phrase. Case marking can be realized through morphological inflection (captured by the feature [Case]() mentioned above) or by clitics or adpositions (prepositions and postpositions). In the interest of cross-linguistic parallelism, UD takes a radical approach and treats all adpositions as case markers, attaching them to the nominal head with the [case]() relation.
This allows us to analyze the following examples as both having a direct dependency relations from the predicate to the noun phrase filling the (oblique) agent role of a passive, despite the fact that Czech uses a noun in the instrumental case ("kočkou") while Swedish adds a preposition ("av"):

~~~ sdparse
pes/NOUN byl/AUX honěn/VERB kočkou/NOUN:Case=Ins \n dog was chased by cat
nsubj:pass(honěn, pes)
obl(honěn, kočkou)
aux:pass(honěn, byl)
~~~

~~~ sdparse
hunden/NOUN jagades/NOUN av/ADP katten/NOUN \n the-dog was-chased by the-cat
nsubj:pass(jagades, hunden)
case(katten, av)
obl(jagades, katten)
~~~

This means that prepositional (and postpositional) phrases are treated in UD as extended noun phrases, where the nominal head is the referential core while the adposition is a functional marker. This can be seen as an instantiation of Tesnière's notion of a dissociated nucleus (Tesnière, 1959) and does not entail that the adposition is seen as a syntactic dependent of the noun in the narrow sense.

<span style="color: blue">**TO DO:** Provide links to a central bibliography?</span>

### Morphological Analysis of Case Markers

While adpositions are normally tagged [ADP](), the tag [PART]() may be more appropriate for case markers that differ from morphological case markers only by being clitics instead of inflectional morphemes. For example, in Ungarinjin (an Australian language), locative case is marked by a phrase-final clitic (Rumsey, 1978; cited in Velupillai, 2012):

~~~ sdparse
dambun/NOUN nininga/PRON ra/PART:Case=Loc \n camp my LOC
nmod:poss(dambun, nininga)
case(dambun, ra)
~~~

The clitic "ra" will be tagged [PART]() and carry the feature <span style="color: blue">Case=Loc</span> feature, whereas ordinary adpositions do not have a [Case]() feature.

## Determiners

Noun phrases headed by nouns often contain determiners, which can be roughly divided into three classes:

* Articles
* Demonstratives
* Interrogatives
* Quantifiers

Articles, like English "a(n)" and "the", specify definiteness or related properties. They are obligatory in some languages (at least with some types of nouns), and completely absent in others. Demonstratives, like Latin "hic", "ille" and "ist", anchors the noun phrase deictically and seem to be available in all languages. Interrogatives, like English "which", are used to form noun phrases that can be used in interrogative (and sometimes relative) clauses. Quantifiers, like French "tout", "quelque", and "aucun", specify quantity or existence of the referent. 

~~~ sdparse
the/DET:PronType=Art book/NOUN
det(book, the)
~~~

~~~ sdparse
this/DET:PronType=Dem book/NOUN
det(book, this)
~~~

~~~ sdparse
which/DET:PronType=Int book/NOUN
det(book, which)
~~~

~~~ sdparse
every/DET:PronType=Tot book/NOUN
det(book, every)
~~~

~~~ sdparse
all/DET:PronType=Tot books/NOUN
det(books, all)
~~~

~~~ sdparse
all/DET:PronType=Tot the/DET:PronType=Art books/NOUN
det(books, all)
det(books, the)
~~~

~~~ sdparse
all/DET:PronType=Tot these/DET:PronType=Dem books/NOUN 
det(books, all)
det(books, these)
~~~

In many languages, different determiners are in complementary distribution or have special constraints on their cooccurrence and possible order. Regardless of whether a noun phrase contains one or more determiners, the syntactic [det]() relation is used to connect them all directly to the nominal head, as illustrated in the examples above. However, in languages where this is relevant, the subtype [det:predet]() may be used to distinguish determiners that have to precede other determiners (such as "all" in the last two examples above).

**NB:** The [det]() relation is not used for numerals ("three books") nor for possessives ("my books"); see below.

### Morphological Analysis of Determiners

Determiners will typically be tagged [DET](), but the tag [PRON]() is also possible for words that are used both as determiners and as full (pronominal) noun phrases and where the pronominal use is predominant. <span style="color: blue">**QUESTION:** Is this the right recommendation?</span>

Regardless of whether determiners are tagged [DET]() or [PRON](), they should normally carry a [PronType]() feature indicating the type of determiner (`Art` for articles, `Dem` for demonstratives, `Int`for interrogatives, and so on). Depending on the language, determiners may also carry additional features that indicate agreement with the head noun,
such as [Gender](), [Number](), and [Case]().
 
## Numerals

A `nummod` is a numeral modifying the head of a nominal phrase.

## Classifiers

A `clf` (classifier) is a word which accompanies a noun in certain grammatical contexts.

## Nominal Modifiers

An `nmod` is a nominal phrase modifying the head of another nominal phrase, with or without a special case marker. Treebanks may optionally use `nmod:poss` to distinguish non-adpositional possessives.

~~~ sdparse
the office of the Chair
nmod(office-2, Chair-5)
~~~

~~~ sdparse
the Chair 's office
nmod:poss(office-4, Chair-2)
~~~

### Possessives

Special case of `nmod` with subtype `nmod:poss`.

## Adjectival Modifiers

An `amod` is an adjective modifying the head of a nominal phrase.

~~~ sdparse
Sam , the manager
appos(Sam, manager)
~~~

~~~ sdparse
Sam eats red meat
amod(meat, red)
~~~

~~~ sdparse
Sam spent forty dollars
nummod(dollars, forty)
~~~

~~~ sdparse
Sam spent everything he had
acl:relcl(everything, had)
~~~

~~~ sdparse
Sam spent everything that he had
acl:relcl(everything, had)
obj(had, that)
~~~

## Function Word Dependents

Nominals may also contain the following typical function word dependents:

* Determiners attach to the head of the nominal with the `det` relation.
* Adpositions attach to the head of the nominal with the `case` relation.
* Classifiers attach to a numeral or possessive with the `clf` relation.

~~~ sdparse
the Chair 's office
det(Chair-2, the-1)
nmod(office-4, Chair-2)
case(Chair-2, 's-3)
~~~

~~~ sdparse
the office of the Chair
det(office-2, the-1)
nmod(office-2, Chair-5)
case(Chair-5, of-3)
det(Chair-5, the-4)
~~~

~~~sdparse
sān gè xuéshēng \n three clf student
nummod(xuéshēng, sān)
clf(sān, gè)
~~~
