## How to create your own stoplists

Stoplists are a .txt file that contain words that you wish to exclude from a Topic Model. The extra stoplist that I used can is [located in this repository: a file named genConj.txt](https://github.com/nmcdowell00/MALLET_tutorial/blob/master/genConj.txt). 
A preview of this document: 
```
i’m
it’s
he’s
i’ve
there’s
i’d
that’s
i’ll
we’d
they’re
one’s
you’re
things
```
One problem I had with stoplists was figuring out how to include words with apostrophes. With the help of Dr. Birnbaum I figured out that MALLET only accepts words with a smart apostrophe(’) not a regular apostrophe('). To create a smarty apostrophe hold OPTION,SHIFT, AND ](close square bracket key). 
