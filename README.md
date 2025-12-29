
# Log Classification Using a Hybrid Framework

This project implements a hybrid log classification system that combines multiple complementary techniques to robustly classify log messages with varying levels of complexity and data availability.

The framework is designed to intelligently route log messages through different classification strategies based on their predictability and semantic complexity, ensuring both efficiency and accuracy.

---

## Classification Approaches

The system uses three layered classification strategies:

1. **Regular Expression (Regex)–Based Classification**:
   - Handles simple, well-defined, and predictable log patterns
   - Uses rule-based matching for fast and deterministic classification
   - Ideal for logs with consistent structure (e.g., known error formats)

2. **Sentence Transformer + Logistic Regression**:
   - Used when sufficient labeled training data is available
   - Converts log messages into dense semantic embeddings using Sentence Transformers
   - Applies Logistic Regression as the classification layer
   - Efficient and scalable for medium-to-large datasets

3. **LLM-Based Classification (Fallback)**:
   - Handles complex or ambiguous log patterns
   - Used when labeled data is insufficient or confidence from ML models is low
   - Leverages Large Language Models to infer semantic intent
   - Acts as a fallback or complementary classifier

![architecture](resources/arch.png)

---

## Folder Structure

.
├── training/
│   ├── regex_classifier.py
│   ├── train_embedding_model.py
│   └── train_logistic_regression.py
│
├── models/
│   ├── sentence_transformer/
│   └── logistic_regression.joblib
│
├── resources/
│   ├── sample_logs.csv
│   ├── outputs/
│   └── arch.png
│
├── server.py
├── requirements.txt
└── README.md

---

## Setup Instructions

1. **Install Dependencies**:
   Ensure Python is installed, then install required packages:

   ```bash
   pip install -r requirements.txt
   ```

2. **Run the FastAPI Server**:
   To start the server, use the following command:

   ```bash
   uvicorn server:app --reload
   ```

   Once the server is running, you can access the API at:
   - `http://127.0.0.1:8000/` (Main endpoint)
   - `http://127.0.0.1:8000/docs` (Interactive Swagger documentation)
   - `http://127.0.0.1:8000/redoc` (Alternative API documentation)

---

## Usage

Upload a CSV file to the API endpoint. The CSV must contain the following columns:
- `source`
- `log_message`

The API returns a CSV file with an additional column: `target_label`, the predicted classification label for each log entry

---

MIT License

Copyright (c) 2025 Om Ramani

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...

## Disclaimer

This project is intended for educational and portfolio purposes.
It is not an official production system.
