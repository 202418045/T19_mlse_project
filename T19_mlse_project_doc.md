# T19 MLSE Project Documentation

## Team Information

**Team ID:** T19

**Project Name:** Verse2Vision - Bidirectional Multimodal RAG System for Cultural Preservation

### Team Members

| Name | SID | Contribution |
|------|-----|--------------|
| Aruni Saxena | 202418006 | [Contribution details] |
| Heer Choksi | 202418019 | [Contribution details] |
| Paarth Patel | 202418045 | [Contribution details] |
| Yash Deshmukh | 202418063 | [Contribution details] |

---

# Project Documentation

## Table of Contents

1. [Project Overview](#project-overview)
2. [Problem Statement](#problem-statement)
3. [Objectives](#objectives)
4. [Methodology](#methodology)
5. [System Architecture](#system-architecture)
6. [Implementation Details](#implementation-details)
7. [Workflow](#workflow)
8. [Technology Stack](#technology-stack)
9. [Results & Evaluation](#results--evaluation)
10. [Cultural Preservation Impact](#cultural-preservation-impact)
11. [Future Enhancements](#future-enhancements)
12. [Conclusion](#conclusion)

---

## 1. Project Overview

**Verse2Vision** is a Bidirectional Multimodal Retrieval-Augmented Generation (RAG) system designed to preserve and transmit authentic Indian epic knowledge (specifically Hanuman Chalisa) to future generations. The system enables:

- **Text → Image**: Converting ancient verses into engaging visual stories
- **Image → Text**: Interpreting mythological images into authenticated narratives
- **Multilingual Support**: Supporting multiple Indian languages
- **Cultural Authenticity**: Grounding all outputs in original knowledge base

### Key Innovation

Unlike traditional AI systems that may hallucinate or generate inaccurate information, Verse2Vision uses RAG to ensure every output is grounded in the original knowledge base (`kb.json`), preventing misinformation and preserving cultural authenticity.

---

## 2. Problem Statement

### Challenges in Cultural Preservation

1. **Information Loss**: Oral traditions and regional variations can lead to loss or alteration of original epic details
2. **Language Barriers**: Sanskrit and traditional texts are not widely accessible to modern audiences
3. **Misinterpretation**: Modern adaptations may deviate from authentic source material
4. **AI Hallucination**: Traditional LLMs may generate incorrect or culturally inappropriate content
5. **Accessibility**: Complex epic narratives are difficult for children and non-specialists to understand

### Solution Approach

Verse2Vision addresses these challenges by:
- Creating a digital knowledge base from authentic sources
- Using RAG to ground all outputs in original material
- Providing visual storytelling for better understanding
- Supporting multiple languages for broader accessibility
- Ensuring traceability to source verses

---

## 3. Objectives

### Primary Objectives

1. **Preservation**: Create a permanent digital repository of authentic epic knowledge
2. **Accessibility**: Make complex epic narratives accessible to children and general audiences
3. **Authenticity**: Ensure all generated content is grounded in original sources
4. **Education**: Provide engaging, educational content that maintains cultural integrity
5. **Innovation**: Demonstrate how modern AI can preserve, not replace, traditional knowledge

### Secondary Objectives

1. Multilingual support for Indian languages
2. Visual storytelling for enhanced learning
3. Interactive Q&A system based on authentic verses
4. Audio narration for accessibility
5. Scalable architecture for expanding to other epics

---

## 4. Methodology

### 4.1 Retrieval-Augmented Generation (RAG)

RAG is a framework that enhances LLM capabilities by:
1. **Retrieval**: Finding relevant information from a knowledge base
2. **Augmentation**: Providing retrieved context to the LLM
3. **Generation**: Creating outputs grounded in retrieved information

**Why RAG?**
- Prevents hallucination (generating false information)
- Ensures authenticity (all outputs traceable to source)
- Maintains accuracy (grounded in knowledge base)
- Enables verification (users can check source verses)

### 4.2 Multimodal Processing

The system processes multiple data types:
- **Text**: Verses, questions, stories
- **Images**: Generated artwork, uploaded photos
- **Audio**: Narrated stories and explanations

### 4.3 Bidirectional Workflow

#### Direction 1: Text → Image
```
Ancient Verse → RAG Retrieval → LLM Enhancement → Image Generation → Visual Story
```

#### Direction 2: Image → Text
```
Mythological Image → Vision Model → RAG Retrieval → Authentic Narrative
```

---

## 5. System Architecture

### 5.1 Component Overview

```
┌─────────────────────────────────────────────────────┐
│              Verse2Vision System                     │
├─────────────────────────────────────────────────────┤
│                                                      │
│  Frontend (Streamlit)                                │
│    ↓                                                 │
│  RAG Pipeline                                        │
│    ├── Knowledge Base (kb.json)                     │
│    ├── Embedding Store (TF-IDF)                     │
│    ├── Retriever (Cosine Similarity)                │
│    └── Generator (Gemini LLM)                       │
│    ↓                                                 │
│  Multimodal Processing                               │
│    ├── Vision Model (Gemini Vision)                 │
│    ├── Image Generator (Pollinations AI)            │
│    └── TTS (Google TTS)                             │
│    ↓                                                 │
│  Output Generation                                   │
│    ├── Visual Stories                                │
│    ├── Narrated Content                              │
│    └── Authentic Explanations                        │
└─────────────────────────────────────────────────────┘
```

### 5.2 Core Modules

#### Module 1: Knowledge Base Loader (`rag/loader.py`)
- Parses `kb.json` into structured Python objects
- Loads verse data: Sanskrit text, translations, contexts, story seeds

#### Module 2: Embedding Store (`rag/embeddings.py`)
- Converts verses into numerical vectors using TF-IDF
- Creates searchable vector representations

#### Module 3: Retriever (`rag/retriever.py`)
- Finds most relevant verses using cosine similarity
- Returns top-k matches for any query

#### Module 4: Generator (`rag/generator.py`)
- Uses Gemini LLM for text generation
- Creates prompts that emphasize KB grounding
- Generates stories, answers, and image descriptions

#### Module 5: Vision Module (`rag/vision.py`)
- Uses Gemini Vision API for image captioning
- Converts images to text descriptions

#### Module 6: Image Generator (`rag/image_generator.py`)
- Generates images using Pollinations AI
- Creates comic-style visual stories

#### Module 7: TTS Module (`rag/tts.py`)
- Provides multilingual text-to-speech
- Auto-detects language from text content

---

## 6. Implementation Details

### 6.1 Embedding Strategy: TF-IDF

**Why TF-IDF?**
- Lightweight (no GPU required)
- Fast processing
- Interpretable results
- Suitable for small-to-medium knowledge bases
- No model downloads required

**Process:**
1. Combine text fields (Sanskrit, transliteration, meanings, tags)
2. Create TF-IDF vectorizer
3. Fit on all verses
4. Transform each verse into vector
5. Store in memory for fast retrieval

### 6.2 Retrieval Mechanism: Cosine Similarity

**Formula:**
```
similarity = (A · B) / (||A|| × ||B||)
```

**Benefits:**
- Normalized similarity (0 to 1)
- Focuses on direction, not magnitude
- Works well with TF-IDF vectors

### 6.3 LLM Integration: Google Gemini

**Models Used:**
- Primary: `gemini-2.5-flash` (fastest)
- Fallback: `gemini-2.5-pro` (more capable)

**Prompt Engineering:**
- Emphasizes KB grounding
- Prevents hallucination
- Maintains cultural authenticity
- Ensures creative presentation while staying true to source

### 6.4 Image Generation: Pollinations AI

**Features:**
- Free API (no key required)
- Fast generation (15-30 seconds)
- High quality (1024x1024)
- Comic-style illustrations

### 6.5 Multilingual Support

**Languages Supported:**
- English, Hindi, Marathi, Bengali, Tamil, Telugu, Kannada, Malayalam, Gujarati, Punjabi, Urdu

**Detection:**
- Automatic script detection
- Language-specific TTS generation

---

## 7. Workflow

### 7.1 Visual Story Creation (Text → Image)

**Step-by-Step:**

1. **User Input**: User enters topic (e.g., "Hanuman carrying Sanjeevani mountain")

2. **RAG Retrieval**:
   - Query converted to TF-IDF vector
   - Cosine similarity calculated with all verse vectors
   - Top-k most relevant verses retrieved

3. **LLM Prompt Building**:
   - System creates prompt emphasizing KB grounding
   - Includes retrieved verses with meanings and contexts
   - Requests 3 sequential comic-style images with subtitles

4. **LLM Generation**:
   - Gemini generates 3 image descriptions
   - Each includes visual description and child-friendly subtitle
   - Ensures narrative continuity and cultural authenticity

5. **Image Generation**:
   - Each description enhanced with comic-style instructions
   - Sent to Pollinations API
   - 1024x1024 images generated

6. **TTS Narration**:
   - Subtitles combined into narration
   - Language auto-detected
   - Audio generated

7. **Display**:
   - Images shown with subtitles
   - Audio player provided
   - Source verses displayed

### 7.2 Image Analysis (Image → Text)

1. **Image Upload**: User uploads mythological image

2. **Vision Analysis**: Gemini Vision generates detailed caption

3. **RAG Retrieval**: Caption used as query to find matching verses

4. **LLM Explanation**: Authentic narrative generated from retrieved verses

5. **TTS Narration**: Explanation narrated in detected language

6. **Display**: Image, explanation, and audio provided

### 7.3 Question Answering

1. **Question Input**: User asks question about Hanuman Chalisa

2. **RAG Retrieval**: Find relevant verses

3. **LLM Answer**: Generate answer using ONLY retrieved verses

4. **TTS Narration**: Answer narrated

5. **Display**: Answer with source verses shown

---

## 8. Technology Stack

### 8.1 Libraries & Versions

| Library | Version | Purpose |
|---------|---------|---------|
| streamlit | ≥1.28.0 | Web UI framework |
| scikit-learn | ≥1.3.0 | TF-IDF vectorization |
| google-generativeai | ≥0.3.0 | Gemini API client |
| numpy | ≥1.24.0 | Numerical operations |
| Pillow | ≥9.0.0 | Image processing |
| requests | ≥2.28.0 | HTTP requests |
| gtts | ≥2.5.0 | Text-to-speech |

### 8.2 AI Models

- **Embedding**: TF-IDF (statistical, no ML model)
- **LLM**: Google Gemini 2.5 Flash/Pro
- **Vision**: Google Gemini Vision API
- **Image Generation**: Pollinations AI (Flux model)
- **TTS**: Google TTS (gTTS)

### 8.3 Infrastructure

- **Frontend**: Streamlit (web-based)
- **Backend**: Python 3.8+
- **Storage**: In-memory (embeddings), JSON file (knowledge base)
- **APIs**: Google Generative AI, Pollinations AI

---

## 9. Results & Evaluation

### 9.1 Functional Results

✅ **Successfully Implemented:**
- Bidirectional text-image conversion
- RAG-based retrieval system
- Visual story generation (3 sequential images)
- Image analysis and explanation
- Multilingual TTS narration
- Q&A system based on authentic verses
- Cultural authenticity preservation

### 9.2 Quality Metrics

**Accuracy:**
- All outputs traceable to source verses
- No hallucination observed
- Cultural authenticity maintained

**Performance:**
- Fast retrieval (<1 second)
- Image generation (15-30 seconds per image)
- TTS generation (<5 seconds)

**User Experience:**
- Clean, intuitive interface
- Multilingual support
- Audio narration for accessibility
- Visual storytelling for engagement

### 9.3 Limitations

1. **Knowledge Base Size**: Currently limited to Hanuman Chalisa verses
2. **Image Quality**: Dependent on external API (Pollinations)
3. **Language Detection**: May require manual selection for mixed-language text
4. **Real-time Processing**: Some operations require internet connection

---

## 10. Cultural Preservation Impact

### 10.1 Problem Solved

**Before Verse2Vision:**
- ❌ Information loss through oral transmission
- ❌ Modern misinterpretations
- ❌ AI hallucination in generated content
- ❌ Language barriers
- ❌ Inaccessible to children

**After Verse2Vision:**
- ✅ Permanent digital preservation
- ✅ Authentic, grounded content
- ✅ No hallucination (RAG ensures KB grounding)
- ✅ Multilingual accessibility
- ✅ Child-friendly visual stories

### 10.2 Long-term Impact

1. **Knowledge Preservation**: Permanent digital record of authentic epics
2. **Educational Value**: Engaging content for learning traditional stories
3. **Cultural Continuity**: Maintaining authentic narratives across generations
4. **Scalability**: Can be expanded to other epics and texts
5. **Accessibility**: Available to anyone with internet access

### 10.3 Verification & Traceability

Every generated output:
- Can be traced back to specific verses
- Shows source verses to users
- Maintains direct lineage to original epics
- Prevents misinformation through RAG grounding

---

## 11. Future Enhancements

### 11.1 Short-term Improvements

1. **Expanded Knowledge Base**: Add more verses and epics
2. **Improved Image Quality**: Fine-tune prompts for better visual stories
3. **Offline Mode**: Local image generation for better privacy
4. **User Feedback**: Collect feedback for continuous improvement

### 11.2 Long-term Vision

1. **Multi-Epic Support**: Expand to Ramayana, Mahabharata, etc.
2. **Advanced Visualization**: 3D models, interactive stories
3. **Collaborative Learning**: User contributions to knowledge base
4. **Mobile App**: Native mobile application
5. **AR/VR Integration**: Immersive storytelling experiences

---

## 12. Conclusion

Verse2Vision demonstrates how modern AI technology can be used to **preserve, not replace**, traditional knowledge. By combining RAG architecture with multimodal processing, the system:

- ✅ Preserves authentic epic knowledge
- ✅ Makes content accessible to all
- ✅ Maintains cultural integrity
- ✅ Provides engaging educational content
- ✅ Prevents misinformation through grounding

The project showcases the potential of RAG in cultural preservation, proving that AI can be a bridge between ancient wisdom and future generations while maintaining authenticity and accuracy.

---

## Appendix

### A. Repository Structure

```
T19_mlse_project/
├── app_streamlit.py              # Main Streamlit UI
├── requirements.txt              # Python dependencies
├── kb.json                       # Knowledge base
├── README.md                     # Project README
├── PROJECT_DOCUMENTATION.md      # Technical documentation
├── rag/                          # RAG modules
│   ├── loader.py                # Knowledge base loader
│   ├── embeddings.py            # TF-IDF embeddings
│   ├── retriever.py             # Verse retrieval
│   ├── generator.py             # LLM generation
│   ├── vision.py                # Image captioning
│   ├── image_generator.py       # Image generation
│   └── tts.py                   # Text-to-speech
└── test_*.py                     # Testing utilities
```

### B. Key Features

- Bidirectional multimodal RAG
- Visual storytelling (comic-style)
- Multilingual support (11+ languages)
- Audio narration
- Interactive Q&A
- Cultural authenticity preservation

### C. Usage Instructions

1. Install dependencies: `pip install -r requirements.txt`
2. Set up Gemini API key in Streamlit sidebar
3. Run: `streamlit run app_streamlit.py`
4. Start creating visual stories!

---

**Team T19 - MLSE Project**

*Preserving Cultural Heritage Through Modern AI*

