# 새로 알게된 것

### EDA (Exploratory Data Analysis)

- 더 좋은 데이터 분석과 더 좋은 머신러닝 모델을 만들기 위한 필수적인 과정

### Matplotlib 과 Seaborn

- seaborn은 matplotlib의 상위 버전
- matplotlib이 조금 더 단순하지만 raw한 느낌, seaborn은 보다 고급화된 그래프

### set자료형으로 만들어주어 중복없는 길이 구하기

ex)

`len(set(pokemon["#"]))`

### 차집합을 구하여 서로 다른점 찾기

```python
set(pokemon["Type 2"]) - set(pokemon["Type 1"])
```

### Total값에 따른 분포 plot

```python
sns.scatterplot(data=pokemon, x="Type 1", y="Total", hue="Legendary")
```

- hue 는 해당 feature을 True|False 로 나타내줌

### 여러 subplot들 seaborn으로 그리기

```python
figure, ((ax1, ax2), (ax3, ax4), (ax5, ax6)) = plt.subplots(nrows=3, ncols=2)
figure.set_size_inches(12, 18)  # 화면 해상도에 따라 그래프 크기를 조정해 주세요.

sns.scatterplot(data=pokemon, y="Total", x="HP", hue="Legendary", ax=ax1)
sns.scatterplot(data=pokemon, y="Total", x="Attack", hue="Legendary", ax=ax2)
sns.scatterplot(data=pokemon, y="Total", x="Defense", hue="Legendary", ax=ax3)
sns.scatterplot(data=pokemon, y="Total", x="Sp. Atk", hue="Legendary", ax=ax4)
sns.scatterplot(data=pokemon, y="Total", x="Sp. Def", hue="Legendary", ax=ax5)
sns.scatterplot(data=pokemon, y="Total", x="Speed", hue="Legendary", ax=ax6)
plt.show()
```

### data는 한 feature

```python
fig, ax = plt.subplots()
fig.set_size_inches(8, 4)

sns.scatterplot(data=legendary, y="Type 1", x="Total")
plt.show()
```

### 알파벳이 아닌 문자를 포함하는 경우 색출

```python
pokemon["Name_nospace"] = pokemon["Name"].apply(lambda i: i.replace(" ", ""))
pokemon.tail()
```

1. `isalpha()` 함수를 사용하여 알파벳인지 아닌지 확인
2. 띄어쓰기의 경우 `isalpha()` 함수가 동작하지 않기 때문에 띄어쓰기를 붙혀주는 과정이 필요
3. `replace()` 함수를 활용

### 데이터프레임 각 행에 대하여 함수 수행, 후 일반 리스트 변환

