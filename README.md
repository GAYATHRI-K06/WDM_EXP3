### EX3 Implementation of GSP Algorithm In Python
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>

### Program:

````````
from collections import defaultdict
from itertools import combinations

def generate_candidates(dataset, k, min_support):
    c = defaultdict(int)
    for seq in dataset:
        items = [tuple(sorted(itemset)) for itemset in seq]
        flat = [elem for itemset in items for elem in itemset]
        for item in combinations(flat, k):
            c[tuple(sorted(item))] += 1  
            
    frequent = {items: support for items, support in c.items() if support >= min_support}
    return frequent

def gsp(dataset, min_support):
    k = 1
    fp = dict()
    while True:
        candidates = generate_candidates(dataset, k, min_support)
        if not candidates:
            break
        fp.update(candidates)
        k += 1
    return fp

dataset1 = [
    [["b","d"], ["c"], ["b"], ["a","c"]],
    [["b","f"], ["c","e"], ["b"], ["f","g"]],
    [["a","h"], ["b","f"], ["a"], ["b"], ["f"]],
    [["b","e"], ["c","e"], ["d"]],
    [["a"], ["b","d"], ["b"], ["c"], ["b"], ["a","d","e"]]
]

dataset2 = [
    [["a","b","c"], ["b","e"], ["c"], ["f"], ["g"], ["a","b","e"]],
    [["a","d"], ["b","c"], ["c"], ["f","g"], ["c","h"]],
    [["b","c"], ["a","d"], ["e"], ["b"], ["f"], ["c","d","f","g","h"]],
    [["c"], ["e","c"], ["e","h"]]
]

min_support = 3

dataset1_result = gsp(dataset1, min_support)
dataset2_result = gsp(dataset2, min_support)

print("Frequent Sequential Patterns - Dataset 1:")
if dataset1_result:
    for pattern, support in dataset1_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Dataset 1.")

print("\nFrequent Sequential Patterns - Dataset 2:")
if dataset2_result:
    for pattern, support in dataset2_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Dataset 2.")
````````` 
    
### Output:
<img width="768" height="765" alt="image" src="https://github.com/user-attachments/assets/32ff2c0b-19e7-4412-9db5-92b2193c0b37" />
<img width="891" height="762" alt="image" src="https://github.com/user-attachments/assets/4907f07b-f0de-4c61-9436-89a6ba90a3d4" />
<img width="886" height="766" alt="image" src="https://github.com/user-attachments/assets/cba4c86f-e92e-405a-821e-b2f1913a919e" />
<img width="663" height="808" alt="image" src="https://github.com/user-attachments/assets/520c0113-dcdc-4052-a923-0a90418b7f7c" />
<img width="760" height="791" alt="image" src="https://github.com/user-attachments/assets/1d3282a6-24ee-4ce4-b3e9-80ed7a22f70e" />

<img width="723" height="704" alt="image" src="https://github.com/user-attachments/assets/942086bd-c6eb-46db-bc28-8f60165a8d50" />




### Visualization:
``````
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each dataset using a line plot
visualize_patterns_line(dataset1_result, 'Dataset 1')
visualize_patterns_line(dataset2_result, 'Dataset 2')


``````````
### Output:
<img width="976" height="555" alt="image" src="https://github.com/user-attachments/assets/63fc3feb-b2bf-4475-bc05-48b0f68055c8" />
<img width="994" height="558" alt="image" src="https://github.com/user-attachments/assets/161c0f82-2a55-4d5b-add7-389e09d5187b" />


### Result:
GSP Algorithm In Python has been implemented successfully.
