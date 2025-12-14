# The Smith-Fibonacci Coordinate Project
### *A Computational Verification of the Fibonacci-Mersenne Coordinate Conjecture*

**Current Version:** Pattern Hunter 3.2  
**Status:** Active Research / Data Collection  
**Lead Researcher:** Joshua Smith

---

## 🧪 The Scientific Discovery

This repository documents the algorithms and raw data supporting the **Smith-Fibonacci Coordinate Conjecture**. 

**The Hypothesis:**  
The Fibonacci Sequence ($F_n$) functions as a coordinate system for structural stability within the Collatz Conjecture. By analyzing a Fibonacci number as a vector of two components—**Head** (leading digits) and **Tail** (trailing digits)—we can predict precise entry points into the Collatz map that yield structurally significant results.

### The Four Observed Laws

Computational analysis of integers up to $10^{10}$ (Indices $F_1$ to $F_{48}$) has confirmed four distinct behaviors:

1. **The Law of Structural Squares (Even Indices):** When $n$ is Even (e.g., $F_{12}, F_{20}, F_{36}$), the corresponding Collatz Key often forms a **Perfect Square** or acts as a "Pillar" (Peak = Start).
2. **The Law of Recursive Distance (Prime/Odd Indices):** When $n$ is Odd or Prime (e.g., $F_{14}, F_{23}$), the Key is found at a distance ($|c - F_n|$) that mirrors the digits of the index or target itself.
3. **The Law of Harmonic Echoes:** Keys appear at harmonic intervals relative to the target (e.g., $1x$, $2x$, or $\approx \frac{1}{3}x$).
4. **The Zero-Point Anomaly:** At high-order "Structural" indices (like $F_{36}$ and $F_{48}$), we observe matches with **Zero Offset**, where the Collatz Number $c$ is also the exact Mersenne Index $n$.

### 🏆 Hall of Fame: Key Artifacts

| Index | Value ($F_n$) | Key Match ($c$) | Distance | Significance |
|:------|:--------------|:----------------|:---------|:-------------|
| **F12** | 144 | 144 | 0 | **Perfect Square Peak** ($12^2$) |
| **F24** | 46,368 | 46,344 | **24** | Distance matches Index (Recursive) |
| **F26** | 121,393 | 26,987 | 26... | Peak is **Palindrome** ($121012$) |
| **F31** | 1,346,269 | 449,805 | $\approx \frac{1}{3} F_{31}$ | **Mersenne Prime** Harmonic Link |
| **F36** | 14,930,352 | 14,746,127 | Harmonic | **Zero-Point Match** (Offset 0) |
| **F48** | 4.8 Billion | 4.807 Billion | 34,848 | **Pillar Match** (Peak = Start) & Distance $\propto 48$ |

---

## 🛠 Software Architecture: Pattern Hunter 3.2

The **Pattern Hunter** is a high-performance Python engine designed to search billions of integers for these specific "Needle in a Haystack" coordinates.

### Core Features

- **Mersenne-First Optimization:** Uses $O(1)$ logarithmic checks to filter Mersenne candidates *before* calculating the expensive Collatz path. This yields a **100x-1000x speedup** over linear searching.
- **Multiprocessing Core:** Automatically spawns workers across all available CPU cores (tested on 16+ cores).
- **Dual Modes:** Support for surgical "Single Hunts" or unattended "Auto-Batch" processing.
- **Multi-Directory Support:** Organize research data into separate directories (fibonacci_logs, mersenne_logs, custom).
- **Searchable Log Files:** Descriptive filenames encode all search parameters for easy discovery.
- **Data Serialization:** Outputs both human-readable logs (`.log`) and machine-parsable JSON (`.json`) for statistical analysis.

### Version 3.2 Highlights

**Searchable Log File Names:**
```
F36_head_1441_tail_151_ratio_50.json
│   │    │     │    │    │      │
│   │    │     │    │    │      └─ Search range: ±50%
│   │    │     │    │    └──────── Mersenne/Tail pattern: 151
│   │    │     │    └─────────────  Head/Peak pattern: 1441
│   │    └────────────────────────  Fibonacci index: 36
└─────────────────────────────────  Self-documenting!
```

