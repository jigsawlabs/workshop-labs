

### Our Data

| Attended College | Under Thirty | Borough   | Income | Customer |
| ---------------- | ------------ | --------- | ------ | :------: |
| ?                | Yes          | Manhattan | < 55   |    0     |
| Yes              | Yes          | Brooklyn  | < 55   |    0     |
| ?                | No           | Brooklyn  | < 55   |    1     |
| No               | No           | Queens    | > 55   |    1     |
| ?                | No           | Queens    | < 55   |    1     |
| Yes              | No           | Queens    | >55    |    0     |
| Yes              | No           | Queens    | >55    |    0     |
| Yes              | Yes          | Manhattan | >55    |    0     |

#### Our Procedure

```
Given a subset of data
For each feature in our dataset
	○ Split the data according to the feature
	○ Compute consistency of data in each split 
Choose the feature with the highest consistency to split the data
Repeat for remaining subset
```



#### 1. Split the data according to each feature



```
Given a subset of data
For each feature in our dataset
	○ Split the data according to the feature
	○ Compute consistency of data in each split 
```

Each of the tests



```mermaid
graph LR
A(Customer Leads)

B{College?}
		B -->|Yes|0,0,0,0
		B -->|No|1
		B -->|?|0,1,1

D{Under 30?}
		D -->|Yes| 0,0,0
		D -->|No| 1,1,1,0,0

F{Borough}
		F -->|Brooklyn| 1,0
		F -->|Queens| 1,1,0,0
    F -->|Manhattan| 0,0
    
G{Income}
		G -->|under 55k| 0,1,0,1
    G -->|over 55k| 1,0,0,0
```

#### 2. Compute consistency of data in each split 





#### 3. Choose the feature with the highest consistency 



```mermaid
graph LR
A(Customer Leads)

B{College?}
		B -->|Yes|1,1,1,1
		B -->|No|0
		B -->|?|0,1,1
```



And turned it into this.

```mermaid
graph LR
A(Customer Leads)

B{College?}
		B -->|Yes|Customer
		B -->|No|Not-Customer
		B -->|?|***
```

#### 4. Repeat for remaining subset



| Attended College | Under Thirty | Borough   | Income | Customer | Customer Predictions |
| ---------------- | ------------ | --------- | ------ | :------: | -------------------- |
| ?                | Yes          | Manhattan | < 55   |    0     | ?                    |
| Yes              | Yes          | Brooklyn  | < 55   |    0     | 1                    |
| ?                | No           | Brooklyn  | < 55   |    1     | ?                    |
| No               | No           | Queens    | > 55   |    1     | 0                    |
| ?                | No           | Queens    | < 55   |    1     | ?                    |
| Yes              | No           | Queens    | >55    |    0     | 1                    |
| Yes              | No           | Queens    | >55    |    0     | 1                    |
| Yes              | Yes          | Manhattan | >55    |    0     | 1                    |

Scoped down to this

| Attended College | Under Thirty | Borough   | Income | Customer | Customer Predictions |
| ---------------- | ------------ | --------- | ------ | :------: | -------------------- |
| ?                | Yes          | Manhattan | < 55   |    0     | ?                    |
| ?                | No           | Brooklyn  | < 55   |    1     | ?                    |
| ?                | No           | Manhattan | < 55   |    1     | ?                    |

Remember our procedure.

```
Given a subset of data
For each feature in our dataset
	○ Split the data according to the feature
	○ Compute consistency of data in each split 
Choose the feature with the highest consistency to split the data
Repeat for remaining subset
```





```mermaid
graph LR
B{Under 30?}
		B -->|Yes|0
		B -->|No|1,1
C{Borough}
		C -->|Manhattan|0,1
		C -->|Brooklyn|1
D{Income}
		D -->|under 55|1,0,1

```

Add to decision tree

```mermaid
graph LR
A(Customer Leads)

B{College?}
		B -->|Yes|Customer
		B -->|No|Not-Customer
		B -->|?|C{Under 30?}
		C -->|Yes| D[Not Customer]
    C -->|No| E[Customer]
```



Predicting new data

| Attended College | Under Thirty | Borough   | Income |
| ---------------- | ------------ | --------- | ------ |
| ?                | No           | Manhattan | < 55   |

### Working with larger datasets

1. How can we count only the data in homogenous groups if no group is homogenous

2. How do we make predictions with data that is not perfectly homogenous

