---
layout: single
title:  "회귀식 정렬(유전 알고리즘) "
---

# 회귀 분석
회귀분석은 데이터 변수들간에 함수관계를 파악하여 통계적 추론을 하는 기술이다.
좀더 쉽게 설명하자면, 독립변수에 대한 종속변수값의 평균을 구하는 방법입니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlsjIi%2FbtqCpQVSDQq%2FcYOKyEDDicbLxIpyDwkZw0%2Fimg.png)

# 단순 선형 회귀
회귀는 독립변수의 개수에 따라 1개인 경우는 단일 회귀 여러 개일 경우에는 다중 회귀로 나뉜다. 또 회귀 계수가 선형이냐 비선형이냐에 따라 선형 회귀와 비선형 회귀로 나눌 수 있다.

단순 선형 회귀는 독립변수도 하나, 종속변수도 하나인 선형 회귀이다. 예를 들어, 주택 가격이 주택의 크기로만 결정된다고 하면 2차원 평면에 직선(선형)형태의 관계로 표현할 수 있다. X축이 주택의 크기이고, Y축이 가격이라할 경우 1차 함수식으로 모델링할 수 있다.

# 유전알고리즘
유전 알고리즘은 자연세계의 진화과정에 기초한 계산 모델로서 존 홀랜드에 의해서 1975년에 개발된 전역 최적화 기법으로, 최적화 문제를 해결하는 기법의 하나이다.

# 돌연변이 연산
변이 연산은 유전자를 변일 시키는 것이다. 자연에서는 아주 드문일이고 안좋게 보인다. 하지만 유전 알고리즘에서 변이를 사용하면, 적합도를 상당히 증가시킬 수 있다. 하지만 좋지 않은 결과를 만들 가능성도 증가한다.
변이를 사용하지 않은면 선택과 교차 연산을 반복하다가 어느새부터 위 과정이 동질적인 해집단에서 정체될 수 있다. 탐색 알고리즘이 효율적으로 진행되지 못하기 때문에 평균 적합도가 향상되지 않는다. 그러면 평균 적합도 변화율이 정체되고, 최적해가 나온 것처럼 보일 수 있다. 변이는 임의 탐색과 동긍한 효과를 주며 유전적 다양성을 잃지 않게 한다.
변이 연산은 염색체에서 임의로 선택한 유전자를 뒤집는다. 예를 들어 염색체의 특정 유전자를 0 -> 1처럼 반대로 바꾼다. 변이는 모든 유전자에 일정한 확률로 일어날 수 있다. 변이율은 자연계에서도 꽤 낮기도 하고, 프로그래밍시 높게 잡으면 안좋은 결과를 만들 가능성도 커지기 때문에 보통 0.001 ~ 0.01 사이의 낮은 수치로 정한다.

1.초기 염색체 생성 연산

초기에는 이전 염색체가 존재하지 않기 때문에 선택된 염색체들로부터 자손을 생성할 수가 없다. 따라서, 초기 염색체를 생성하는 연산을 별도로 정의해야 한다. 유전 알고리즘에서 가장 많이 이용되는 방법은 어떠한 규칙도 없이 단순히 임의의 값으로 염색체를 생성하는 것이다. 예를 들어, 자바로 작성된 [코드 1]과 같은 소스 코드는 유전 알고리즘의 초기 염색체 생성 연산으로 이용될 수 있다.

<br/>

```c
def _generate_parent(length, geneSet, get_fitness):
chromosome_list = []
for i in range(0, 10):
    genes = []
    while len(genes) < length:
        sampleSize = min(length - len(genes), len(geneSet))
        genes.extend(random.sample(geneSet, sampleSize))
    fitness = get_fitness(genes)
    chromosome_list.append(Chromosome(genes, fitness))
return chromosome_list
```
염색체를 10개정도 생성하여, 리스트에 저장한다. 이때 유전자의 배열은 0부터 9까지 사이 숫자의 랜덤 값이다.

2.적합도를 계산하는 연산
유전 알고리즘에서는 자손을 생성하는 연산으로 주로 crossover라는 연산을 이용한다. Crossover 연산을 그림으로 표현하면, 아래의 [그림 2]와 같다.

![image]https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F2204125057DBC01320BE0C

<br/>

