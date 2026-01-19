# 📊 TOPSIS Command-Line Implementation

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)

## Overview

This project is a **command-line implementation** of **TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution)** 📈, built from scratch in Python. It provides a robust CLI tool for multi-criteria decision making with comprehensive input validation and error handling.
---

## 🧐 About TOPSIS

TOPSIS is a widely-used **Multi-Criteria Decision Making (MCDM)** technique that ranks alternatives based on multiple criteria.

### 🎯 Core Principle

The optimal alternative should:
- ✅ Be **closest** to the **Positive Ideal Solution (PIS)**
- ❌ Be **farthest** from the **Negative Ideal Solution (NIS)**

### 📌 Applications
- Business analytics and decision-making
- Supplier and vendor selection
- Product ranking and comparison
- Engineering design evaluation
- Data science model selection

---

## 🚀 Features

| Feature | Description |
|---------|-------------|
| 🖥️ Command-Line Interface | Easy-to-use CLI with clear syntax |
| ✅ Robust Validation | Comprehensive input checking and error handling |
| 🔍 Exception Handling | Graceful handling of file errors and invalid data |
| 📊 CSV Support | Input and output via CSV files |
| 🧮 From Scratch | Pure Python implementation with NumPy/Pandas |
| 📝 Clear Error Messages | Descriptive messages for debugging |

---

## 🛠️ Prerequisites

| Requirement | Version |
|-------------|---------|
| 🐍 Python | 3.8+ |
| 📦 Pandas | Latest |
| 🔢 NumPy | Latest |

---

## 🔧 Installation

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/aishani-s20/TOPSIS_Implementation.git
cd TOPSIS_Implementation
```

### 2️⃣ Install Dependencies
```bash
pip install pandas numpy
```

---

## 💻 Usage

### Command Syntax
```bash
python <program.py> <InputDataFile> <Weights> <Impacts> <OutputResultFileName>
```

### Parameters

| Parameter | Description | Format |
|-----------|-------------|--------|
| `InputDataFile` | CSV file with decision matrix | `data.csv` |
| `Weights` | Comma-separated weights for criteria | `"1,1,1,2"` |
| `Impacts` | Comma-separated impacts (+/- for each criterion) | `"+,+,-,+"` |
| `OutputResultFileName` | Output CSV file name | `output-result.csv` |

### Example Usage
```bash
python topsis.py data.csv "1,1,1,2" "+,+,-,+" output-result.csv
```

---

## 📊 Input File Format

### Requirements

Your input CSV file must meet the following criteria:

✅ **Minimum 3 columns** (1 object/name column + at least 2 criteria columns)  
✅ **First column:** Object names/identifiers (text)  
✅ **Columns 2 to last:** Numeric values only  
✅ **No missing values** in criteria columns

### Example Input (`data.csv`)

| Model | Price | Storage | Camera | Looks |
|-------|-------|---------|--------|-------|
| M1    | 250   | 16      | 12     | 5     |
| M2    | 200   | 16      | 8      | 3     |
| M3    | 300   | 32      | 16     | 4     |
| M4    | 275   | 32      | 8      | 4     |
| M5    | 225   | 16      | 16     | 2     |

### Example Output (`output-result.csv`)

| Model | Price | Storage | Camera | Looks | Topsis Score | Rank |
|-------|-------|---------|--------|-------|--------------|------|
| M1    | 250   | 16      | 12     | 5     | 0.5345       | 3    |
| M2    | 200   | 16      | 8      | 3     | 0.3082       | 5    |
| M3    | 300   | 32      | 16     | 4     | 0.6914       | 1    |
| M4    | 275   | 32      | 8      | 4     | 0.5349       | 2    |
| M5    | 225   | 16      | 16     | 2     | 0.4018       | 4    |

---

## ✅ Input Validation

The program performs comprehensive validation:

### 1️⃣ Parameter Count Validation
```
❌ Error: Incorrect number of parameters
✅ Usage: python topsis.py <InputDataFile> <Weights> <Impacts> <ResultFileName>
```

### 2️⃣ File Existence Check
```
❌ Error: File 'data.csv' not found
```

### 3️⃣ Minimum Column Check
```
❌ Error: Input file must contain at least 3 columns
```

### 4️⃣ Numeric Value Validation
```
❌ Error: Columns 2 onwards must contain numeric values only
```

### 5️⃣ Parameter Length Matching
```
❌ Error: Number of weights, impacts, and columns must be the same
✅ Expected: 4 values for 4 criteria columns
❌ Received: 3 weights, 4 impacts
```

### 6️⃣ Impact Validation
```
❌ Error: Impacts must be either '+' or '-'
❌ Invalid impact: 'x'
```

### 7️⃣ Separator Validation
```
❌ Error: Weights and impacts must be separated by commas
```

---

## 📈 TOPSIS Methodology

The implementation follows these steps:

### Step 1: Normalize the Decision Matrix
Convert the raw data into a normalized matrix using vector normalization:
```
normalized_value = value / sqrt(sum_of_squares)
```

### Step 2: Apply Weights
Multiply each normalized value by its corresponding weight:
```
weighted_value = normalized_value × weight
```

### Step 3: Determine Ideal Solutions

- **Positive Ideal Solution (V⁺):** Best value for each criterion
  - For beneficial criteria (+): maximum value
  - For cost criteria (-): minimum value

- **Negative Ideal Solution (V⁻):** Worst value for each criterion
  - For beneficial criteria (+): minimum value
  - For cost criteria (-): maximum value

### Step 4: Calculate Separation Measures

- **Distance from V⁺:** Euclidean distance from positive ideal
- **Distance from V⁻:** Euclidean distance from negative ideal
```
distance = sqrt(sum((value - ideal)²))
```

### Step 5: Calculate TOPSIS Score
```
score = distance_from_V⁻ / (distance_from_V⁺ + distance_from_V⁻)
```

Score ranges from 0 to 1, where higher is better.

### Step 6: Rank Alternatives

Rank all alternatives based on TOPSIS score in descending order.

---

## 📊 Score Interpretation

| Score Range | Interpretation |
|-------------|----------------|
| 🔴 0.0 – 0.3 | Poor alternative |
| 🟡 0.3 – 0.6 | Average alternative |
| 🟢 0.6 – 1.0 | Excellent alternative |

---

## 📂 Project Structure
```
📦 TOPSIS-CLI-Implementation
 ┣ 📜 topsis.py              # Main program
 ┣ 📜 README.md              # Documentation
 ┗ 📜 LICENSE                # MIT License
```
---

## 🔍 Error Handling Summary

The program handles:

- ✅ Invalid command-line arguments
- ✅ Missing or inaccessible files
- ✅ Insufficient columns in input
- ✅ Non-numeric values in criteria columns
- ✅ Mismatched parameter counts
- ✅ Invalid impact symbols
- ✅ Incorrect separator formats
- ✅ Empty or malformed CSV files

---

## 📝 License

This project is licensed under the **MIT License** 📜

---

## 👨‍💻 Author

**Aishani Shreya**  
📧 **Roll Number:** 102303250

---

## 🙏 Acknowledgments

- TOPSIS algorithm methodology
- Python community for excellent libraries
- Academic resources for MCDM techniques
