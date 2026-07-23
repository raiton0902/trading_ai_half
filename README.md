# 📈 Custom AI Trading Assistant (Phi-3 LoRA Fine-Tuning)

A complete pipeline to build, fine-tune, and deploy a personalized AI Trading Assistant. This project takes a base Large Language Model (Microsoft's Phi-3-Mini) and trains it on your personal historical trading data (JSONL) using LoRA (Low-Rank Adaptation). 

The result is an interactive, daily trading copilot that analyzes live chart setups strictly through the lens of your unique trading edge.

## ✨ Features
* **Interactive Data Collector:** Built-in Jupyter UI widgets to seamlessly log new trading setups (entry, stop loss, take profit, indicator conditions) directly into your dataset.
* **T4 GPU Optimized:** Engineered to run perfectly on Google Colab's free tier. Uses 4-bit quantization (`bitsandbytes`) to shrink the model footprint.
* **Hardware Crash Protections:** Includes custom memory-scrubbing scripts to bypass `BFloat16` math errors natively found on older T4 architectures.
* **Anti-Hallucination Guardrails:** Strict generation parameters (low temperature, explicit stop tokens) ensure the AI outputs cold, calculated trading logic without rambling.
* **Daily Scanner UI:** A clean, button-driven interface to input live Bybit chart setups and receive instant confluence from your trained model.

## 🛠️ Tech Stack
* **Language:** Python
* **AI/ML Libraries:** PyTorch, Hugging Face `transformers`, `peft` (LoRA), `trl` (SFTTrainer), `bitsandbytes`
* **Environment:** Jupyter Notebook / Google Colab
* **UI:** `ipywidgets`

## 🚀 Getting Started

### Prerequisites
1. A Google Account (to use Google Colab and Google Drive).
2. A basic understanding of your own trading rules (e.g., Stochastic crosses, chart patterns).
3. A `your_trades.jsonl` file containing your historical setups (or use the built-in form to create one!).

### Setup Instructions
1. Upload the `trading_ai_finetune.ipynb` notebook to Google Colab.
2. Upload your `your_trades.jsonl` file to your Google Drive (root folder, or update the path in the code).
3. Open the notebook and run **Cell 1** to install all required dependencies and connect your Google Drive.

## 📖 How to Use

The notebook is divided into three distinct phases:

### Phase 1: Data Collection & Preparation
Use the interactive form block to input your trading setups. The code automatically validates your inputs (checking for Entry, SL, and TP) and appends them safely to your Google Drive dataset.

### Phase 2: The Training Room
Run the training cells sequentially. The code will:
1. Download Microsoft's `Phi-3-Mini-4k-Instruct`.
2. Compress it to 4-bit precision.
3. Sanitize the model of rogue BFloat16 buffers to prevent PyTorch GradScaler crashes.
4. Fine-tune the LoRA adapters on your specific dataset.
5. Save the customized model back to your Google Drive.

### Phase 3: Live Daily Scanning
Once trained, use the final cell to launch the **Daily AI Trading Assistant UI**. 
Type your live market observations (e.g., *"Exotic alt, stochastic %K cross above %D on daily, Ascending triangle..."*) into the text box, click **Analyze Trade**, and receive instant, personalized confluence.

## 🗺️ Future Roadmap
- [ ] **Automated Screener:** Connect to the Bybit API via `ccxt` to auto-fetch live ticker data and feed it to the model.
- [ ] **Vision Integration:** Upgrade from `Phi-3-Mini` to `Phi-3-Vision` to allow the model to ingest raw chart screenshots instead of text prompts.

## ⚠️ Disclaimer
**This project is for educational and experimental purposes only.** The AI is entirely blind to live macroeconomic data and black-swan events. It operates solely on the text parameters provided to it. Never execute trades blindly based on AI output. Always use strict risk management.
