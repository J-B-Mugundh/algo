---
id: look-and-say-problem-dsa  
title: Look and Say Recursion  
sidebar_label: Look and Say  
sidebar_position: 7  
description: "The Look and Say sequence is a sequence of numbers where each term is generated by reading off the digits of the previous term. The sequence starts with 1, and each subsequent number describes the digits in the previous number. The problem can be solved recursively by processing each number and generating the next in the sequence."  
tags: [look-and-say, recursion, sequence, dsa]  
---


### Introduction

The **Look and Say sequence** is a mathematical sequence in which each term is generated by describing the digits of the previous term. The first term in the sequence is always "1", and each subsequent term is constructed by reading consecutive digits and saying how many of each digit are present.

For example, starting with "1":
- The next term is "11" (one 1).
- The following term is "21" (two 1s).
- The next term is "1211" (one 2, one 1), and so on.

### Problem Statement

Given an integer `n`, return the `n`th term of the Look and Say sequence.

### Approach

The Look and Say sequence can be generated recursively. We observe that each term is derived from the previous term by counting consecutive occurrences of digits and constructing the next term based on these counts.

For example:
- Term 1: "1" → "11" (one 1)
- Term 2: "11" → "21" (two 1s)
- Term 3: "21" → "1211" (one 2, one 1)

### Pseudo Code

1. Base Case: If `n == 1`, return "1".
2. Recursive Call: Get the `(n-1)`th term.
3. Process the previous term:
   - Iterate through the term and count consecutive occurrences of digits.
   - Append the count and the digit to the result string.
4. Return the result for the `n`th term.

### Algorithm

1. **Base Case**: The first term is always "1".
2. **Recursive Construction**: For each subsequent term, use the previous term to generate the current one by counting consecutive digits.
3. **Iterate**: Loop through the digits of the previous term, counting how many times each digit appears consecutively.
4. **Form the New Term**: For each group of consecutive digits, append the count followed by the digit itself to form the next term.
5. **Return the `n`th term**: Repeat this process recursively or iteratively until the `n`th term is generated.

### Implementation in C++

```cpp
#include <iostream>
#include <string>
using namespace std;

class Solution {
public:
    // Function to recursively generate the nth term of the Look and Say sequence
    string lookAndSay(int n) {
        // Base case: the first term is "1"
        if (n == 1) return "1";
        // Get the previous term
        string prevTerm = lookAndSay(n - 1);
        string result = "";
        int count = 1;
        
        // Iterate through the previous term and generate the current term
        for (int i = 1; i < prevTerm.length(); i++) {
            // If the current digit matches the previous one, increment the count
            if (prevTerm[i] == prevTerm[i - 1]) {
                count++;
            } else {
                // Append the count and the digit to the result string
                result += to_string(count) + prevTerm[i - 1];
                count = 1; // Reset the count for the next group
            }
        }
        
        // Append the last group to the result
        result += to_string(count) + prevTerm[prevTerm.length() - 1];
        return result;
    }
};

int main() {
    Solution obj;
    int n = 5; // Let's find the 5th term in the Look and Say sequence
    string result = obj.lookAndSay(n);
    
    // Output the result
    cout << "The " << n << "th term of the Look and Say sequence is: " << result << endl;
    return 0;
}
```
