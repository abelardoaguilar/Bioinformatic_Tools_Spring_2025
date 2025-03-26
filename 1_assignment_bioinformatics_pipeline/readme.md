# Assignment: Investigating Mystery Sequences

In this assignment, you'll practice creating reproducible bioinformatics pipelines to characterize unknown biological sequences. The tasks are divided into two main parts:

1. **Sequence Analysis:** Investigate sequence properties, predict functions, organisms of origin, and explore evolutionary relationships (Jupyter Notebook).
2. **Structure Analysis:** Predict protein structures manually (using AlphaFold), then analyze and compare these structures computationally (Chimera script, `.cxc` or `.py`).

Remember: Bioinformatics pipelines are rarely perfect on the first try—iteration and incremental improvement are key. Start small, progress gradually, and integrate your results as you go.

---

> ### ⚠️ **Note about viewing this README file:**  
> Always open and view this file using software capable of rendering markdown (e.g., VSCode, Google Colab, or markdown viewers). Viewing in a basic text editor will make formatting confusing and your assignment harder than necessary!

---

## 📌 Assignment Goals

You will start with nucleotide sequences provided by the instructors (`sequences.fna`). Your main deliverables are:

- One Jupyter Notebook (`sequence_analysis_pipeline.ipynb`)
- One Chimera script (`structure_analysis_pipeline.cxc` or `.py`)
- A short summary report
- A README file documenting your pipeline clearly for reproducibility

---

## 🔸 Part 1: Sequence Analysis (Jupyter Notebook)

### Suggested Workflow:

1. **Load sequences** into Python as objects.
   - **Objects you'll likely use**: `SeqRecord`, lists of sequences, strings (`BioPython`).

2. **Compute basic properties** (sequence length, GC content).
   - **Objects you'll likely use**: Numeric variables (`int`, `float`), pandas DataFrames for structured data.

3. **Translate nucleotide sequences** into proteins.
   - **Objects you'll likely use**: BioPython `Seq` and `SeqRecord` objects.

4. **Perform alignments** at nucleotide and protein levels.
   - **Objects you'll likely use**: Alignment objects, files in FASTA format.

5. **Construct phylogenetic trees** and visualize them.
   - **Objects you'll likely use**: Phylogenetic tree objects (`BioPython Phylo`).

6. **Predict functions and organisms** with BLAST and HMM searches.
   - **Objects you'll likely use**: Results as pandas DataFrames or CSV files.

### Simple pseudocode example:

```plaintext
Load nucleotide sequences into Python
|
|--> Calculate length and GC content (store in tables/dataframes)
|--> Translate sequences into proteins (store as new sequence objects)
|--> Perform alignments (generate alignment files)
|--> Construct and visualize phylogenetic trees (tree objects and images)
|--> Predict functions and organism origin (generate prediction tables)
```

---

## 🔸 Part 2: Structure Analysis (Chimera Script)

This part involves structure-based analysis. First, manually predict protein structures with **AlphaFold**, then analyze them in Chimera.

### Steps to follow:

1. **Predict protein structures manually (AlphaFold)**:
   - Manually upload amino acid sequences to the AlphaFold webserver.
   - Download resulting structure files (`.pdb` or `.cif`).

2. **Analyze predicted structures in Chimera**:
   - Load structures into Chimera.
   - Identify structural homologs (using `Foldseek`, AFDB in UniProt, etc.).
   - Align structures and visualize results.
   - Document and save visualizations, alignments, and results tables clearly.

### Example pseudocode for Chimera:

```plaintext
Upload amino acid sequences to AlphaFold server
Download predicted structure files (.pdb/.cif)
|
|--> Load structures into Chimera
|--> Identify structural homologs
|--> Perform structural alignments
|--> Save visualizations (.png) and alignment files clearly
```

---

## 📁 Expected Folder Structure (think of it as a file tree):