```python
all_tokens = list(legendary["Name"].apply(tokenize).values)

token_set = []
for token in all_tokens:
    token_set.extend(token)

print(len(set(token_set)))
print(token_set)
>>>

[array(['Articuno'], dtype='<U8'), array(['Zapdos'], dtype='<U6'), array(['Moltres'], dtype='<U7'), array(['Mewtwo'], dtype='<U6'), array(['Mewtwo', 'Mega', 'Mewtwo', 'X'], dtype='<U6'), array(['Mewtwo', 'Mega', 'Mewtwo', 'Y'], dtype='<U6'), array(['Raikou'], dtype='<U6'), array(['Entei'], dtype='<U5'), array(['Suicune'], dtype='<U7'), array(['Lugia'], dtype='<U5'), array(['Ho'], dtype='<U2'), array(['Regirock'], dtype='<U8'), array(['Regice'], dtype='<U6'), array(['Registeel'], dtype='<U9'), array(['Latias'], dtype='<U6'), array(['Latias', 'Mega', 'Latias'], dtype='<U6'), array(['Latios'], dtype='<U6'), array(['Latios', 'Mega', 'Latios'], dtype='<U6'), array(['Kyogre'], dtype='<U6'), array(['Kyogre', 'Primal', 'Kyogre'], dtype='<U6'), array(['Groudon'], dtype='<U7'), array(['Groudon', 'Primal', 'Groudon'], dtype='<U7'), array(['Rayquaza'], dtype='<U8'), array(['Rayquaza', 'Mega', 'Rayquaza'], dtype='<U8'), array(['Jirachi'], dtype='<U7'), array(['Deoxys', 'Normal', 'Forme'], dtype='<U6'), array(['Deoxys', 'Attack', 'Forme'], dtype='<U6'), array(['Deoxys', 'Defense', 'Forme'], dtype='<U7'), array(['Deoxys', 'Speed', 'Forme'], dtype='<U6'), array(['Uxie'], dtype='<U4'), array(['Mesprit'], dtype='<U7'), array(['Azelf'], dtype='<U5'), array(['Dialga'], dtype='<U6'), array(['Palkia'], dtype='<U6'), array(['Heatran'], dtype='<U7'), array(['Regigigas'], dtype='<U9'), array(['Giratina', 'Altered', 'Forme'], dtype='<U8'), array(['Giratina', 'Origin', 'Forme'], dtype='<U8'), array(['Darkrai'], dtype='<U7'), array(['Shaymin', 'Land', 'Forme'], dtype='<U7'), array(['Shaymin', 'Sky', 'Forme'], dtype='<U7'), array(['Arceus'], dtype='<U6'), array(['Victini'], dtype='<U7'), array(['Cobalion'], dtype='<U8'), array(['Terrakion'], dtype='<U9'), array(['Virizion'], dtype='<U8'), array(['Tornadus', 'Incarnate', 'Forme'], dtype='<U9'), array(['Tornadus', 'Therian', 'Forme'], dtype='<U8'), array(['Thundurus', 'Incarnate', 'Forme'], dtype='<U9'), array(['Thundurus', 'Therian', 'Forme'], dtype='<U9'), array(['Reshiram'], dtype='<U8'), array(['Zekrom'], dtype='<U6'), array(['Landorus', 'Incarnate', 'Forme'], dtype='<U9'), array(['Landorus', 'Therian', 'Forme'], dtype='<U8'), array(['Kyurem'], dtype='<U6'), array(['Kyurem', 'Black', 'Kyurem'], dtype='<U6'), array(['Kyurem', 'White', 'Kyurem'], dtype='<U6'), array(['Xerneas'], dtype='<U7'), array(['Yveltal'], dtype='<U7'), array(['Zygarde', 'Forme'], dtype='<U7'), array(['Diancie'], dtype='<U7'), array(['Diancie', 'Mega', 'Diancie'], dtype='<U7'), array(['Hoopa', 'Hoopa', 'Confined'], dtype='<U8'), array(['Hoopa', 'Hoopa', 'Unbound'], dtype='<U7'), array(['Volcanion'], dtype='<U9')]
65
['Articuno', 'Zapdos', 'Moltres', 'Mewtwo', 'Mewtwo', 'Mega', 'Mewtwo', 'X', 'Mewtwo', 'Mega', 'Mewtwo', 'Y', 'Raikou', 'Entei', 'Suicune', 'Lugia', 'Ho', 'Regirock', 'Regice', 'Registeel', 'Latias', 'Latias', 'Mega', 'Latias', 'Latios', 'Latios', 'Mega', 'Latios', 'Kyogre', 'Kyogre', 'Primal', 'Kyogre', 'Groudon', 'Groudon', 'Primal', 'Groudon', 'Rayquaza', 'Rayquaza', 'Mega', 'Rayquaza', 'Jirachi', 'Deoxys', 'Normal', 'Forme', 'Deoxys', 'Attack', 'Forme', 'Deoxys', 'Defense', 'Forme', 'Deoxys', 'Speed', 'Forme', 'Uxie', 'Mesprit', 'Azelf', 'Dialga', 'Palkia', 'Heatran', 'Regigigas', 'Giratina', 'Altered', 'Forme', 'Giratina', 'Origin', 'Forme', 'Darkrai', 'Shaymin', 'Land', 'Forme', 'Shaymin', 'Sky', 'Forme', 'Arceus', 'Victini', 'Cobalion', 'Terrakion', 'Virizion', 'Tornadus', 'Incarnate', 'Forme', 'Tornadus', 'Therian', 'Forme', 'Thundurus', 'Incarnate', 'Forme', 'Thundurus', 'Therian', 'Forme', 'Reshiram', 'Zekrom', 'Landorus', 'Incarnate', 'Forme', 'Landorus', 'Therian', 'Forme', 'Kyurem', 'Kyurem', 'Black', 'Kyurem', 'Kyurem', 'White', 'Kyurem', 'Xerneas', 'Yveltal', 'Zygarde', 'Forme', 'Diancie', 'Diancie', 'Mega', 'Diancie', 'Hoopa', 'Hoopa', 'Confined', 'Hoopa', 'Hoopa', 'Unbound', 'Volcanion']
```

