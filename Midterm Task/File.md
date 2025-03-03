# Midterm Lab Task 1
This task is Data cleaning and preparation using Excel.

# Part 1.
### STEP 1: Autofit Columns and Rows:
Select the entire worksheet and use the autofit feature to make columns and rows visible.
Keyboard shortcuts: CTRL+A to select all, ALT+H+O+I for column width, and ALT+H+O+A for row height.

### Step 2: Identify and Remove Duplicates:
Use conditional formatting to highlight duplicates, then remove them using the 'Remove Duplicates' feature under the Data tab.

### Step 3: Trim Extra Spaces:
Use the TRIM function to remove extra spaces from the data.
Apply the formula to the necessary columns and copy the cleaned data back into the original columns.

### Step 4: Eliminate Blank Cells:

Use the 'Go To Special' option to select and fill blank cells with a placeholder value or data from the cell above.

### Step 5; Spell Check:

Run a spell check on the selected columns to correct typos and misspellings.
Use the keyboard shortcut F7 to open the spell check dialog box.

### Step 6: Data Validation:

Set up data validation rules to enforce data integrity.

Create dropdown lists for specific columns to prevent future errors.

### Step 7: Handle Errors with IFERROR:

Use the IFERROR function to manage and display errors in the dataset.

Return a custom value or formula in place of error messages.

### Step 8: Number Formats:

Use plain number formats during the analysis phase to avoid unnecessary clutter.

Apply comma separators for large numbers and format dates as 'Short Date' if the time component is not needed.

### Step 9: Find & Replace:

Use the Find & Replace tool for bulk corrections to maintain data consistency.

Replace unwanted values, such as 'inf', with desired values or blank cells. 


# Sample output:
<img src="image/Screenshot%20(1).png" alt="Alt Text" width="400" height="300">

# Part 2
### Normalization

### Understand Data Schema: 
- Ensure you fully understand the data schema, identifying all the attributes and their relationships.

### First Normal Form (1NF):
- Ensure that each column contains atomic, indivisible values, and there are no repeating groups. If necessary, break down composite attributes into individual attributes.

### Second Normal Form (2NF):
- Ensure that the data is in 1NF and that all non-key attributes are fully functional dependent on the primary key. If necessary, remove partial dependencies by creating additional tables.

### Third Normal Form (3NF):
- Ensure that the data is in 2NF and that all the attributes are only dependent on the primary key. Remove transitive dependencies by creating new tables if necessary.

### Boyce-Codd Normal Form (BCNF):
- Ensure that for every non-trivial functional dependency, the left-hand side is a superkey. This step is an extension of 3NF with a stricter requirement.

### Fourth Normal Form (4NF):
- Ensure that there are no multi-valued dependencies. If an attribute in a table uniquely determines another attribute, ensure there are no more sets of multi-valued dependencies.

### Fifth Normal Form (5NF):
- Ensure that there are no join dependencies. This form deals with cases where information can be reconstructed from smaller pieces of data without introducing redundancy.

### Domain-Key Normal Form (DKNF):
- Ensure that every constraint on the relationship is a logical consequence of the definition of the keys and domains.

### Sixth Normal Form (6NF):
- Ensure that each table only contains a single candidate key along with its functional dependencies.

# Sample output:
<img src="image/Screenshot%20(4).png" alt="Alt Text" width="400" height="300">
