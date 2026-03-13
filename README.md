# DL- Developing a Deep Learning Model for NER using LSTM

## AIM
To develop an LSTM-based model for recognizing the named entities in the text.

## Problem Statement and Dataset
This notebook tackles Named Entity Recognition (NER), an NLP task focused on identifying and classifying named entities within text. It employs a Bi-directional Long Short-Term Memory (Bi-LSTM) network in PyTorch to train a model. The objective is to accurately extract and categorize entities like person, location, and organization from input sentences.

<img width="413" height="795" alt="{78571FB6-9767-4446-9F4C-B1728AD1924C}" src="https://github.com/user-attachments/assets/6e856b84-7832-4118-8125-1cd117bd4cde" />

## DESIGN STEPS
### STEP 1: 
Collect Dataset – Obtain a labeled dataset for Named Entity Recognition (NER).


### STEP 2: 
Preprocess Data – Tokenize text, convert words to numbers, and pad sequences.




### STEP 3: 
Word Embedding – Convert words into vector representations using an embedding layer.




### STEP 4: 

Build Model – Create an LSTM-based deep learning model.



### STEP 5: 

Train Model – Train the model using the training dataset.


### STEP 6: 
Evaluate Model – Test the model and measure accuracy.






## PROGRAM

### Name:VENKATESAN R

### Register Number:212224230299

```python
# Model definition
class BiLSTMTagger(nn.Module):
    def __init__(self, vocab_size,tagset_size, embedding_dim=50, hidden_dim=100):
        super(BiLSTMTagger,self).__init__()
        self.embedding=nn.Embedding(vocab_size,embedding_dim)
        self.dropout=nn.Dropout(0.1)
        self.lstm=nn.LSTM(embedding_dim,hidden_dim,batch_first=True,bidirectional=True)
        self.fc=nn.Linear(hidden_dim*2,tagset_size)
    def forward(self, input_ids):
        x.self.embedding(x)
        x=self.dropout(x)
        x, _ = self.lstm(x)
        return self.fc(x)

model =BiLSTMTagger(len(word2idx)+1,len(tag2idx)).to(device)
loss_fn =nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)


# Training and Evaluation Functions
def train_model(model, train_loader, test_loader, loss_fn, optimizer, epochs=3):
    def train_model(model, train_loader, test_loader, loss_fn, optimizer, epochs=3):
    train_losses, val_losses = [], []
    for epoch in range(epochs):
        model.train()
        train_loss = 0.0
        for batch in train_loader:
            input_ids = batch["input_ids"].to(device)
            labels = batch["labels"].to(device)
            optimizer.zero_grad()
            outputs = model(input_ids) 
            loss = loss_fn(outputs.view(-1, len(tag2idx)), labels.view(-1))
            loss.backward()
            optimizer.step()
            train_loss += loss.item()
        train_losses.append(total_loss)

        model.eval()
        val_loss=0
        with torch.no_grad():
            for batch in test_loader:
              input_ids = batch["input_ids"].to(device)
              labels = batch["labels"].to(device)
              outputs = model(input_ids)
              loss = loss_fn(outputs.view(-1, len(tag2idx)), labels.view(-1))
              val_loss += loss.item()
        val_losses.append(val_loss)
        print(f"Epoch {epoch+1}: Train loss = {total_loss:.4f}")
    return train_losses, val_losses


```

### OUTPUT

## Loss Vs Epoch Plot

<img width="441" height="68" alt="{E80D0DAC-8EC7-4FBA-A10A-17C5F23CDBE4}" src="https://github.com/user-attachments/assets/50471533-9ae7-4a69-baa1-4d5b89fa0a26" />

<img width="648" height="564" alt="{26F34064-7FE6-4FE0-9C84-B5F9B07DDD1C}" src="https://github.com/user-attachments/assets/b8872766-40f2-437d-a38e-eaed70026a6e" />

### Sample Text Prediction
<img width="363" height="533" alt="{E003FED4-6D5C-4D18-B4D6-B5B651D2BB2F}" src="https://github.com/user-attachments/assets/68edb9d5-be25-47a4-a0aa-cf106c64d084" />

## RESULT
The LSTM-based deep learning model successfully identified named entities such as person, location, and organization from text data with good accuracy.
