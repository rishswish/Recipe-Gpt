# 🍳 Personalized Recipe Recommendation Using LLM

This project presents a smart, user-centric **recipe recommendation system** that leverages **Large Language Models (LLMs)** and advanced **natural language processing** to deliver highly personalized culinary suggestions. It tackles key challenges like personalization, cold start problem, and hallucinations in generated content—offering a refined meal planning experience tailored to each user’s preferences, allergies, and dietary needs.

---

## 🎯 Objectives

- Recommend recipes tailored to individual preferences and dietary restrictions
- Handle new users with limited history (cold start)
- Ensure allergen-aware and contextually relevant recommendations
- Incorporate user feedback through a continuous learning loop
- Deploy a real-time system using LLMs and a vector database

---

## 📂 Dataset

- **RecipeNLG Dataset** (based on Recipe1M+)
- Over **2 million deduplicated recipes**
- Key fields: Title, Ingredients, Directions, Source, NER (food entities)
- Used **text-embedding-ada-002** for vector representation

---

## ⚙️ System Architecture

### 🧪 Preprocessing

- Merged Title, Ingredients, and Directions into `combined_info`
- Tokenized and embedded using OpenAI’s `text-embedding-ada-002`
- Stored embeddings in **LanceDB** for fast vector search

### 🧠 Candidate Generation

1. **User Inputs:**
   - Ingredients, preferences, allergies
   - Prompt generated from profile data

2. **LLM Selection:**
   - Prompt and top relevant recipes passed to **GPT-4**
   - Returns 3 diverse, coherent candidate recipes

---

## 🍽️ Recommendation Algorithm

### 🆕 For New Users:
- **Ingredient Overlap Score**:

math
Overlap = |Prompt ∩ Recipe| / |Prompt ∪ Recipe|
Recommends recipe with highest ingredient overlap

---

## 👤 Personalized Recommendation for Existing Users

- Recommends recipe with **highest ingredient overlap** for new users.
- For existing users:
  - Retrieves last **5 rated recipes** from history.
  - Computes **cosine similarity** between recipe embeddings.
  - Final **score** is a weighted sum of similarity × scaled rating.
  - Recipes with allergens are **penalized with a score of -1** and excluded.

---

## 🔁 Feedback Loop

- Users rate recipes on a scale of **1–5 stars**.
- Ratings are **normalized to [-1, 1]** and saved to user history.
- These ratings are used to **update future recommendations**, making the system smarter with every interaction.

---

## 📊 Results Summary

| Component         | Observation                                                |
|------------------|------------------------------------------------------------|
| Cosine Similarity| Accurately aligned vegetarian history with veg recipes     |
| Rating Influence | Higher-rated historical items skewed final recommendation  |
| Allergen Filter  | Recipes with allergens are penalized and excluded          |

> **Sample Finding:**  
> *Paneer Tikka Masala* was assigned a score of `-1` due to a **nut allergen** and was **excluded** from recommendation.

---

## 💡 Conclusion

This system demonstrates:

- ✅ Effective use of **LLMs** for personalized generation  
- ✅ Robust handling of **diverse dietary needs and preferences**  
- ✅ Continuous improvement via **user feedback loop**

With thoughtful design and safety-first filtering, the model creates a **dynamic and inclusive recommendation experience**.

---

## 🚀 Future Work

- Support for **real-time personalization** and user interaction  
- Integration with **vision models** for image-based suggestions  
- Support for **multilingual** and culturally-specific cuisines  
- Explore **LLM prompt distillation** for faster and cheaper inference

---

## 🧾 Publication

This work has been **published in Springer**:

- **Journal:** SN Computer Science Journal  
- **Paper Title:** *Recipe Recommendation System Using LLM*  
- **Submission ID:** SNCS-D-24-03268  
- **Authors:** Aaryan Kangte, Omprakash Choudhary, Rishabh Patil

---

## 👨‍💻 Team

- **Rishabh Patil**  
- **Aaryan Kangte**  
- **Omprakash Choudhary**  
- **Guide:** Prof. Pooja Vartak

---

## 📚 References

- [1] Rostami et al. (2023)
- [3] Freyne & Berkovsky (2020)
- [4] RecipeGPT (2020)
- [5] Ratatouille (2022)
- [6] Zero-shot Next-Item Recommendation (2023)
- [7] LLM-Based Item Description (2023)
- And many more as listed in the full project report

