# Predicting Frequent Itemsets in a Grocery Store

A C++ implementation of the Apriori algorithm for mining frequent itemsets from grocery store transaction data. This project identifies patterns and associations in customer purchase behavior to provide valuable insights for market basket analysis.

![Language](https://img.shields.io/badge/Language-C++-blue.svg)
![Algorithm](https://img.shields.io/badge/Algorithm-Apriori-green.svg)
![Data%20Structure](https://img.shields.io/badge/Data%20Structure-Linked%20Lists-orange.svg)

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Algorithm](#algorithm)
- [Installation](#installation)
- [Usage](#usage)
- [Input Format](#input-format)
- [Output Format](#output-format)
- [Project Structure](#project-structure)
- [Technical Implementation](#technical-implementation)
- [Example](#example)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

This project implements the Apriori algorithm to discover frequent itemsets in supermarket transaction data. By analyzing customer purchase patterns, the system identifies which items are frequently bought together, enabling retailers to:

- Optimize product placement and store layout
- Design effective cross-selling strategies
- Create targeted promotional campaigns
- Improve inventory management
- Enhance customer shopping experience

## ✨ Features

- **Multi-level Itemset Generation**: Discovers frequent 1-itemsets, 2-itemsets (pairs), and 3-itemsets (triplets)
- **Threshold-based Filtering**: Configurable minimum support threshold to filter significant patterns
- **Data Preprocessing**: 
  - Automatic removal of punctuation marks and special characters
  - Case normalization (uppercase to lowercase conversion)
  - Data cleaning and validation
- **Efficient Data Structures**: Custom linked list implementation for optimal memory management
- **Frequency Calculation**: Accurate counting of item occurrence and co-occurrence
- **Sorted Output**: Results sorted by frequency in descending order

## 🔬 Algorithm

The implementation follows the classic Apriori algorithm with these key steps:

1. **Data Loading & Preprocessing**
   - Read transaction data from input file
   - Clean and normalize item names
   - Remove invalid characters and punctuation

2. **Frequent 1-Itemset Generation**
   - Count occurrence of each individual item
   - Filter items based on minimum support threshold
   - Sort by frequency

3. **Frequent 2-Itemset Generation (Duplets)**
   - Generate candidate pairs from frequent 1-itemsets
   - Count co-occurrence in transactions
   - Apply threshold filtering
   - Sort by frequency

4. **Frequent 3-Itemset Generation (Triplets)**
   - Generate candidate triplets from frequent 2-itemsets
   - Count co-occurrence in transactions
   - Apply threshold filtering
   - Sort by frequency

## 🚀 Installation

### Prerequisites

- C++ compiler (GCC 7.0+ or equivalent)
- Standard C++ libraries
- Make (optional, for build automation)

### Setup

1. Clone the repository:
```bash
git clone https://github.com/heenaikramdekhan/Predicting-Frequent-item-set-sold-in-a-Grocery-Store-.git
cd Predicting-Frequent-item-set-sold-in-a-Grocery-Store-
```

2. Navigate to the project directory:
```bash
cd "DS Assignment 1/DS Assignment 1"
```

3. Compile the project:
```bash
g++ -o apriori main.cpp -std=c++11
```

## 💻 Usage

### Basic Usage

```bash
./apriori input.txt
```

### Function Calls

```cpp
// Read input file
readInputFile("transactions.txt");

// Remove punctuation marks
removePunctuationMarks();

// Convert to lowercase
convertUpperToLowerCase();

// Generate frequent 1-itemsets
generateFirstItemSet("itemset1.txt");

// Generate frequent 2-itemsets
generateSecondItemSet("itemset2.txt");

// Generate frequent 3-itemsets
generateThirdItemSet("itemset3.txt");

// Write cleaned transactions to file
writingTransactionLLToFile("cleaned_transactions.txt");
```

## 📊 Input Format

The input file should follow this structure:

```
0.3
<blank line>
bread,milk,eggs
milk,butter,cheese
bread,milk,butter
eggs,bacon,bread
milk,eggs,bread,butter
```

- **Line 1**: Minimum support threshold (e.g., 0.3 = 30%)
- **Line 2**: Blank line
- **Line 3+**: Transaction data (comma-separated items)

### Input File Requirements

- Threshold value must be between 0 and 1 (decimal format)
- Each transaction on a separate line
- Items separated by commas
- No empty transactions

## 📈 Output Format

The system generates three output files:

### 1. Frequent 1-Itemsets (`itemset1.txt`)
```
milk(5)
bread(4)
eggs(3)
butter(3)
```

### 2. Frequent 2-Itemsets (`itemset2.txt`)
```
milk,bread(4)
milk,eggs(3)
milk,butter(3)
bread,eggs(2)
```

### 3. Frequent 3-Itemsets (`itemset3.txt`)
```
milk,bread,eggs(2)
milk,bread,butter(2)
```

Format: `item1,item2,...(frequency)`

## 📁 Project Structure

```
Predicting-Frequent-item-set-sold-in-a-Grocery-Store-/
│
├── DS Assignment 1/
│   └── DS Assignment 1/
│       ├── apriori.h              # Header file with algorithm implementation
│       ├── main.cpp               # Main driver program
│       ├── transactions.txt       # Sample input file
│       └── output/                # Generated output files
│           ├── itemset1.txt       # Frequent 1-itemsets
│           ├── itemset2.txt       # Frequent 2-itemsets
│           └── itemset3.txt       # Frequent 3-itemsets
│
└── README.md
```

## 🛠️ Technical Implementation

### Core Data Structures

#### 1. Node Class
```cpp
class Node {
    char* dataArray;    // Item name
    int size;           // Size of data
    Node* next;         // Pointer to next node
};
```
- Represents individual items in a transaction
- Forms linked list for each transaction

#### 2. FrequencyNode Class
```cpp
class FrequencyNode {
    string stringName;       // Item/itemset name
    int frequency;           // Occurrence count
    FrequencyNode* next;     // Pointer to next node
};
```
- Tracks frequency of items and itemsets
- Maintains sorted frequency lists

#### 3. TransactionsLL Class
Main class managing the entire Apriori implementation with key methods:

- `readData()`: Load and parse transaction data
- `removePunctuation()`: Clean item names
- `UpperToLower()`: Normalize case
- `CalculateFrequencies()`: Count item occurrences
- `calculateFrequencyOfDuplets()`: Count pair occurrences
- `calculateFrequencyOfTriplets()`: Count triplet occurrences
- `sortFrequencies()`: Sort results by frequency
- `writeFrequencies()`: Output results to files

### Algorithm Complexity

- **Time Complexity**: O(n × m²) for 2-itemsets, O(n × m³) for 3-itemsets
  - n = number of transactions
  - m = number of unique items
  
- **Space Complexity**: O(n × k)
  - k = average items per transaction

## 📝 Example

### Sample Input (`transactions.txt`)
```
0.4

apple,banana,orange
banana,milk,bread
apple,banana,milk
orange,juice,bread
apple,banana,bread,milk
banana,bread
```

### Sample Output

**itemset1.txt** (threshold 40% = 3 transactions):
```
banana(5)
bread(4)
apple(3)
milk(3)
```

**itemset2.txt**:
```
banana,bread(3)
apple,banana(3)
banana,milk(3)
```

**itemset3.txt**:
```
apple,banana,milk(2)
```

## 🔑 Key Features Explained

### 1. Data Preprocessing
- **Punctuation Removal**: Eliminates special characters (@, +, -, numbers)
- **Case Normalization**: Converts all text to lowercase for consistency
- **Validation**: Ensures clean, standardized data for accurate analysis

### 2. Threshold-based Filtering
The minimum support threshold determines which itemsets are considered "frequent":
- Threshold = 0.3 means items must appear in at least 30% of transactions
- Helps focus on significant patterns and reduce noise

### 3. Dynamic Memory Management
- Efficient use of linked lists for variable-length transactions
- Dynamic allocation and deallocation to optimize memory usage
- No fixed-size limitations on transaction data

## 🎓 Applications

This frequent itemset mining system can be applied to:

1. **Retail Analytics**
   - Market basket analysis
   - Product bundling strategies
   - Cross-selling recommendations

2. **Inventory Management**
   - Stock optimization
   - Demand forecasting
   - Supply chain efficiency

3. **Store Layout Optimization**
   - Product placement decisions
   - Aisle organization
   - Promotional display planning

4. **Customer Behavior Analysis**
   - Shopping pattern identification
   - Customer segmentation
   - Personalized marketing

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Contribution Guidelines

- Follow existing code style and conventions
- Add comments for complex logic
- Update documentation for new features
- Test thoroughly before submitting

## 📄 License

This project is available for educational and research purposes.

## 👨‍💻 Author

**Heena Ikram Dekhan**

- GitHub: [@heenaikramdekhan](https://github.com/heenaikramdekhan)
- Project Link: [Predicting Frequent Itemsets](https://github.com/heenaikramdekhan/Predicting-Frequent-item-set-sold-in-a-Grocery-Store-)

## 🙏 Acknowledgments

- Apriori algorithm based on the seminal paper by Agrawal & Srikant (1994)
- Data structures and algorithms concepts
- Market basket analysis research community

## 📚 References

1. Agrawal, R., & Srikant, R. (1994). "Fast Algorithms for Mining Association Rules"
2. Data Mining: Concepts and Techniques - Han, Kamber & Pei
3. Introduction to Data Mining - Tan, Steinbach & Kumar

---

**Note**: This is an academic project demonstrating the implementation of the Apriori algorithm for frequent itemset mining. For production use, consider optimization techniques and additional features like association rule generation.
