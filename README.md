# Student Data Processing Project

This Code lab processes student data to generate email addresses, separate gender lists, identify names with special characters, calculate name similarities, and shuffle the student list.

## Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package installer)

### Setting Up the Virtual Environment

1. *Create a Virtual Environment*:
    bash
    python -m venv myenv
    

2. *Activate the Virtual Environment*:
    - On Windows:
      bash
      myenv\Scripts\activate
      
    - On macOS and Linux:
      bash
      source myenv/bin/activate
      

3. *Install the Required Libraries*:
    bash
    pip install numpy pandas openpyxl tensorflow tensorflow-hub
    

## Usage

1. *Place the Excel File*:
   Ensure the Test files.xlsx file is in the project root directory.

2. *Run the Main Script*:
    bash
    python main.py
    

   This will read the data from the Excel file, process it, and generate the required outputs.

## Project Structure
 *main.py*: The main script that orchestrates the data processing.
- *function.py*: Contains helper functions used in the main script.
- *logs.txt*: Log file where the counts of male and female students and names with special characters are recorded.

## Functions Overview

### main.py

- *Import Libraries*: 
  python
  import pandas as pd
  import numpy as np
  import re
  import json
  import tensorflow_hub as hub
  from function import generate_email, separate_gender_lists, special_character_names, calculate_similarity, shuffle_and_save
  
- **Load the Tools**:

First, we bring in some tools that will help us with the job. It's like getting your pencils, erasers, and rulers ready before you start working on a project.
 
- python

    import pandas as pd
    import numpy as np
    import re
    import json
    import tensorflow_hub as hub
    from function import generate_email, separate_gender_lists, special_character_names, calculate_similarity, shuffle_and_save
- *Read the Student List*:

We read the student list from an Excel file called 'Test files.xlsx'. Think of it like opening your notebook to see all the names written down

---

# Function.py

## Step 1: Load the Tools
We start by bringing in some tools that will help us work with data and text. It's like getting your school supplies ready before you start your homework.

```python
import re
import pandas as pd
import numpy as np
```

## Step 2: Create Email Addresses
We define a function to create email addresses. It takes the first letter of the first name and combines it with the last name to make an email. For example, "John Doe" becomes "jdoe@gmail.com".

```python
def generate_email(first_name, last_name):
    clean_last_name = re.sub(r'\W+', '', last_name).lower()
    return f"{first_name[0].lower()}{clean_last_name}@gmail.com"
```

Here’s what happens:
- `clean_last_name` removes any special characters from the last name and makes it lowercase.
- The email is created by combining the first letter of the first name with the cleaned last name.

## Step 3: Separate Boys and Girls
We define a function to separate boys and girls into different lists. This is like making two different teams from your class list and saving them in separate files.

```python
def separate_gender_lists(df):
    males = df[df['Gender'] == 'Male']
    females = df[df['Gender'] == 'Female']
    males.to_csv('male_students.csv', index=False)
    females.to_csv('female_students.csv', index=False)

    with open('logs.txt', 'a') as log_file:
        log_file.write(f"Number of male students: {len(males)}\n")
        log_file.write(f"Number of female students: {len(females)}\n")
```

In this function:
- We create two new lists: one for boys (males) and one for girls (females).
- We save these lists into two separate files: 'male_students.csv' and 'female_students.csv'.
- We log the number of boys and girls.

## Step 4: Find Special Names
We define a function to find names with special characters (like "Ng'wono"). We make a list of these names and save it in a file.

```python
def special_character_names(df):
    pattern = re.compile(r"[^\w\s]")
    special_char_names = df[df['Last Name'].apply(lambda x: bool(pattern.search(x)))]
    special_char_names.to_csv('special_char_names.csv', index=False)

    with open('logs.txt', 'a') as log_file:
        log_file.write(f"Special character names:\n{special_char_names.to_string(index=False)}\n")
```

Here’s what happens:
- We use a pattern to look for special characters in the last names.
- We create a list of names that have these special characters and save it in 'special_char_names.csv'.
- We log the special character names.

## Step 5: Calculate Name Similarities
We define a placeholder function to calculate how similar boys' names are to girls' names. This is like seeing if "John" and "Joan" sound alike.

```python
def calculate_similarity(male_names, female_names):
    # Placeholder for your similarity calculation logic
    pass
```

Right now, this function doesn't do anything because it's just a placeholder. You would need to add the logic for comparing names.

## Step 6: Shuffle and Save the List
We define a function to shuffle the student list (like shuffling a deck of cards) and then save the shuffled list in different formats.

```python
def shuffle_and_save(df):
    shuffled_df = df.sample(frac=1).reset_index(drop=True)
    shuffled_df.to_json('shuffled_students.json', orient='records', lines=False)
    shuffled_df.to_json('shuffled_students.jsonl', orient='records', lines=True)
```

Here’s what happens:
- `shuffled_df = df.sample(frac=1).reset_index(drop=True)` shuffles the list randomly.
- We save the shuffled list in two formats: JSON and JSONL.

## Summary
This code helps you:
1. Create email addresses for students.
2. Separate boys and girls into different lists.
3. Find names with special characters.
4. Shuffle the student list.
5. Save all the information into files and log some details for reference.

It's like organizing a class list, making sure everyone has an email, and saving everything neatly in your notebook and computer.

---