---

## 🚀 Quick Start

### 1. Installation

No external dependencies required for the search engine:

```bash
git clone [https://github.com/cygnusxi/smith_fibonacci_coords.git](https://github.com/cygnusxi/smith_fibonacci_coords.git)
cd smith_fibonacci_coords

For visualization dashboard (optional):
```bash
pip install -r requirements.txt
```

### 2. Run a Search

**Single Mode** - Test a specific hypothesis:
```powershell
python Auto_Heavy_hunt.py
# 1. Select directory (1=fibonacci_logs, 2=mersenne_logs, 3=custom)
# 2. Select mode (1=Single)
# 3. Enter Fibonacci index (e.g., 36)
# 4. Configure patterns (or use defaults)
# 5. Set search range (e.g., 50%)
```

**Auto Mode** - Batch process a range:
```powershell
python Auto_Heavy_hunt.py
# 1. Select directory
# 2. Select mode (2=Auto)
# 3. Enter range (e.g., 30 to 40)
# 4. Set search range for all (e.g., 50%)
# 5. Use default patterns or custom
```

### 3. Visualize Results

```powershell
python visualizer.py
# Select directory to visualize
# Open browser to http://127.0.0.1:5000
```

### 4. Search Your Data

```powershell
# List all logs
python log_search.py list

# Get statistics
python log_search.py stats

# Search by parameters
python log_search.py search --f 36
python log_search.py search --head 1441 --tail 151
python log_search.py search --ratio 50
```

---

## 📊 Data Visualization Dashboard

A custom Flask dashboard provides interactive visualization of pattern matches and distributions.

### Dashboard Features

| Chart Type | Purpose |
|------------|---------|
| **Matches per Fibonacci** | Identify which Fibonacci numbers yield most matches |
| **Execution Time** | Track computational cost and scaling |
| **Search Efficiency** | Monitor numbers scanned per second (hardware benchmark) |
| **Fibonacci Growth** | Visualize exponential sequence growth |
| **Distance Distribution** | Proves the "Cluster Theory" (matches near $F_n$) |
| **Distance Percentage** | Compare relative distances across indices |
| **Collatz Peaks** | Scatter plot identifying "Pillars" vs. "Explosions" |
| **Offset Distribution** | Analysis of Mersenne alignments ($+1, -1, 0$) |

### Starting the Dashboard

```powershell
# Interactive mode
python visualizer.py

# Command-line mode
python visualizer.py fibonacci_logs
python visualizer.py mersenne_logs
```

---

## 📂 File Structure

```
Fibanocci_Mersenne/
├── Auto_Heavy_hunt.py          # Main multiprocessing search engine
├── visualizer.py               # Flask web server for data analytics
├── log_search.py               # Command-line log search utility
│
├── fibonacci_logs/             # General research data
│   ├── F36_head_1441_tail_151_ratio_50.json
│   ├── F36_head_1441_tail_151_ratio_50.log
│   └── ...
│
├── mersenne_logs/              # Mersenne-focused research
│   └── (organized by parameters)
│
├── templates/                  # Dashboard HTML
│   └── dashboard.html
│
└── Documentation/
    ├── README.md               # This file
    ├── QUICKSTART.md           # Quick reference guide
    ├── NAMING_CONVENTION.md    # Log file naming specification
    ├── LOG_DIRECTORIES.md      # Directory management guide
    ├── VISUALIZATIONS.md       # Chart explanations
    ├── CHANGELOG.md            # Version history
    └── PROJECT_SUMMARY.md      # Complete project overview
```

---

## 🔍 Searchable Log Files

### Naming Convention

Log files use a descriptive format that encodes all search parameters:

```
F{index}_head_{pattern}_tail_{pattern}_ratio_{percent}
```

**Example:**
```
F36_head_1441_tail_151_ratio_50.json
```

This tells you immediately:
- Fibonacci index: F36
- Head pattern: 1441 (Collatz peak leading digits)
- Tail pattern: 151 (Mersenne leading digits)
- Search range: ±50% of F36

### PowerShell Searching

```powershell
# Find all F36 searches
Get-ChildItem fibonacci_logs\F36_*.json

