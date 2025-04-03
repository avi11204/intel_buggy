# intel_buggy

# Bug Detection and Fixing Model

## Overview
This project implements a **Bug Detection and Fixing Model** using a **T5 Transformer Model** to identify and correct errors in source code. The model is trained on the **Krish-05/bug-detection-and-fixing** dataset and deployed using **FastAPI** with Ngrok for remote access.

## Features
- **Automatic Bug Detection**: Identifies errors in given source code.
- **Code Correction**: Suggests and applies fixes to detected issues.
- **FastAPI API**: Provides a web interface for model interaction.
- **Ngrok Deployment**: Enables public access to the API.

## Dataset
The dataset consists of pairs of buggy and corrected code snippets. It contains:
- `original_code`: The buggy code.
- `modified_code`: The corrected code.
- Additional metadata such as `changed_line`, `line_number`, and `mutation_type`.

## Model
- **Architecture**: T5 (Text-to-Text Transfer Transformer)
- **Preprocessing**: Tokenization using Hugging Face `T5Tokenizer`.
- **Training**: Fine-tuned on the dataset for code correction.
- **Inference**: Generates corrected code for a given input.

## Installation
1. Clone the repository:
   ```sh
   git clone https://github.com/your-username/bug-fixer.git
   cd bug-fixer
   ```
2. Install dependencies:
   ```sh
   pip install -r requirements.txt
   ```
3. Run the API:
   ```sh
   uvicorn app:app --host 0.0.0.0 --port 8000
   ```
4. Start Ngrok (if needed):
   ```sh
   ngrok http 8000
   ```

## API Endpoints
- **GET /** - Check if the model is running.
- **GET /accuracy** - Retrieve model accuracy.
- **POST /predict** - Submit buggy code and receive corrected output.

## Example Usage
Make a request to the API:
```sh
curl -X POST "http://localhost:8000/predict" -H "Content-Type: application/json" -d '{"code": "def sum(a, b) return a + b"}'
```
Response:
```json
{
  "fixed_code": "def sum(a, b): return a + b"
}
```

## Deployment
To make the API publicly accessible, use **Ngrok**:
```sh
ngrok http 8000
```
This will provide a public URL like:
```
https://random-id.ngrok-free.app
```

## Evaluation
- **Metric Used**: Exact Match Accuracy
- **Current Accuracy**: `0.00%` (likely due to model output issues)
- **Predictions Issue**: Model returns empty outputs (`''`), requiring debugging.

## Known Issues & Future Improvements
- **Improve Tokenization**: Ensure correct input formatting before inference.
- **Optimize Model Inference**: Fix CUDA memory errors and ensure proper device handling.
- **Data Augmentation**: Enhance training dataset with more diverse samples.
- **Better Accuracy Calculation**: Use BLEU or CodeBLEU scores instead of exact match.



![Screenshot 2025-04-03 195456](https://github.com/user-attachments/assets/d10cfced-074f-4e43-8077-fd8b2667e61b)

![Screenshot 2025-04-03 195540](https://github.com/user-attachments/assets/ec80e75c-bf88-4598-bf58-531ddf3ad4ea)
