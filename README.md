# PROGRAMMING ASSIGNMENT #2
### by: LABAYAN, Princess Noreen - 2ECEA

This repository is submitted as a partial requirement for **ECE 2112 – Advanced Computer Programming and Algorithms**. The objective of this experiment is to demonstrate the basic use of the Pandas library in loading a CSV file, selecting rows and columns, filtering data using Boolean conditions, and creating subsets of a DataFrame without modifying the original dataset.

---

## A. Positional and Label-Based Slicing


The first part of the experiment loads the `cars.csv` dataset into a Pandas DataFrame named `cars`. The program first displays the shape of the DataFrame together with the complete list of column names. It then uses positional indexing (`.iloc`) to extract rows 6 to 10 of the dataset and stores the result in a new DataFrame named `cars_6_to_10`. Finally, only the Model, mpg, cyl, hp, and gear columns are displayed using column labels.

### Functions Used

- `pd.read_csv()` – Reads the CSV file and stores it as a DataFrame.
- `.shape` – Returns the number of rows and columns.
- `.columns` – Displays the names of all columns.
- `.iloc[]` – Selects rows using integer positions.
- `[['column1','column2',...]]` – Selects specific columns by their labels.

### Code

```python
import pandas as pd

cars = pd.read_csv("cars.csv")

print(cars.shape)
print(cars.columns)

cars_6_to_10 = cars.iloc[5:10]

cars_subset = cars_6_to_10[["Model", "mpg", "cyl", "hp", "gear"]]

print(cars_subset)
```

### Output

```text
Shape:
(32, 12)

Columns:
Index(['Model', 'mpg', 'cyl', 'disp', 'hp', 'drat',
       'wt', 'qsec', 'vs', 'am', 'gear', 'carb'],
      dtype='object')
```
#### Rows 6–10 (`cars_6_to_10`)

| Index | Model | mpg | cyl | disp | hp | drat | wt | qsec | vs | am | gear | carb |
|:----:|----------------|----:|----:|-----:|---:|-----:|----:|-----:|---:|---:|----:|----:|
| 5 | Valiant | 18.1 | 6 | 225.0 | 105 | 2.76 | 3.46 | 20.22 | 1 | 0 | 3 | 1 |
| 6 | Duster 360 | 14.3 | 8 | 360.0 | 245 | 3.21 | 3.57 | 15.84 | 0 | 0 | 3 | 4 |
| 7 | Merc 240D | 24.4 | 4 | 146.7 | 62 | 3.69 | 3.19 | 20.00 | 1 | 0 | 4 | 2 |
| 8 | Merc 230 | 22.8 | 4 | 140.8 | 95 | 3.92 | 3.15 | 22.90 | 1 | 0 | 4 | 2 |
| 9 | Merc 280 | 19.2 | 6 | 167.6 | 123 | 3.92 | 3.44 | 18.30 | 1 | 0 | 4 | 4 |

#### Selected Columns

| Model | mpg | cyl | hp | gear |
|----------------|----:|----:|---:|----:|
| Valiant | 18.1 | 6 | 105 | 3 |
| Duster 360 | 14.3 | 8 | 245 | 3 |
| Merc 240D | 24.4 | 4 | 62 | 4 |
| Merc 230 | 22.8 | 4 | 95 | 4 |
| Merc 280 | 19.2 | 6 | 123 | 4 |

---

## B. Model Lookup


The second part of the experiment demonstrates Boolean indexing. The program searches the dataset for the model Toyota Corolla and displays its complete row. It also searches for Pontiac Firebird but displays only the Model, mpg, hp, and wt columns. The results are stored in the variables `toyota` and `pontiac`, respectively.

### Functions Used

- `.loc[]` – Selects rows and columns using labels.
- `==` – Compares values in a column.
- Boolean indexing – Returns rows that satisfy a given condition.

### Code

```python
toyota = cars[cars["Model"] == "Toyota Corolla"]

pontiac = cars.loc[
    cars["Model"] == "Pontiac Firebird",
    ["Model", "mpg", "hp", "wt"]
]

print(toyota)
print(pontiac)
```
### Output

**Toyota Corolla**

| Model | mpg | cyl | disp | hp | drat | wt | qsec | vs | am | gear | carb |
|------|----:|----:|----:|---:|----:|----:|----:|---:|---:|----:|----:|
| Toyota Corolla | 33.9 | 4 | 71.1 | 65 | 4.22 | 1.835 | 19.90 | 1 | 1 | 4 | 1 |

**Pontiac Firebird**

| Model | mpg | hp | wt |
|------|----:|---:|---:|
| Pontiac Firebird | 19.2 | 175 | 3.845 |

---

## C. Multi-Model Subsetting

The final part creates a new DataFrame named `selected_cars` containing only the records for Datsun 710, Lotus Europa, and Ferrari Dino. The program retains only the Model, mpg, cyl, hp, and gear columns and displays the resulting DataFrame together with its shape.

### Functions Used

- `.loc[]` – Selects rows and columns using labels.
- `.shape` – Displays the dimensions of the resulting DataFrame.

### Code

```python
selected_cars = cars.loc[
    cars["Model"].isin([
        "Datsun 710",
        "Lotus Europa",
        "Ferrari Dino"
    ]),
    ["Model", "mpg", "cyl", "hp", "gear"]
]

print(selected_cars)
print(selected_cars.shape)
```
### Output

| Model | mpg | cyl | hp | gear |
|------|----:|----:|---:|----:|
| Datsun 710 | 22.8 | 4 | 93 | 4 |
| Lotus Europa | 30.4 | 4 | 113 | 5 |
| Ferrari Dino | 19.7 | 6 | 175 | 5 |

```text
Shape:
(3, 5)
```

---
