# Titanic: Machine Learning from Disaster

머신러닝을 사용해서 타이타닉 난파에서 어떤 승객이 살아남는지 예측하는 모델을 만든다.

## How to Get Started with Kaggle’s Titanic Competition \| Kaggle

{% embed url="https://www.youtube.com/watch?v=8yZMXCaFshs" %}

### 시작하기

1. 규칙을 확인하고 경쟁에 참가한다.
2. 데이터를 다운로드 한다.
3. 문제를 이해한다
4. EDA\(Exploratory Data Analysis\)
5. ML 모델을 훈련하고 조정하고 앙상블 한다.
6. 예측을 업로드해서 제출하고 점수를 받는다.

### 점수 개선하기

1. 데이터에 대해 더 배다.
2. 실험한다.
   1. 새 기능을 디자인하고 생성한다
   2. 다른 종류의 전처리를 시도한다
   3. 다른 종류의 ML 모델을 시도한다
   4. 여러 모델을 합쳐본다\(앙상블\)
3. 다른 사람 코드와 아이디어에서 배운다.

## Data

승객정보: name, age, gender, socio-economic class, etc

train.csv\(891\): 생존했는지 아닌지\(ground truth\) 정보가 있다.

test.csv: ground truth가 없다.

### Data dictionary

| **Variable** | **Definition** | **Key** |
| :--- | :--- | :--- |
| survival | Survival | 0 = No, 1 = Yes |
| pclass | Ticket class | 1 = 1st, 2 = 2nd, 3 = 3rd |
| sex | Sex |  |
| Age | Age in years |  |
| sibsp | \# of siblings / spouses aboard the Titanic |  |
| parch | \# of parents / children aboard the Titanic |  |
| ticket | Ticket number |  |
| fare | Passenger fare |  |
| cabin | Cabin number |  |
| embarked | Port of Embarkation | C = Cherbourg, Q = Queenstown, S = Southampton |

## Alexis Cook’s Titanic Tutorial

{% embed url="https://www.kaggle.com/alexisbcook/titanic-tutorial" %}

### 1. 제출을 해보자. gender\_submission.csv

![](../../.gitbook/assets/image%20%2834%29.png)

![](../../.gitbook/assets/image%20%2820%29.png)

### 2. 코딩 환경: Notebook

![](../../.gitbook/assets/image%20%283%29.png)

새 노트북을 생성한다. 무료 GPU 접근을 제공한다.

![](../../.gitbook/assets/image%20%2832%29.png)

데이터가 포함되어 있다.

![](../../.gitbook/assets/image%20%2833%29.png)

### 3. 코딩해보기

```python
train_data = pd.read_csv("/kaggle/input/titanic/train.csv")
train_data.head()

test_data = pd.read_csv("/kaggle/input/titanic/test.csv")
test_data.head()
```

```python
women = train_data.loc[train_data.Sex == 'female']["Survived"]
rate_women = sum(women)/len(women)

print("% of women who survived:", rate_women)

> % of women who survived: 0.7420382165605095

men = train_data.loc[train_data.Sex == 'male']["Survived"]
rate_men = sum(men)/len(men)

print("% of men who survived:", rate_men)

> % of men who survived: 0.18890814558058924
```

### 4. ML 모델 적용해보기

random forest 모델을 적용해 보자. 이 모델은 여러개의 트리들로 구성되어 있다.

![](../../.gitbook/assets/image%20%2831%29.png)

네개의 서로 다른 컬럼  \(**"Pclass"**, **"Sex"**, **"SibSp"**, and **"Parch"**\) 으로 패턴을 찾아 보자.

```python
from sklearn.ensemble import RandomForestClassifier

y = train_data["Survived"]

features = ["Pclass", "Sex", "SibSp", "Parch"]
X = pd.get_dummies(train_data[features])
X_test = pd.get_dummies(test_data[features])

model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=1)
model.fit(X, y)
predictions = model.predict(X_test)

output = pd.DataFrame({'PassengerId': test_data.PassengerId, 'Survived': predictions})
output.to_csv('my_submission.csv', index=False)
print("Your submission was successfully saved!")
```



```python
model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=1)
# X는 train_data, y는 train_data의 결과(Survived)
model.fit(X, y)
predictions = model.predict(X_test)
```

### 5. 제출

![](../../.gitbook/assets/image%20%2819%29.png)

![](../../.gitbook/assets/image%20%2810%29.png)



