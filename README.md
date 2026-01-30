# Memes4Good  
**Multimodal Hate Speech Detection for Spanish Memes**

Memes4Good is a **multimodal AI system** designed to detect and classify **hate speech** in **Spanish-language memes**.  
Unlike traditional **text-based approaches**, this project analyzes **both visual content and  text** of the meme to better capture **context, irony and sarcasm**.

The system follows a **late-fusion architecture**, combining **computer vision** and **natural language processing** to model how meaning emerges from the interaction between images and text.

---

## **Key Result**
The model achieved **96.55% validation accuracy**, showing strong performance in distinguishing between **harmless humor** and **offensive content** in validation memes.

---

## **Dataset**
- **Total samples:** ~6,750 memes  
- **Train / validation split:** **80% / 20%**  
- **Sources:**  
  - **Public datasets:** DIMEMEX, Chilean Memes Dataset  
  - **Custom data collection** from public social media sources using APIs to capture **current slang and trends**  

---

## **Handling Irony and Context**
Detecting **irony** is one of the main challenges in meme classification.

- The model identifies cases where a **neutral image becomes offensive due to text**, and vice versa.  
- It is able to detect **ironic or sarcastic expressions** used to convey hate speech in most evaluated cases.

---

## **Limitations**
- Some memes depend on very specific **cultural or temporal context** that is difficult to model automatically.  
- For **ambiguous cases**, the system outputs **confidence scores close to 50%**, indicating uncertainty and the need for **human review**.  
- Performance is strongest on **clearly polarized content** (clearly harmless vs. clearly offensive).

---

## **Technical Stack**
- **Vision:** ResNet50V2 (feature extraction)  
- **Language:** BETO (Spanish BERT)  
- **Vision-Language Model:** Qwen2-VL (OCR and image understanding)  
- **ML Frameworks:** PyTorch, TensorFlow  
- **Deployment:** Interactive dashboard built with **Gradio**

---

## **Project Status**
This project was developed as an **academic and experimental system**, focused on **multimodal content moderation** in the Spanish language.
Hope you enjoy it!
