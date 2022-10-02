# Making it easier to read abstracts.

Dataset used: `PubMed_20k_RCT_numbers_replaced_with_at_sign`

## Summary of all approaches:
<img width="500" alt="image" src="https://user-images.githubusercontent.com/84656834/191027015-dde51408-220d-4081-81e0-b989f352a240.png">
It was interesting to see how the tribrid model, which includes the token embedding, the character embedding and the positional
embedding performed well than other approaches and lead to a <b>6.33% increase</b> in the F1-Score.

## Details of the approaches used

### 1. Preprocessing.
- Read lines from the text file.
- Separate the tag and the text.
- Keep track of line numbers and total lines in abstract.

### 2. Data exploration encoding.
- Check distributions of tags.
- Check distributions of token lengths and sequence lengths. This helps in decising hyperpapameters when using embeddings and vectorizers.
- Encode the labels/tags using one-hot and label encoders.

### 3. Using Naive-Bayes model.
- I used a tf-idf vectorizer and a multinomial naive bayes model in this. This was the baseline model, further models attempted to perform better than this.

### 4. Data preparation for deep sequence models.
- Basically, this includes transforming our data to tensorflow datasets which are more efficient and faster. 
- We use batching and prefetching so that when the deep model is training on one batch, the other batch is fetched, loaded and kept 
ready for training.

### 5. Creating text vectorizer and embedding.
- Creating text vectorizer to map text to vectors. The distributions used earlier helped in selecting various parameters.
- Also created some visualization (wordcloud) using stats from the text vectorizer.
<!--- ![image](https://user-images.githubusercontent.com/84656834/191025749-08d153e5-01c9-4799-a3a5-7fc61a21c56d.png) --->
<img width="741" alt="image" src="https://user-images.githubusercontent.com/84656834/191028102-70dbb697-4f70-4eea-8dc0-6265a36d9793.png">


- Creating an embedding layer(this gets updated during training of models).

### 6. Modelling experiments (with token embeddings).
- Firstly I used the custom embedding to train a model with Conv1D layers.
- Then I used a pretrained embedding (universal sentence embedding) and Con1D and dense layers model.

### 7. Modelling experiments (with token and character embeddings).
- In this approach, I used pretrained token embeddings and custom character embeddings.
- First I tried using only character level embeddings.
- Then I concatenated these to take into account both and created a hybrid model. 
<img width="300" height="300" alt="image" src="https://user-images.githubusercontent.com/84656834/191028392-1ddaeef9-8ae1-406a-b56f-dec158584bbb.png">
- The above model made use of LSTM layers to get character embeddings.

### 8. Tribrid model (token and characters, line number, total lines).
- This model used the concatenated embeddings of token and character level embeddings and 
concatenated them with one hot encoding of line number (in an abstract) of each sentence and total lines one hot vector.
- This model performed the best as it also included positional information in the form of line numbers.
<img width="658" height="600" alt="image" src="https://user-images.githubusercontent.com/84656834/191029335-dd9a9e4e-0a3a-4ba9-ac54-5eff2bc6a51e.png">




