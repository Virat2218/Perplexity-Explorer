# Perplexity Explorer

An interactive, in-browser educational tool to explore and understand how language models measure predictability, surprise, and perplexity.

Built with **HTML, CSS, and plain JavaScript** inside a single file (`index.html`), running a real language model directly inside the browser using [Transformers.js](https://huggingface.co/docs/transformers.js). No backend, no API key, and no external frameworks required.

---

## Features

- **Section 1: Interactive Sentence Input**
  - Type any custom sentence or choose from quick sample presets.
  - Automatically loads and runs `Xenova/distilgpt2` (quantized `q8`) locally via WebAssembly / WebGPU in the browser upon first calculation.
  - Prepends token ID `50256` (`<|endoftext|>`) as the start marker to compute the initial word's probability.
  - Implements numerically stable softmax (`logits - max(logits)`).

- **Section 2: Token Probabilities & Perplexity Breakdown**
  - Detailed table showing token index `#`, decoded token (spaces clearly visualized with `␣`), probability $P$, and inverse probability $1/P$.
  - Three clear educational steps:
    - **Step 1**: Multiplication of all $1/P$ branching factors.
    - **Step 2**: Total number of tokens $N$.
    - **Step 3**: Perplexity $(\text{product})^{1/N}$, computed with numerically stable log-sums: $\exp\left(\frac{1}{N}\sum -\ln P\right)$.

- **Section 3: Next Token Predictions**
  - Analyzes the model's logits at the final token position.
  - Renders horizontal probability bars for the top 8 predicted next tokens, highlighting the #1 top candidate.

- **Section 4: Try It by Hand (Simulation)**
  - Experiment with custom tokens and probabilities in real time.
  - Add or remove tokens dynamically.
  - Built-in presets:
    - *“I love Python”* ($0.5, 0.8, 0.2$) → Perplexity **2.32**
    - *“All 1/8”* ($8$ tokens at $0.125$ each) → Perplexity **8.00**
    - *“One surprising word”* ($0.9, 0.9, 0.9, 0.01$) → Perplexity **3.42**

---

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/Virat2218/Perplexity-Explorer.git
   cd Perplexity-Explorer
   ```

2. Open `index.html` in your browser:
   - On macOS:
     ```bash
     open index.html
     ```
   - Or serve with Python:
     ```bash
     python3 -m http.server 8000
     ```
     and open `http://localhost:8000`.

---

## License

MIT
