╔══════════════════════════════════════════════════════════════╗
║           RNN TEXT GENERATION — Step-by-Step Guide           ║
║         From Raw Corpus to Human-Readable Output             ║
╚══════════════════════════════════════════════════════════════╝

  This guide walks through every stage of an RNN text-generation
  pipeline, explaining what happens and why it matters.

──────────────────────────────────────────────────────────────
  STEP 1  │  Collect & Clean the Corpus
──────────────────────────────────────────────────────────────
  ▸ Gather a large text dataset.
  ▸ Remove extra whitespace, unwanted symbols, and fix casing.

  WHY  →  Garbage in, garbage out. Clean data = better learning.

──────────────────────────────────────────────────────────────
  STEP 2  │  Tokenize the Text
──────────────────────────────────────────────────────────────
  ▸ Split text into tokens — words, characters, or subwords.

  WHY  →  Models need discrete units; raw strings won't work.

──────────────────────────────────────────────────────────────
  STEP 3  │  Build Vocabulary & Token IDs
──────────────────────────────────────────────────────────────
  ▸ Collect every unique token into a vocabulary.
  ▸ Assign each token a numeric ID.

  WHY  →  Neural networks operate on numbers, not words.

──────────────────────────────────────────────────────────────
  STEP 4  │  Create Input-Output Training Pairs
──────────────────────────────────────────────────────────────
  ▸ Slide a fixed-length window across token IDs.
  ▸ Input  : sequence of context token IDs.
  ▸ Target : the very next token ID.

  EXAMPLE
    Input  →  [ "the",  "cat",  "sat" ]
    Target →    "on"

  WHY  →  This teaches the model next-token prediction.

──────────────────────────────────────────────────────────────
  STEP 5  │  Convert Token IDs to Embeddings
──────────────────────────────────────────────────────────────
  ▸ Pass token IDs through an Embedding layer.

  WHY  →  Embeddings map sparse IDs to dense semantic vectors.

──────────────────────────────────────────────────────────────
  STEP 6  │  Pass Embeddings Through RNN / LSTM / GRU
──────────────────────────────────────────────────────────────
  ▸ Feed the embedding sequences into a recurrent layer.

  WHY  →  Recurrent layers capture sequence order and context.

──────────────────────────────────────────────────────────────
  STEP 7  │  Train the Model
──────────────────────────────────────────────────────────────
  ▸ Predict the next token at every time step.
  ▸ Compute cross-entropy loss; backpropagate gradients.

  WHY  →  Training nudges predictions toward the true next token.

──────────────────────────────────────────────────────────────
  STEP 8  │  Start Generation with a Seed Prompt
──────────────────────────────────────────────────────────────
  ▸ Provide initial words, e.g. "once upon a".

  WHY  →  The seed gives the model a starting context to build on.

──────────────────────────────────────────────────────────────
  STEP 9  │  Generate Tokens Iteratively
──────────────────────────────────────────────────────────────
  ▸ Predict next token → append → feed back → repeat.

  WHY  →  Each loop step extends the output by one token.

──────────────────────────────────────────────────────────────
  STEP 10 │  Decode Token IDs Back to Words
──────────────────────────────────────────────────────────────
  ▸ Convert the predicted token ID sequence into readable text.

  WHY  →  Produces the final human-readable generated output.

══════════════════════════════════════════════════════════════
  PIPELINE AT A GLANCE
══════════════════════════════════════════════════════════════

  Corpus
    │
    ▼
  Clean  ──▶  Tokenize  ──▶  Token IDs  ──▶  Input/Target Pairs
                                                      │
                                                      ▼
                                               Embedding Layer
                                                      │
                                                      ▼
                                            RNN / LSTM / GRU
                                                      │
                                                      ▼
                                                   Train
                                                      │
                                                      ▼
                                               Seed Prompt
                                                      │
                                                      ▼
                                          Predict Next Token (loop)
                                                      │
                                                      ▼
                                            Decode to Text  ✓