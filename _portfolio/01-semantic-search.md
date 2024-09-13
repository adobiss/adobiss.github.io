---
layout: single
title: "Advanced Music Metadata Matching: Leveraging NLP for Semantic Search in the Music Industry"
permalink: /projects/semantic-search
---

**GitHub:** [](https://github.com/)

## Project Overview

Developed a cutting-edge semantic matching system for music metadata, addressing the challenge of identifying and linking related musical compositions across varying formats and spellings. This project demonstrates proficiency in data science, machine learning and software engineering principles.

## Key Achievements

- Improved model accuracy from **40%** to **97%** through iterative development and fine-tuning
- Implemented a robust data cleaning pipeline for a real-world, inconsistent dataset
- Successfully applied state-of-the-art NLP models (BERT, Sentence-BERT) to a domain-specific problem
- Achieved high accuracy **(97%)** with minimal fine-tuning data **(1,000 samples)**, showcasing efficient domain adaptation

## Technical Skills Showcased

- **Programming:** Python, Pandas, NumPy
- **Machine Learning:** PyTorch, BERT, Sentence-BERT, FAISS
- **Data Analysis:** Exploratory Data Analysis (EDA), data cleaning, feature engineering
- **Development:** Jupyter Notebooks, VSCode, conda, modular code design

## Project Highlights

### Sophisticated Data Preparation
- Conducted thorough EDA to uncover and address data corruption and inconsistencies
- Implemented dynamic encoding to handle multiple character encodings within the dataset
- Developed flexible, reusable cleanup functions for efficient data processing

### Advanced Model Implementation and Optimisation
- Initial implementation: BERT Base Uncased (40% accuracy)
- Improved model: Sentence-BERT (88% accuracy)
- Fine-tuned model: Customised Sentence-BERT (97% accuracy)

### Innovative Problem-Solving Approaches
1. **Fail Fast Methodology:** Rapidly implemented PoC to gather practical feedback and iterate quickly
2. **Strategic Framework Selection:** Chose PyTorch for PoC flexibility, with modular design for potential transition to TensorFlow in production
3. **Efficient Fine-Tuning Strategy:** Utilised specialised loss function for fine-tuning with only positive pairs, achieving significant accuracy boost with minimal data

## Key Decisions and Rationale

- **Framework Selection (PyTorch vs TensorFlow):** Opted for PyTorch due to its flexibility and prototyping speed, while implementing modular code design to facilitate potential future transition to TensorFlow for production scaling.

- **Model Evolution:** Transitioned from BERT Base Uncased to Sentence-BERT based on performance analysis and understanding of embedding pooling strategies for sentence-like structures.

- **Fine-Tuning Approach:** Implemented a minimal viable training sample (1,000 pairs) for PoC, demonstrating the power of transfer learning in domain adaptation with limited data.

## Forward-Thinking Architecture

Implemented "Flexibility Strategies" from the project's inception to ensure scalability and ease of transition:

- Modular code design with clear interfaces between components
- Framework-agnostic practices using standard data processing libraries
- Abstract data access layer for encapsulated data handling
- Configuration management for easy parameter tuning
- Basic data version control for maintaining data integrity

## Learnings and Insights

- The critical importance of thorough data validation in real-world datasets
- The power of transfer learning in achieving high performance with minimal domain-specific data
- The value of balancing quick PoC development with considerations for future scalability

## Future Enhancements

- Implement robust data version control for organised training experimentation
- Analyse false match similarity score distribution to understand unexpected central tendency around 60%
- Conduct more rigorous training, evaluation and testing with proper stratification to further improve accuracy
- Develop and deploy a web application prototype to demonstrate real-world applicability of the solution
- Implement secondary applications of the model, such as automated duplicate entry detection in large music catalogs

This project showcases my ability to tackle complex, real-world data challenges, implement and optimise state-of-the-art machine learning models and design scalable, forward-thinking solutions. It demonstrates my proficiency in data science, machine learning and software engineering principles, making me well-equipped to contribute to challenging projects in AI and data-driven industries.

This system could significantly streamline royalty collection and music catalogue management by automating metadata matching use-cases previously carried out manually and surfacing duplicate entries that would previously go unnoticed.
