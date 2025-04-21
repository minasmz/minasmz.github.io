---
layout: post
title: "Enhancing Graph Recognition with Gemini: Fine-Tuning for Hamiltonian Path Detection"
date: 2025-04-20
categories: projects ai machine-learning
---
# Enhancing Graph Recognition with Gemini: Fine-Tuning for Hamiltonian Path Detection

## Introduction

As part of my Google Generative AI Capstone Project, I tackled an interesting challenge: teaching multimodal models to accurately identify whether a graph is Hamiltonian. The Hamiltonian path problem is a classic NP-complete problem in graph theory, where we need to determine if a graph contains a path that visits each vertex exactly once.

Using Google Cloud Vertex AI, I fine-tuned Gemini 2.0 Flash to significantly improve its ability to analyze graph images and make accurate determinations about their Hamiltonicity properties.

While modern large multimodal models like Gemini can "see" graphs as images, they often lack the specialized knowledge needed to make accurate determinations about complex properties like Hamiltonicity. This project demonstrates how fine-tuning can significantly improve model performance on specialized tasks.

## The Challenge

Determining whether a graph is Hamiltonian is computationally difficult - it belongs to the class of NP-complete problems, which are notoriously challenging to solve efficiently. For humans and AI systems alike, this requires both visual understanding of the graph structure and the application of specialized graph theory knowledge.

My initial testing with the base Gemini 2.0 Flash model revealed a significant limitation: it classified all test graphs as Hamiltonian, regardless of their actual properties. This highlighted the need for specialized training.

## Project Workflow

My approach to solving this problem consisted of five key steps:

### 1. Setting Up Google Cloud Authentication

First, I established the necessary infrastructure by:
- Creating a service account in Google Cloud with appropriate permissions
- Downloading and configuring credential files
- Verifying authentication with the Cloud Storage client

### 2. Converting Images and Captions to JSONL Format

To prepare data for fine-tuning, I:
- Organized a dataset of graph images paired with accurate captions describing Hamiltonicity
- Uploaded images to Google Cloud Storage
- Created training and validation datasets in the required JSONL format
- Split the data with 80% for training and 20% for validation

### 3. Evaluating the Base Model

Before fine-tuning, I tested the baseline "gemini-2.0-flash-001" model on several graph images. For these tests, I used a structured prompt approach that requested the model to output its analysis in JSON format with specific keys for 'description' and 'is_hamiltonian' (a boolean value). This structured output approach made it easier to systematically evaluate the model's performance.

The results showed:
- Two Hamiltonian graphs (correctly identified)
- Two non-Hamiltonian graphs (incorrectly identified as Hamiltonian)

This baseline test confirmed my suspicion that the model lacked the specialized knowledge to accurately determine Hamiltonicity, as it tended to classify all graphs as Hamiltonian regardless of their actual properties.

### 4. Fine-Tuning the Model

Using Google Cloud Vertex AI's tuning capabilities, I:
- Used my prepared JSONL datasets to fine-tune the gemini-2.0-flash-001 base model
- Configured appropriate learning parameters (learning rate multiplier of 1.0 and adapter size of 1)
- Monitored the training job through completion in the Vertex AI platform

The fine-tuning process ran for several hours in the cloud, resulting in a custom model specifically trained to analyze graph images and determine Hamiltonicity. By leveraging Vertex AI's infrastructure, I was able to efficiently train the model without requiring extensive local computing resources.

### 5. Evaluating the Fine-Tuned Model

After fine-tuning, I tested the model on the same four test graphs:
- The model correctly identified both Hamiltonian graphs
- **Critically, it now correctly identified the non-Hamiltonian graphs**, which the base model had misclassified

## Results and Insights

The results demonstrate the power of specialized fine-tuning for complex domain-specific tasks:

1. **Improved Accuracy**: The fine-tuned model correctly classified all test cases, compared to the base model's 50% accuracy.

2. **Domain Adaptation**: Through fine-tuning, we effectively transferred specialized graph theory knowledge to a general-purpose vision-language model.

3. **NP-Complete Problem Solving**: This approach shows promise for using AI to help with challenging computational problems.

## Technical Implementation

The project leveraged several key technologies:
- **Google Cloud Platform**: For authentication, storage, and Vertex AI services
- **Vertex AI**: For fine-tuning and hosting the model
- **Python**: For data preparation, model interaction, and evaluation
- **Pandas and Matplotlib**: For data manipulation and visualization

## Conclusion

This project demonstrates how general-purpose multimodal models can be effectively fine-tuned to perform specialized tasks requiring domain expertise. By providing a targeted dataset of graph images with accurate Hamiltonicity classifications, we transformed a model that initially struggled with this NP-complete problem into one that can make accurate determinations.

The implications extend beyond this specific application - this approach could be applied to many other specialized visual recognition tasks where domain expertise is traditionally required. As generative AI continues to evolve, fine-tuning represents a powerful strategy for adapting these general models to specific, complex domains.

## Future Directions

Some promising directions for extending this work include:
- Expanding to other NP-complete graph problems (vertex cover, graph coloring, etc.)
- Creating larger, more diverse training datasets
- Comparing performance across different model architectures and sizes
- Developing interactive tools that can help visualize why a graph is or isn't Hamiltonian

---

*This project was completed as part of the Google Generative AI Capstone Project, 2025.*
