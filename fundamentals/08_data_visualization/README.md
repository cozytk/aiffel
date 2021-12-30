- Pandas, Matplotlib, Seaborn 이용 그래프 그리기
- 시각화를 해보고 EDA를 하며 인사이트 도출

# 몰랐던 것

### `%matplotlib inline`

IPython에서 사용하는 매직메서드. notebook을 실행한 브라우저에서 바로 그림을 볼 수 있게 해줌.

[ipython 의 매직명령어들](https://studymake.tistory.com/601)

### `plt.plot()`

- plot을 그릴 때는 figure() 객체를 생성하고 add_subplot으로 서브 플롯을 생성해야 함.
- 위 명령으로 그래프를 그리면 matplotlib은 가장 최근의 figure 객체와 서브플롯을 그림. 없으면 서브플롯 하나를 생성

### 범주형 데이터

- 주로 막대 그래프를 사용하여 수치를 요약
- 일반적으로 가로, 세로, 누적, 그룹화된 막대 그래프 사용

### 템플릿

```python
fig = plt.figure() # 새로운 figure 만들어줌
ax1 = add_subplot(1,1,1) or plt.plot(x=,y= ...)
plt.bar or plt.hist or sns.barplot(df, x=, y=) sns.scatterplot etc... #seaborn은 바로 df를 매개변수로 넣어줌
```

# 궁금한 것

```python
>>>

Text(0.5, 1.0, "Yuna's Test Result")
```

시각화를 하고 나오는 값 (0.5, 1.0)의 뜻

### plot 그리기

- plt.show()를 하면 아직 안 넣은 기존에 값이 나오거나 값이 제대로 나오지 않음 어떻게 처리?
- 다 그렸다가 처음부터 다시 그릴때 주의사항

- 한번에 하면 실행이 되고, 쉘을 나눠서 작업하면 plt따로fig따로 그려짐