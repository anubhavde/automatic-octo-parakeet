<h1>sentence_parser</h1>
<p>Parsing is a common task in natural language processing i.e it is the process of determining the structure of a sentence. This can be useful for a number of reasons: knowing the structure of a sentence can prove to be useful for a computer to better understand the meaning of a sentence. Also it can be useful for the computer to extract information out of a sentence. In particular, often it is useful to extract noun phrases out of a sentence to get an understanding for what the sentence is about.</p>
<p>In this project, I have used context-free grammer formalism to parse English sentences to determine their structure. Please note that in a context-free grammer, we repeatedly apply rewriting rules to transform symbols into other symbols. Our main objective here is to start with a nonterminal symbol S (representing a line) and repeatedly apply context-free grammer rules until we are able to generate a complete sentence of terminal symbols (i.e words). The rule S -> N V, for example, means that the S symbol can be rewritten as N V (a noun followed by a verb). If we also have the rule N -> "Holmes" and the rule V -> "sat", we can generate the complete sentence "Holmes sat.". </p>
<p>Of course, noun phrases might not always be as simple as a single word like "Holmes". We might have noun phrases like "my companion" or "a country walk" or "the day before Thursday", which require more complex rules to account for. To account for the phrase "my companion", for example, we might imagine a rule like:
NP -> N | Det N
</p>
<p>In this rule, I can say that an NP (a “noun phrase”) could be either just a noun (N) or a determiner (Det) followed by a noun, where determiners include words like "a", "the", and "my". The vertical bar (|) just indicates that there are multiple possible ways to rewrite an NP, with each possible rewrite separated by a bar.
</p>
<p>To incorporate this rule into how I parse a sentence (S), I modified my S -> N V rule to allow for noun phrases (NPs) as the subject of my sentence. See how? And to account for more complex types of noun phrases, I need to modify my grammar even further.</p>
<p>First, in the sentences directory, look at the text files . Each file contains an English sentence.</p>
<p>Now take a look at parser.py, and notice the context free grammar rules defined at the top of the file. I've defined a set of rules for generating terminal symbols (in the global variable TERMINALS). Notice that Adj is a nonterminal symbol that generates adjectives, Adv generates adverbs, Conj generates conjunctions, Det generates determiners, N generates nouns (spread across multiple lines for readability), P generates prepositions, and V generates verbs.</p>
<p>Next is the definition of NONTERMINALS, which contains all of the context-free grammar rules for generating nonterminal symbols. Right now, there’s just a single rule: S -> N V. With just that rule, we can generate sentences like "Holmes arrived." or "He chuckled.", but not sentences more complex than that.</p>
<p>The main function first accepts a sentence as input, either from a file or via user input. The sentence is preprocessed (via the preprocess function) and then parsed according to the context-free grammar defined by the file. The resulting trees are printed out, and all of the “noun phrase chunks” (defined in the Specification) are printed as well (via the np_chunk function).</p>
<h5>OUTPUT</h5>
<p>Sentence: Holmes sat</p>
<p>        S           </p>
<p>   _____|___   
<p>  NP        VP</p>
<p>  |         |</p>  
<p>  N         V</p> 
<p>  |         |  </p>
<p>holmes     sat</p>
<p></p>
<p>Noun Phrase Chunks</p>
<p>holmes</p>