```bash
assignment_1_last_name/
|
|–– readme.md
|–– report_last_name.docx
|–– report_last_name.pdf
|
|–– data/
|   ├── sequences.fna                        # Instructor-provided nucleotide sequences
|   └── folded_proteins/
|       └── sequence_ID/
|           └── sequence_ID.pdb (or .cif)    # Alphafold-predicted structures
|
|–– bin/
|   ├── sequence_analysis_pipeline.ipynb     # Your Jupyter Notebook for sequence analysis
|   └── structure_analysis_pipeline.(cxc or py) # Your Chimera script for structural analysis
|
└── results/
    ├── sequence_properties/
    |   ├── properties.csv                   # Length and GC content per sequence (DataFrame)
    |   ├── lengths.png                      # Length plot
    |   ├── gc_content.png                   # GC content plot
    |   └── sequences_translated.faa         # Translated protein sequences (FASTA)
    |
    ├── alignments/
    |   ├── sequence_alignments_nucleotide.fna
    |   ├── sequence_alignments_proteins.faa
    |   └── sequence_similarities.csv        # Similarity matrix (table/DataFrame)
    |
    ├── phylogenetic_tree/
    |   ├── tree_nucleotides.nwk
    |   ├── tree_nucleotides_visualization.png
    |   ├── tree_proteins.nwk
    |   └── tree_proteins_visualization.png
    |
    ├── functional_prediction/
    |   ├── domain_predictions.csv           # Domains detected per sequence
    |   └── sequence_ID/                     # Additional details per sequence
    |
    ├── organism_origin/
    |   ├── organism_prediction.csv          # Predicted organism per sequence
    |   └── sequence_ID/                     # Supporting BLAST results
    |
    ├── predicted_structures_visualizations/
    |   └── sequence_ID_structure_visualization.png
    |
    ├── structural_homology/
    |   └── homology_predictions.csv         # Structural homologs found (table)
    |
    └── pair_homology/
        ├── pair_homology_predictions.csv    # Pairwise structural similarity matrix
        └── pair_comparisons/                # Detailed structural comparison results
```

---

## 📖 Recommended Initial Code Block (for Google Colab):

To avoid issues with file paths, start with this interactive and user-friendly way to load your sequences file:

```python
# Install and import required libraries
!pip install biopython
from Bio import SeqIO
from google.colab import files

# Upload your sequences file interactively:
uploaded = files.upload()  # select sequences.fna from your computer

# Get the name of your uploaded file
filename = list(uploaded.keys())[0]

# Load sequences into a Python object
sequences = list(SeqIO.parse(filename, "fasta"))

# Your sequences are now ready for analysis!
print(f"You successfully loaded {len(sequences)} sequences.")
```

This code snippet lets you easily select and load your input file without worrying about complicated file paths.

---

## 📌 Helpful hints about Python objects you'll encounter:

- **Strings (`str`)**: Individual nucleotide/amino acid sequences.
- **Lists (`list`)**: Collections of sequences.
- **BioPython `SeqRecord` objects**: Convenient sequence representation with metadata.
- **Pandas DataFrames (`pd.DataFrame`)**: Structured tables for analysis results.
- **Numeric types (`int`, `float`)**: For numerical calculations (e.g., GC%, lengths).
- **Alignment objects**: Represent alignments from sequences.
- **Phylogenetic Tree objects (`Phylo`)**: For visualizing relationships between sequences.

If you're unsure about your next steps, always reflect:

- "What is the current object I have?"
- "What am I trying to achieve?"
- "How can I convert or transform this object to reach the next step?"

---

## 📝 Final Short Report (Summary):

A brief (<500 words) report clearly answering:

- **Function:** Likely biological functions of your sequences?
- **Origin:** Possible organisms these sequences originate from?
- **Relationships:** Are these sequences related (phylogenetically or structurally)?

Include clear, concise figures as evidence when helpful.

---

## 🚩 **Final Reminder on Markdown Files:**
Use a markdown viewer (like VSCode or Google Colab) to open this file clearly. Viewing it as plain text will likely make you suffer more unnecessarily!

---

**Enjoy the exploration! Remember, bioinformatics is best done progressively, step by step. Don't worry if you're initially unsure—it's all part of the journey!**
