#  NutriBot: Smart Nutrition Assistant for Personalized Dietary Support

NutriBot is a multimodal AI chatbot designed to deliver personalized, evidence-based dietary guidance using text, voice, or image inputs. It integrates OpenAIs GPT-4o, Whisper for audio transcription, BLIP for image captioning, and LangChain for retrieval-augmented question answering (RAG) using nutrition-focused documents and datasets.


##  Project Goals

- Provide reliable nutrition information based on trusted medical literature.
- Support users in both English and Arabic.
- Accept multimodal input: text, speech, and images.
- Offer dietary suggestions tailored to user health conditions.
- Detect and minimize AI hallucinations with LangSmith.


##  Architecture Overview

| Component        | Technology |
|------------------|------------|
| LLM              | OpenAI GPT-4o via LangChain |
| Vector Store     | ChromaDB (using OpenAIEmbeddings) |
| Audio Input      | Faster-Whisper |
| Image Captioning | BLIP (Hugging Face Transformers) |
| Translation      | Deep Translator (Google Translate API) |
| UI               | Gradio with custom ChatGPT-style layout |
| Memory           | LangChain ConversationBufferMemory |
| Evaluation       | LangSmith API (Latency, Cost, Hallucinations) |


##  Methodology

### 1. **Knowledge Base Construction**
- Extracted nutrition content from:
  - *Krauses Food & the Nutrition Care Process*
  - *Essential Pocket Guide to Clinical Nutrition*
  - *Nutrition Therapy and Pathophysiology*
- Text parsed using `PyMuPDF (fitz)`, chunked with `CharacterTextSplitter`, and embedded using `text-embedding-ada-002`.

### 2. **Retrieval-Augmented QA**
- Questions are passed to a `ConversationalRetrievalChain` that uses ChromaDB and GPT-4o.
- Structured prompts minimize hallucinations.
- Conversation memory maintains coherence using LangChain Memory.

### 3. **Multimodal Interaction**
- Voice input transcribed with Whisper.
- Image input processed with BLIP to generate food captions.
- Translation handled by GoogleTranslator for bilingual support.

### 4. **Evaluation**
- LangSmith is used to:
  - Measure latency and cost per query.
  - Detect hallucinations using keyword heuristics.
  - Compare output relevance.


##  Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/nutribot.git
cd nutribot
```

### 2. Create virtual environment
```bash
python -m venv nutribot-env
source nutribot-env/bin/activate  # Windows: nutribot-env\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Add `.env` file with your API keys
Create a `.env` file with the following:
```env
OPENAI_API_KEY=your-openai-api-key
LANGCHAIN_API_KEY=your-langsmith-api-key
```


##  Repository Structure

```
nutribot/

 NutriBot.ipynb             # Main development notebook
 requirements.txt           # All required dependencies
 .env                       # API keys (not included in Git)
 /data                      # PDF nutrition books
 /assets                    # Images, fonts for UI
 /utils                     # Image/audio processing helpers
 app.py (optional)          # Deployment script for HuggingFace/Spaces
```


##  Usage Guide

###  Run Locally
Open the notebook or run:
```bash
python app.py
```


## Demo

You can watch a full demo of NutriBot in action at the following link:

🔗 [NutriBot Deployment Demo (Google Drive)](https://drive.google.com/file/d/1tfI8nJMaLl4BngcDBiNepx-7GzbEusXR/view?usp=drive_link)

This demo shows how to use NutriBot with different input types (text, voice, and image), how the chatbot responds to nutrition questions, and how the evaluation results are generated using LangSmith.


###  Launch via Gradio
The Gradio interface supports:
- Chat history
- File upload (image or voice)
- Health condition field
- Bilingual interaction

###  Ask NutriBot:
- What is the best breakfast for diabetes?
- هل التفاح مفيد لارتفاع ضغط الدم
- Upload a photo of a food item and ask, Is this healthy for someone with anemia?


##  Features

-  Multimodal input support (text, voice, image)
-  Condition-specific dietary recommendations
-  Context-aware conversation with memory
-  English/Arabic support
-  Evaluation dashboard with LangSmith


##  Future Improvements

- Add structured diet plans based on diagnosis
- Expand to more languages (e.g., French, Spanish)
- Mobile-first UI
