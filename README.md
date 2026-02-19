# Memes4Good: Multimodal Meme Classification

## Project Description

Memes4Good is a project focused on classifying Spanish memes using a multimodal approach. Since memes combine image and text to create meaning, the system processes both at the same time.

The main goal is to explore how different architectural choices affect performance and generalization with a limited dataset.

---

## Model Versions

The project includes three model versions, each with a different level of complexity.

### ROBUST

**Architecture:** Uses frozen EfficientNetB0 and BETO (Spanish BERT). Most layers are not trained, which keeps the model simpler.

**Parameters:** 64-unit projection layers and a high dropout rate (0.7).

**Input:** MAX_LEN = 64.

**Performance:** This version performs well with the current dataset because its limited capacity helps reduce overfitting.

---

### BALANCED

**Architecture:** Light fine-tuning. The last 15 CNN layers and the final BERT layer are trainable.

**Parameters:** 192-unit projection layers with dropout between 0.45 and 0.55.

**Input:** MAX_LEN = 128.

**Performance:** Provides stable results and a good balance between flexibility and regularization.

---

### POWERFUL

**Architecture:** More layers are trainable (18 CNN layers and 2 BERT layers).

**Complexity:** Uses three BERT outputs (pooler output, CLS token, and mean pooling) combined with 256-unit projection layers.

**Input:** MAX_LEN = 128.

**Status:** This version is more scalable in theory. However, with the current dataset size, it tends to overfit and does not generalize well.

---

## Multimodal Architecture Overview

All models follow the same general process:

1. **Image Branch**  
   EfficientNetB0 extracts visual features from the meme image.

2. **Text Branch**  
   BETO (Spanish BERT) processes the meme text to extract contextual meaning.

3. **Feature Combination**  
   - ROBUST: simple concatenation of image and text features.  
   - BALANCED & POWERFUL: combine features using sum, difference, and element-wise product to capture relationships between image and text (useful when they contradict each other).

4. **Final Classification**  
   A dense layer with sigmoid activation outputs a probability between 0 (Harmful) and 1 (Harmless).

---

## Dataset Information

The dataset contains approximately 6,750 Spanish memes.

Sources:

- **Dimemex** (Mexican memes)  
- **Chilean Memes**  
- **Telegram scraping** (~3,000 memes from a specific offensive meme group)

Important details:

- The dataset comes from only three sources.  
- The Telegram data was collected from a single group, so it does not represent the full diversity of internet memes.  
- Compared to the huge variety of meme formats online, this dataset is limited.  
- The model is trained only with Spanish memes.

Defining what is “offensive” is not always clear and can depend on context or interpretation. Because of these limitations, the model should be seen as a **pre-filtering tool**, not a final decision system.

You can find the full dataset here: [Memes4Good Dataset on Hugging Face](https://huggingface.co/datasets/sebasyuste/MEMES4GOOD-DATA) <br><br>

For detailed information regarding each sample, you can access the metadata CSV here: [Memes4Good Metadata CSV](https://github.com/sebasyuste/Memes4Good/blob/main/text_and_description_dataset.csv)

The file contains the following key columns used for training and inference:
* **meme_id**: Unique identifier corresponding to the meme image filename.
* **extracted_text**: The literal text present in the meme image.
* **description_es_new**: A Spanish semantic description of the visual scene and context.
* **harmless**: The target label where 0 indicates harmful/offensive content and 1 indicates harmless content.

---

## Generalization and Real-World Performance

Validation results during training were reasonably good.

However, when testing with random memes from the internet, performance drops. The models struggle with new templates, different humor styles, and formats not seen during training.

This shows the gap between validation performance and real-world behavior.

---

## Limitations

- **Dataset size:** 6,750 samples are not enough for large multimodal models.  
- **Limited diversity:** Only three sources, and one Telegram group.  
- **Subjectivity:** Humor, irony, and cultural context make meme classification difficult.  
- **Real-world performance:** None of the models perform especially well outside the training data.

With the current dataset, ROBUST and BALANCED behave more reliably. POWERFUL could benefit from much more and more diverse data.

---

## Notebooks

- `Memes4Good_ROBUST_sebasyuste.ipynb`  
- `Memes4Good_BALANCED_sebasyuste.ipynb`  
- `Memes4Good_POWERFUL_sebasyuste.ipynb`  
- `MEMES4GOOD_DEMO_sebasyuste.ipynb` (interactive demo)

The demo allows switching between the three model versions.

---

## Hugging Face Models

All three models are available here:  
[https://huggingface.co/sebasyuste/MEMES4GOOD-MODELS/tree/main](https://huggingface.co/sebasyuste/MEMES4GOOD-MODELS/tree/main)

---

## Final Note

POWERFUL has the most flexible architecture and could improve with a much larger and more diverse dataset. For the current data scale, ROBUST and BALANCED offer more stable results.

This project shows both the potential and current limitations of multimodal meme classification with limited data.