### 문자열에 특정 구문이 있는가

```python
for token, _ in most_common:
    pokemon[token] = pokemon["Name"].str.contains(token)

pokemon.head(10)
```

`contains()` 함수 사용

### 부울 데이터로 변환

- 문자열 데이터는 소중한 정보를 가지고 있지만, 문자열 그대로 학습에 사용할 수는 없습니다
- 문자열 데이터를 숫자나 부울 데이터로 변환해서 정보를 넣어주면 모델의 성능을 올리는 데에 도움을 줄 수 있습니다.

### 베이스라인 모델

- 가장 기초적인 방법으로 만든 모델
- 성능은 안 좋을지 모르지만, 성능 하한선을 제공함으로써 우리가 새롭게 만들 모델이 맞는 방향으로 가고 있는지 확인할 수 있게 도와줌

### 정확도

- target이 개체에 비해 훨씬 적은경우라면, 기본적인 정확도가 높음 따라서 별 의미 없음

---

# 더 궁금한 것

### 10-4

데이터셋을 판다스로 불러오기

legendary = pokemon[pokemon["Legendary"] == True].reset_index(drop=True)

- 0부터 시작하는 것은 인덱스가 아님 (기본 인덱스 느낌)
- 그렇다면 인덱스를 drop할일이 없는데 왜?

→ reset_index를 해주지 않으면 기존의 인덱스가 남아있음 (0부터 시작하는 것이 아님), 따라서 index_drop을 통해서 없애주는것. drop=True를하지 않으면 기존의 인덱스가 인덱스라는 새로운 컬럼이 되어 보존됨

### 10-7

```python
len(list(set(pokemon["Type 1"]))), len(list(set(pokemon["Type 2"])))
```

- 왜 set을 list로 만든다음에 길이를 잴까?

### Matplotlib 캔버스에 seaborn으로 그리고 그럴 수가 있는건가?

- 넵

### countplot의 order

```python
plt.figure(figsize=(12, 10))  # 화면 해상도에 따라 그래프 크기를 조정해 주세요.

plt.subplot(211)
sns.countplot(data=ordinary, x="Type 2", order=types).set_xlabel('')
plt.title("[Ordinary Pokemons]")

plt.subplot(212)
sns.countplot(data=legendary, x="Type 2", order=types).set_xlabel('')
plt.title("[Legendary Pokemons]")

plt.show()
```

- order가 무슨 역할을 하는거지? type들이 알파벳 기준 오름차순으로 정렬되는 것도 아니다

**공식 문서 설명**

*Order to plot the categorical levels in, otherwise the levels are inferred from the data objects.*

### `df.values()`

- values 메소드를 사용하면 데이터프레임이 np arrray 배열로 변환

pokemon["Name_nospace"] = pokemon["Name"].apply(lambda i: i.replace(" ", ""))
pokemon.tail()