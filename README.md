
# VLM — Ollama OCR Notebook

This repository centers on the `Ollama_OCR.ipynb` notebook, which demonstrates image-to-text workflows using local vision-language models (via Ollama) and classical OCR tools. The README below summarizes how to reproduce the notebook examples, set up Ollama, and run the provided `OCRProcessor` example.

## Quick Highlights

- Primary artifact: `Ollama_OCR.ipynb` (notebook-driven demos and examples)
- Uses local Ollama models for vision-language processing plus optional Tesseract for fallback OCR
- Example helper: `ollama_ocr.OCRProcessor` (used in the notebook for image processing)

## Notebook-specific setup (from `Ollama_OCR.ipynb`)

- Install Ollama (run in terminal):

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

- Start the local Ollama server:

```bash
ollama serve
```

- The notebook also uses `colab-xterm` to open a terminal in the notebook environment (optional):

```bash
pip install colab-xterm
# then in a notebook cell: %load_ext colabxterm  and  %xterm
```

## Recommended models (notebook examples)

The notebook references several vision-language models you can pull with Ollama:

- `llama3.2-vision:11b` — higher-accuracy model for complex documents
- `granite3.2-vision` — efficient model focused on document understanding
- `moondream` — smaller, edge-friendly VLM
- `minicpm-v` — supports large images and varied aspect ratios

Pull examples shown in the notebook:

```bash
ollama pull llama3.2-vision:11b
ollama pull granite3.2-vision
ollama pull moondream
ollama pull minicpm-v
```

## Requirements

- Python 3.8+ recommended
- Jupyter or JupyterLab to open and run `Ollama_OCR.ipynb`
- Ollama CLI and `ollama serve` running locally for VLM interactions
- Optional system OCR: `tesseract-ocr` (install via your OS package manager)

Suggested Python packages (add to `requirements.txt`):

```
jupyter
numpy
pandas
Pillow
opencv-python
pytesseract
colab-xterm
requests
# torch (optional if using PyTorch-based models locally)
```

If the notebook imports or uses a local helper module named `ollama_ocr`, ensure that package/module is available in the notebook environment (either installed in the active venv or present in the repo).

## Example usage (from the notebook)

This snippet shows how the notebook initializes the `OCRProcessor` and runs it against an image:

```python
from ollama_ocr import OCRProcessor

# Initialize OCR processor with the selected model
ocr = OCRProcessor(model_name='llama3.2-vision:11b')  # or granite3.2-vision, moondream, minicpm-v

result = ocr.process_image(
	image_path='data/your_image.jpg',
	format_type='text',        # options: markdown, text, json, structured, key_value
	custom_prompt='Extract all text, focusing on dates and names.',
	language='English'
)

print(result)
```

## Running the notebook

Start Jupyter and open the notebook:

```bash
jupyter lab
# or
jupyter notebook
```

Open `Ollama_OCR.ipynb` and run cells top-to-bottom. The top cells include setup commands and instructions for pulling models and starting a terminal in the notebook.

## Configuration notes

- Data paths: point to images in a `data/` folder or use absolute paths in the notebook.
- Ollama: run `ollama serve` and ensure the notebook environment can reach the server (same machine / container network).
- Model selection: change the `model_name` passed to `OCRProcessor` based on the models you pulled.

## Next steps I can do for you

- Generate a `requirements.txt` based on the notebook imports.
- Add an example image to `data/` and a short demo script to run outside the notebook.
- Expand the README with exact environment variable names or troubleshooting steps for `ollama serve`.