# Find all searches with head pattern 1441
Get-ChildItem fibonacci_logs\*_head_1441_*.json

# Find all 50% ratio searches
Get-ChildItem fibonacci_logs\*_ratio_50.json
```

### Log Search Utility

```powershell
# List all logs with parameters
python log_search.py list

# Get statistics
python log_search.py stats

# Search by any parameter
python log_search.py search --f 36 --ratio 50
```

See [NAMING_CONVENTION.md](NAMING_CONVENTION.md) for complete details.

---

## 📖 Documentation

- **[QUICKSTART.md](QUICKSTART.md)** - Quick reference for common tasks
- **[NAMING_CONVENTION.md](NAMING_CONVENTION.md)** - Log file naming specification
- **[LOG_DIRECTORIES.md](LOG_DIRECTORIES.md)** - Directory management guide
- **[VISUALIZATIONS.md](VISUALIZATIONS.md)** - Detailed chart explanations
- **[CHANGELOG.md](CHANGELOG.md)** - Version history and updates
- **[PROJECT_SUMMARY.md](PROJECT_SUMMARY.md)** - Complete project overview

---

## 🎯 Use Cases

### Research Workflows

1. **Pattern Discovery** - Test different head/tail combinations to find new patterns
2. **Parameter Optimization** - Compare different search ranges to optimize efficiency
3. **Verification Studies** - Reproduce and verify specific results
4. **Batch Analysis** - Process ranges of Fibonacci indices for statistical analysis
5. **Publication Preparation** - Organize and export verified results

### Example: Testing the Hall of Fame

```powershell
# Test F36 Zero-Point Anomaly
python Auto_Heavy_hunt.py
# Directory: mersenne_logs
# Mode: Single
# Index: 36
# Head: 1493, Tail: 352, Ratio: 50%

# Result: F36_head_1493_tail_352_ratio_50.json
```

---

## 🔬 Technical Details

### Algorithms

- **Fibonacci Calculation:** Iterative O(n) approach
- **Collatz Sequence:** Standard 3n+1 with peak tracking
- **Mersenne Check:** Logarithmic O(1) leading digit extraction
- **Multiprocessing:** Work-stealing pool with dynamic load balancing

### Performance

- **Speed:** Millions of numbers per minute (hardware dependent)
- **Scalability:** Linear speedup with CPU core count
- **Memory:** Efficient chunked processing
- **Optimization:** Mersenne-first filtering reduces Collatz calculations by 99%+

### Requirements

- Python 3.6+
- Standard library (no dependencies for search engine)
- Flask + Plotly (optional, for visualization)
- Multi-core CPU recommended

---

## 📜 Citation & License

### Citation

If you use this tool or reference the Smith-Fibonacci Coordinate Conjecture, please cite:

```
Smith, Joshua. (2025). The Smith-Fibonacci Coordinate Project: 
Computational Verification of Collatz-Mersenne-Fibonacci Structures. 
GitHub Repository. https://github.com/cygnusxi/smith_fibonacci_coords
```

### License

MIT License - See LICENSE file for details.

---

## 🤝 Contributing

This is an active research project. Contributions, suggestions, and discussions are welcome:

- Open issues for bugs or feature requests
- Submit pull requests for improvements
- Share interesting patterns you discover
- Contribute to documentation

---

## 📞 Contact

**Lead Researcher:** Joshua Smith  
**Project Status:** Active Research  
**Current Focus:** Computational verification of Fibonacci-Mersenne coordinate structures

---

## 🔄 Version History

- **v3.2** (2025-01-13) - Searchable log file naming convention
- **v3.1** (2025-01-13) - Multi-directory support
- **v3.0** (2025-01-13) - Auto mode, visualization dashboard, comprehensive logging
- **v2.0** - Multiprocessing optimization
- **v1.0** - Initial release

See [CHANGELOG.md](CHANGELOG.md) for detailed version history.

---

**Pattern Hunter 3.2** - Transforming raw computation into mathematical discovery.
