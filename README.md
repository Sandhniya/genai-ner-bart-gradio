## Development of a Named Entity Recognition (NER) Prototype Using a Fine-Tuned BART Model and Gradio Framework

### AIM:
To design and develop a prototype application for Named Entity Recognition (NER) by leveraging a fine-tuned BART model and deploying the application using the Gradio framework for user interaction and evaluation.

### PROBLEM STATEMENT:
The goal is to develop an application that can accurately recognize and categorize named entities such as persons, organizations, locations, dates, etc., from input text. By fine-tuning a pre-trained BART model specifically for NER tasks, the system should be able to understand contextual relationships and identify relevant entities. The Gradio framework will be used to build a user-friendly interface for real-time interaction and evaluation.

### DESIGN STEPS:

STEP 1: Data Preparation and Model Fine-Tuning
Collect or obtain a labeled NER dataset (e.g., CoNLL-2003).
Preprocess the dataset for tokenization and entity tagging.
Fine-tune a pre-trained BART model on the dataset using Hugging Face's transformers library.
STEP 2: Model Evaluation
Test the fine-tuned BART model on a validation set.
Evaluate performance using standard metrics like F1-score, precision, and recall.
Perform necessary adjustments and re-training if needed.
STEP 3: Gradio Interface Development
Use Gradio to build a simple interface where users can input text.
Integrate the fine-tuned model to process the input and display recognized entities in real-time.
Ensure the interface is intuitive and allows users to submit queries for NER.

### PROGRAM:
```
import gradio as gr
from transformers import BartForSequenceClassification, BartTokenizer
import torch

# Load the fine-tuned BART model and tokenizer
model = BartForSequenceClassification.from_pretrained('path_to_fine_tuned_model')
tokenizer = BartTokenizer.from_pretrained('facebook/bart-large')

# Function to perform NER
def recognize_entities(text):
    inputs = tokenizer(text, return_tensors="pt")
    outputs = model(**inputs)
    predictions = torch.argmax(outputs.logits, dim=2)
    
    # Convert predictions to entities (this is a simplified placeholder)
    entities = []
    for idx, pred in enumerate(predictions[0]):
        if pred.item() != 0:  # Non-zero predictions are entities
            entity = tokenizer.decode(inputs['input_ids'][0][idx])
            entities.append(entity)
    
    return {'entities': entities}

# Create Gradio interface
iface = gr.Interface(fn=recognize_entities, inputs="text", outputs="json")

# Launch the interface
iface.launch()
```

### OUTPUT:
![image](https://github.com/user-attachments/assets/144eacd4-a2d3-46a2-9d30-3cca2e6d3432)

### RESULT:
Hence Development of a Named Entity Recognition (NER) Prototype Using a Fine-Tuned BART Model and Gradio Framework  is verified.

