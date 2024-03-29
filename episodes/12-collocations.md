## Collocations

Keypoints:
- We can use NLTK's ```BigramAssocMeasures()``` and ```BigramCollocationFinder``` to find the words commonly found together in a document set.
- We can score collocations using ```bigram_measures.likelihood_ratio```.

We may want to see what terms are often used together. We can do this by looking for collocations in a text, i.e. two word tokens occurring together in the text more often than would be expected by chance.

For this we need to import the ```nltk.collocations``` module and more specifically ```BigramAssocMeasures()``` and ```BigramCollocationFinder```. We allow a window of 5 words between collocated words.


```python
from nltk.collocations import BigramAssocMeasures
from nltk.collocations import BigramCollocationFinder

bigram_measures = BigramAssocMeasures()
finder = BigramCollocationFinder.from_words(inaugural_tokens, 5)
```

We then look for words that appear together 10 times or more.


```python
finder.apply_freq_filter(10)
```

A number of measures are available to score collocations or other associations including ```bigram_measures.likelihood_ratio```. We apply this measure below and show the top ten collocated tokens (occuring in a window of 5 tokens with a frequency of 10 or more).


```python
finder.nbest(bigram_measures.likelihood_ratio, 10)
```

    [('the', 'of'),
     ("'", 's'),
     ('.', 'The'),
     ('.', 'We'),
     ('United', 'States'),
     ('has', 'been'),
     ('.', '.'),
     ('have', 'been'),
     ('.', 'It'),
     (',', 'and')]


> ## Task: Change the code above to display collocations in the inaugural speeches after stopwords, punctuation and single digits have been removed.
>
> > ## Answer
> > ~~~python
> > nltk.download('stopwords')
> > from nltk.corpus import stopwords
> > remove_these = set(stopwords.words('english') + list(string.punctuation) + list(string.digits))
> > bigram_measures = BigramAssocMeasures()
> > filtered_text = [w for w in inaugural_tokens if not w in remove_these]
> > finder = BigramCollocationFinder.from_words(filtered_text, 5)
> > finder.apply_freq_filter(10)
> > finder.nbest(bigram_measures.likelihood_ratio, 7)
> > ~~~
```
[('United', 'States'),
 ('fellow', 'citizens'),
 ('let', 'us'),
 ('one', 'another'),
 ('I', 'shall'),
 ('Let', 'us'),
 ('men', 'women')]
```
[Index](https://ang-uio.github.io/Textmining/) or  
[next](https://ang-uio.github.io/Textmining/episodes/13-part-of-speech-tagging-text.html)
