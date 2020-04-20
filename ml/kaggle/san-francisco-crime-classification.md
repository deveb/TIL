---
description: 'https://www.kaggle.com/c/sf-crime'
---

# San Francisco Crime Classification

## Data preprocessing <a id="Data-preprocessing"></a>

```python
X = train.copy()
X['Dates'] = pd.to_datetime(X['Dates'], errors='coerce')
X['DayOfWeek'] = X['Dates'].dt.weekday
X['Day'] = X['Dates'].dt.day
X['Month'] = X['Dates'].dt.month
X['Year'] = X['Dates'].dt.year
X['Hour'] = X['Dates'].dt.hour
X['Minute'] = X['Dates'].dt.minute

# from datetime import datetime
# import time
# X['Timestamp'] = train['Dates'].apply(lambda x: time.mktime(datetime.strptime(x, '%Y-%m-%d %H:%M:%S').timetuple()))

from sklearn.preprocessing import LabelEncoder
le1 = LabelEncoder()
X['PdDistrict'] = le1.fit_transform(X['PdDistrict'])
# le2 = LabelEncoder()
# X['Address'] = le2.fit_transform(X['Address'])

X.drop(columns=['Dates', 'Descript', 'Resolution', 'Address'], inplace=True)

X.head()
```

```python
X.drop_duplicates(inplace=True)
X.shape
```

```python
X_test = test.copy()
X_test['Dates'] = pd.to_datetime(X_test['Dates'], errors='coerce')
X_test['DayOfWeek'] = X_test['Dates'].dt.weekday
X_test['Day'] = X_test['Dates'].dt.day
X_test['Month'] = X_test['Dates'].dt.month
X_test['Year'] = X_test['Dates'].dt.year
X_test['Hour'] = X_test['Dates'].dt.hour
X_test['Minute'] = X_test['Dates'].dt.minute
# from datetime import datetime
# import time
# X_test['Timestamp'] = test['Dates'].apply(lambda x: time.mktime(datetime.strptime(x, '%Y-%m-%d %H:%M:%S').timetuple()))


X_test['PdDistrict'] = le1.transform(X_test['PdDistrict'])
# X_test['Address'] = le2.transform(X_test['Address'])

X_test.drop(columns=['Id', 'Dates', 'Address'], inplace=True)
```

```python
from sklearn.model_selection import train_test_split

train_data = X.drop('Category', axis=1)
target_data = X['Category']

x_train, x_test, y_train, y_test  = train_test_split(train_data, target_data)

print(train_data.shape, x_train.shape, x_test.shape)
```

## Estimator

```python
from sklearn.ensemble import RandomForestClassifier

forest = RandomForestClassifier(n_estimators=100)
forest.fit(x_train, y_train)

print('training set accuracy:', forest.score(x_train, y_train))
print('test set accuracy:', forest.score(x_test, y_test))
```

```python
predictions = forest.predict_proba(X_test)

answer = train['Category'].value_counts().keys().tolist()
answer.sort()

output = pd.DataFrame({'Id': test['Id']})
output[answer] = pd.DataFrame(predictions)

output.to_csv('my_submission.csv', index=False)
print("Your submission was successfully saved!")
```

{% embed url="https://www.kaggle.com/eunbit/san-francisco-crime-classification" %}