```c
 def get_fitness(guess, target):
fitness = 0
for expected, actual in zip(target, guess):
    if expected == actual:
        fitness += 5
    elif actual in target:
        fitness += 1

return fitness
```

3.적합도를 기준으로 염색체를 선택하는 연산

<br/>

```c
 def _generate_child(parent_list, geneSet, get_fitness):
child_list = []
fitness_percent_list = []
fitness_accum_list = []
fitness_sum = 0
for parent in parent_list:
    fitness_sum += parent.Fitness

for parent in parent_list:
    fitness_percent_list.append(parent.Fitness / fitness_sum)

fitness_sum = 0
for fitness_percent in fitness_percent_list:
    fitness_sum += fitness_percent
    fitness_accum_list.append(fitness_sum)

# Selection
for i in range(0, 10):
    rand = random.random()
    before = 0
    for j in range(0, len(fitness_accum_list)):
        if rand > before and rand <= fitness_accum_list[j]:
            child_list.append(copy.deepcopy(parent_list[j]))
            break
        before = fitness_accum_list[j]

```

부모들로부터 계산된 적합도 값을 모두 더한 후, 백분율로 환산하여 축적하여 저장한다. 이후 난수를 돌려서 걸린 염색체를 자식 염색체로 지정한다. 룰렛 휠 방식이다.

선택된 염색체들로부터 자손을 생성하는 연산

<br/>

```c
 def _generate_child(parent_list, geneSet, get_fitness):

crossover_rate = 0.20
selected = None
for i in range(0, len(child_list)):
    rand = random.random()
    if rand < crossover_rate:
        if selected is None:
            selected = i
        else:
            child_list[selected].Genes[2:], child_list[i].Genes[2:] = \
                child_list[i].Genes[2:], child_list[selected].Genes[2:]
            selected = None
            
    child_list[i].Fitness = get_fitness(child_list[i].Genes)
```

선택한 염색체 중 랜덤으로 선택하여 유전자를 교배 시킨다. 즉 숫자의 일부를 두 유전자끼리 교환시킨다.

돌연변이 연산

<br/>

```c
def _generate_child(parent_list, geneSet, get_fitness):
mutate_rate = 0.2
for i in range(0, len(child_list)):
    rand = random.random()
    if rand < mutate_rate:
        child = _mutate(child_list[i], geneSet, get_fitness)
        del child_list[i]
        child_list.append(child)
return child_list
```

기존의 염색체들로만 교배를 한다면 지역 최적점, 즉 원하는 값에 도달할 수가 없기 때문에, 광역 최적점에 도달하기 위해서는 돌연변이 연산을 섞어줘야 한다. 일정 확률로 돌연변이를 발생 시킨 후, 유전자의 일부를 치환하였다.

![image]https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F236D374857DBC2AF2C3A50

결과 값

<br/>

```c
target : 841532
820653	1/3	8	0:00:00.000997
491670	1/1	6	0:00:00.000997
763810	0/3	3	0:00:00.000997
642183	1/4	9	0:00:00.000997
702563	1/2	7	0:00:00.000997
721048	1/3	8	0:00:00.000997
978064	0/2	2	0:00:00.000997
543081	1/4	9	0:00:00.000997
841530	5/0	25	0:00:00.000997
493157	0/4	4	0:00:00.000997
average fitness : 8.1
new maximum fitness : 9.1
new maximum fitness : 13.6
new maximum fitness : 17.2
...중략...
new maximum fitness : 29.2
new maximum fitness : 29.6
new maximum fitness : 30.0
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
841532	6/0	30	0:00:00.038933
average fitness : 30.0

 target : 495367
450791	1/3	8	0:00:00
315478	1/3	8	0:00:00
068147	1/2	7	0:00:00
598437	2/3	13	0:00:00
385704	1/3	8	0:00:00
623759	0/5	5	0:00:00
253147	1/3	8	0:00:00
548967	2/3	13	0:00:00
067142	0/3	3	0:00:00
431768	2/2	12	0:00:00
average fitness : 8.5
new maximum fitness : 9.5
new maximum fitness : 11.0
...중략...
new maximum fitness : 29.1
new maximum fitness : 30.0
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
495367	6/0	30	0:00:00.025973
average fitness : 30.0
```
