# attention_persistent_homology
Studying how well the persistent homology of collocations and keyphrases are preserved by various models. 

In this repo, we study how well the persistent homology of the probability distributions associated to tokens by the softmax of individual attention matrices is preserved by various models including 

- `bert-base-multilingual-cased`
- `gpt2`
- `gpt2-large`
- `gpt2-xl`
- `xlm-roberta-large`

We find that in all examples they are ranked as above, according to the Wasserstein distance between persistence diagrams. The methodology is as follows:

1. Select an `layer` and specific attention `head` in that layer. 
2. Compute the probability distributions of some text input given by the softmax of that attention matrix. 
3. Select the probability distributions associed with some subset of tokens, such as a keyphrase, a collocation, a multiword expression, or an idiom. 
4. Compute the pairwise distances between those probability distributions using the Jensen-Shannon distance. 
5. Compute the persistent homology of the distance matrix (obtained in the previous step) using Gudhi.
6. Repeat steps 1-5 for the same subset of tokens in a new contextual setting (like a new paragraph or some other text corpus).
7. Compare the two persistent diagrams obtained in this way using the Wasserstein distance. 

We can of course do this for multiple text corpera instead of just two, an in fact we do this for four text corpera and two different keyphrases in the notebooks. This gives a total of 12 comparisons (6 for each subset of text). In other words, we obtain $4$ persistence diagrams to compare, twice. Each set of $4$ persistence diagrams gives a total of $4 \choose 2$ comparisons. So, for $n$ text corpera, each containing some common keyphrase, we would have $n \choose 2$ comparisons in general. 
