# SpellChecker with Bloom Filter

## Overview

This tool implements a spell checker using a Bloom filter, a space-efficient probabilistic data structure. The Bloom filter allows for quick lookups to determine if a word is in the dictionary, with a small probability of false positives. This makes it ideal for spell checking, where we want to minimize the number of misspelled words that are incorrectly identified as correct.

## Features

- **Efficient Spell Checking**: Uses a Bloom filter to quickly check if a word is in the dictionary.
- **Customizable Parameters**: Allows setting the number of elements and the false positive probability.
- **Persistence**: Saves and loads the Bloom filter to/from a file for persistent use.

## Installation

To install the tool, clone the repository and build the project:

```sh
git clone https://github.com/islamghany/bloom-filter-spell-checker.git
cd bloom-filter-spell-checker
go build -o spellchecker
```

## Usage

### Building the Bloom Filter

To build the Bloom filter from a dictionary file, use the `-build` flag:

```sh
./spellchecker -build dictionary.txt
```

This command will read the dictionary file, populate the Bloom filter, and save it to a file (`bloom_filter.json`).

### Checking Words

To check if words are in the dictionary, simply run the tool with the words as arguments:

```sh
./spellchecker word1 word2 word3
```

The tool will load the Bloom filter from the file (`bloom_filter.json`) and check each word. If a word is not found in the Bloom filter, it will print a message indicating that the word is not found.

### Example

```sh
./spellchecker -build dictionary.txt
./spellchecker hello world example
```

Output:

```
word not found: example
```

## Configuration

The Bloom filter is configured with the following parameters:

- **Number of Elements (n)**: The number of words in the dictionary.
- **False Positive Probability (p)**: The desired false positive probability.

These parameters are used to calculate the size of the bit array and the number of hash functions.

## How It Works

1. **Bloom Filter Calculation**:

   - **Bit Array Size (m)**: Calculated using the formula `m = -n * ln(p) / (ln(2)^2)`.
   - **Number of Hash Functions (k)**: Calculated using the formula `k = (m / n) * ln(2)`.

2. **Hash Functions**:

   - The tool uses a combination of FNV-1a and MurmurHash algorithms with different seeds to generate multiple hash values for each element.

3. **Bit Manipulation**:

   - Each hash value is used to set specific bits in the bit array, indicating the presence of an element.

4. **Lookup**:
   - To check if an element is in the set, the tool generates the same hash values and checks the corresponding bits in the bit array.

### Additional Notes

- **Dictionary File Format**: Ensure that the dictionary file is formatted with one word per line.
- **Performance**: The Bloom filter is designed to be space-efficient, but the performance may vary depending on the size of the dictionary and the false positive probability.

Feel free to customize this README file further to better match your project's specifics.
