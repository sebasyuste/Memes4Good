# Memes4Good (v3)
**Multimodal Hate Speech Detection for Spanish Memes**

**Memes4Good v3** is an experimental AI system for detecting hate speech and offensive content in **Spanish-language memes**.  
It uses a **late-fusion multimodal architecture** that combines visual, textual, and OCR-based context, achieving **~78.8% accuracy** and **~85% AUC** on a culturally diverse Spanish meme dataset.

---

## Project Overview
Memes4Good is an academic research project focused on **multimodal content moderation**.  
Unlike traditional text-only approaches, this system addresses the fact that memes often convey meaning through the **interaction between image and text**, frequently involving irony, sarcasm, or cultural references.

Version 3 (v3) introduces a more interaction-aware fusion strategy to better capture implicit and contextual hate speech in Spanish memes.

---

## Model & Dataset Access
Due to file size limits, the model weights and the meme dataset are hosted on Hugging Face:
* **Model Weights (v3):** https://huggingface.co/sebasyuste/MEMES4GOOD-MODEL
* **Meme Dataset:** https://huggingface.co/sebasyuste/MEMES4GOOD-DATA
* **Live Demo:** https://huggingface.co/sebasyuste/MEMES4GOOD-DEMO

---

## Why a Multimodal Approach?
Memes rarely communicate meaning through a single modality:

- A neutral image can become offensive depending on the caption  
- A harmless text can turn hateful depending on the image  
- Irony often appears when text and image contradict each other  

For this reason, **unimodal models are fundamentally limited**.  
A multimodal approach is necessary to properly understand meme semantics.

---

## Architecture Design
### Why Late Fusion?

Memes4Good v3 uses a **late-fusion architecture**, where each modality is processed independently before being combined at a high semantic level.

This design was chosen for the following reasons:

1. **Modality Independence**  
   Visual and textual data have very different structures. Late fusion allows each model to learn strong, specialized representations.

2. **Reduced Noise Propagation**  
   Early fusion can amplify OCR errors or irrelevant visual features. Late fusion combines abstract features, reducing this risk.

3. **Better Handling of Irony and Context**  
   Irony usually emerges only after each modality is understood separately. Late fusion enables reasoning over cross-modal relationships.

For these reasons, late fusion is a robust and practical choice for meme moderation.

---

## Multimodal Pipeline

### Visual Branch — *EfficientNetB0*
- Pre-trained on ImageNet  
- Efficient and lightweight  
- Captures hierarchical visual patterns (faces, gestures, symbols)  
- Suitable for scalable or real-world deployment  

---

### Textual Branch — *BETO (bert-base-spanish-wwm-cased)*
- Spanish-specific BERT model  
- Better handling of slang and informal language  
- More accurate representation of regional Spanish variations  

Multilingual BERT models often miss these nuances.

---

### OCR & Visual Context — *Qwen2-VL (2B-Instruct)*
Qwen2-VL is used to:
- Perform advanced OCR on meme images  
- Generate a **semantic description of the visual scene**

This visual context helps the classifier understand *what is happening in the image*, not just what text is present.

> Qwen2-VL is used only as a context-generation module and is not fine-tuned during training.

---

## Fusion Mechanism (v3)
Instead of simple concatenation, version 3 introduces an **interaction-aware fusion strategy**:

1. Element-wise **Multiply** between visual and textual feature vectors  
2. Followed by **Concatenation**  
3. Final classification using a dense layer  

This forces the model to focus on **cross-modal agreement or conflict**, which is critical for detecting implicit hate and sarcasm.

---

## Dataset Construction
Due to the lack of large Spanish meme datasets, multiple sources were combined to build a dataset of approximately **6,750 samples**:

- **DIMEMEX (IberLEF)** — Mexican Spanish memes  
- **Chilean Memes Dataset** — Regional and linguistic diversity  
- **Custom Dataset (~3,000 samples)**  
  - Scraped from public social media  
  - Includes recent slang and internet-specific language  

### Dataset Limitations
- **Label subjectivity**: Hate speech is often ambiguous  
- **Cultural bias**: Meaning depends on local context  
- **Label noise**: Introduces a natural performance ceiling  

---

## Training and Results

- **Epochs:** 30  
- **Learning Rate:** 1e-5  
- **Loss Function:** Binary Cross-Entropy  
- **Techniques:** Class weighting and label smoothing  

### Validation Performance
- **Accuracy:** ~78.82%  
- **AUC:** ~84.97%  

These metrics show good discriminative ability, but must be interpreted considering dataset limitations.

---

## Why Real-World Performance Is Inconsistent
Despite solid validation results, performance in real-world scenarios can be unstable. This is expected for this task.

### Main Reasons:
1. **Cultural Context Drift**  
   Memes evolve quickly. New formats and references appear faster than datasets can be updated.

2. **Irony and Ambiguity**  
   Even humans often disagree on whether a meme is offensive.

3. **False Positive vs. False Negative Trade-off**  
   Higher sensitivity to hate speech increases the risk of false positives.

4. **Data Quality Ceiling**  
   No model can outperform noisy or inconsistent labels.

For this reason, Memes4Good is intended as a **decision-support system**, not a fully autonomous moderation tool.

---

## Project Status
Memes4Good v3 is an **academic and experimental research project** exploring multimodal reasoning for Spanish content moderation.

It highlights:
- The necessity of multimodal approaches for meme understanding  
- The effectiveness of late fusion for cross-modal reasoning  
- Data quality and cultural context as the main remaining challenges  

