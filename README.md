<H3>NAME: AARON H</H3>
<H3>REGISTER NO: 212223040001</H3>
<H3>EX. NO.7</H3>

<H1 ALIGN =CENTER>Implementation of Text  Summarization</H1>
<H3>Aim: to perform automatic text summarization using Natural Language Processing (NLP) techniques. </H3> 
 <BR>
<h3>Algorithm:</h3>
Step 1 Import necessary libraries for natural language processing tasks.<BR>
Step 2: Download NLTK resources, including the punkt tokenizer and stopwords.<BR>
Step 3: Define Text Preprocessing Function to tokenize, remove stopwords, and perform stemming.<BR>
Step 4: Define the Text Summarization Function using a simple frequency-based approach.<br>
    - Calculate the frequency of each word in the preprocessed text.<br>
    - Calculate a score for each sentence based on the sum of word frequencies.<br>
    - Select the top N sentences with the highest scores to form the summary.<br>
Step 5: Construct the main program to read the paragraph  and perform text summarization<br>
      - Generate and print the original text.<br>
      - Generate and print the text summary using the  Text Summarization function<br>
<H3>Program:</H3>

```
import nltk
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.stem import PorterStemmer
from heapq import nlargest
import string

nltk.download('punkt')
nltk.download('stopwords')
nltk.download('punkt_tab')

ps = PorterStemmer()

def preprocess_text(text):
    words = word_tokenize(text.lower())

    filtered_words = []

    for word in words:
        if word not in stopwords.words('english') and word not in string.punctuation:
            stemmed_word = ps.stem(word)
            filtered_words.append(stemmed_word)

    return filtered_words

def text_summarization(text, num_sentences=2):

    processed_words = preprocess_text(text)

    word_frequencies = {}

    for word in processed_words:
        if word in word_frequencies:
            word_frequencies[word] += 1
        else:
            word_frequencies[word] = 1

    sentences = sent_tokenize(text)

    sentence_scores = {}

    for sentence in sentences:

        sentence_words = word_tokenize(sentence.lower())

        for word in sentence_words:

            stemmed_word = ps.stem(word)

            if stemmed_word in word_frequencies:

                if sentence in sentence_scores:
                    sentence_scores[sentence] += word_frequencies[stemmed_word]
                else:
                    sentence_scores[sentence] = word_frequencies[stemmed_word]

    summary_sentences = nlargest(num_sentences, sentence_scores, key=sentence_scores.get)

    summary = ' '.join(summary_sentences)

    return summary

text = input("Enter the paragraph:\n")

summary = text_summarization(text)

print("\nOriginal Text:\n")
print(text)

print("\nSummary:\n")
print(summary)

```

<H3>Output</H3>

```

Enter the paragraph:
Artificial Intelligence (AI) is transforming the world in many ways. It is being used in healthcare to diagnose diseases, in transportation to develop self-driving cars, and in education to provide personalized learning experiences. AI systems can process huge amounts of data much faster than humans, helping businesses make better decisions. However, there are also concerns about job displacement, privacy, and ethical issues related to AI. Researchers and governments are working together to create regulations and guidelines to ensure that AI is developed and used responsibly. As technology continues to advance, AI is expected to become an even more important part of everyday life.

Original Text:

Artificial Intelligence (AI) is transforming the world in many ways. It is being used in healthcare to diagnose diseases, in transportation to develop self-driving cars, and in education to provide personalized learning experiences. AI systems can process huge amounts of data much faster than humans, helping businesses make better decisions. However, there are also concerns about job displacement, privacy, and ethical issues related to AI. Researchers and governments are working together to create regulations and guidelines to ensure that AI is developed and used responsibly. As technology continues to advance, AI is expected to become an even more important part of everyday life.

Summary:

AI systems can process huge amounts of data much faster than humans, helping businesses make better decisions. Researchers and governments are working together to create regulations and guidelines to ensure that AI is developed and used responsibly.


```

<H3>Result:</H3>
Thus ,the program to perform the Text summarization is executed sucessfully.


