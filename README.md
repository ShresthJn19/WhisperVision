# 🧠 WhisperVision — Real-Time Lip Reading from Silent Video

WhisperVision is a deep learning pipeline that reads lips and predicts spoken sentences using only silent video input. Built using 3D CNNs, BiLSTMs, and CTC decoding, this system enables voice-free communication, real-time inference, and silent speech recognition — no audio needed.

---

## 📦 Dataset

- **Source**: GRID corpus (publicly available lip-reading dataset)
- **Format**: Video clips (`.mpg`) with sentence-level annotations (`.align`)
- **Structure**:
  - Each video: 75 frames, grayscale, cropped to mouth region
  - Each label: Cleaned, character-level transcription of spoken sentence

---

## 🧱 Model Architecture

| Layer              | Details                             |
|-------------------|-------------------------------------|
| Input              | 75 grayscale frames per sequence    |
| 3D Conv Blocks     | Spatial-temporal feature extraction |
| Bi-directional LSTM| Sequence modeling                   |
| Dense + Softmax    | Character probabilities             |
| CTC Loss           | Alignment-free transcription        |

- **Loss**: Connectionist Temporal Classification (CTC)
- **Decoder**: Greedy CTC decoding (`ctc_decode`)

---

## 🧪 Evaluation

| Metric | Score  |
|--------|--------|
| CER    | 22%    |
| WER    | 41%    |

- Tested on ~300 sentence-level samples  
- Evaluated using edit distance between ground truth and predicted transcription

---

## 🔧 Tech Stack

- Python, TensorFlow  
- OpenCV, NumPy  
- Streamlit (for web app)  
- ImageIO, EditDistance

---

## 🛠 Project Structure

```
📁 dataset/
    ├── videos/         # Silent input videos
    └── alignments/     # Sentence-level transcriptions

📁 model/
    └── saved_model/    # Trained weights

📁 utils/
    ├── utils.py        # Preprocessing functions
    ├── model_utils.py  # Model builder and decoder
    └── app.py          # Streamlit frontend (upload + prediction)

📄 whispervision.ipynb  # Training & Evaluation notebook
```

---

## 🚀 Inference Pipeline

1. 📥 Upload silent video (`.mpg`)
2. 🎥 Preprocess & extract 75 frames
3. 🧠 Feed into trained model
4. 🧾 Decode output characters (CTC)
5. ✅ Display predicted sentence in real time

---

## 🌐 Streamlit App

Run the app locally:

```bash
streamlit run app.py
```

Upload any silent `.mpg` video from GRID dataset and see the real-time transcription.

---

## 💡 Use Cases

- Voice-free communication in noisy or secure environments  
- Speech-to-text accessibility for hearing-impaired users  
- Silent surveillance & lip-reading systems  
- Multimodal NLP/vision research

---

## 🧪 Error Metrics Explained

**CER (Character Error Rate)**  
Measures the percentage of characters incorrectly predicted, including insertions, deletions, and substitutions.

```
CER = (Substitutions + Insertions + Deletions) / Total Characters
```

Used for fine-grained accuracy on character-level predictions.

**WER (Word Error Rate)**  
Measures the percentage of words incorrectly predicted — similar to CER but at the word level.

```
WER = (Substitutions + Insertions + Deletions) / Total Words
```

Useful for evaluating overall sentence readability and semantic accuracy.

---

### 🔍 Example:
Ground Truth: “please set the channel”  
Predicted  : “please set the channil”

- CER = 1 error / 21 chars = ~4.8%  
- WER = 1 error / 4 words = 25%
