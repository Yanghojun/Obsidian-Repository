
# Property
출처: https://www.daleseo.com/python-property/

사용 이유: **캡슐화**

Python에서 캡슐화 방법 2개 존재.
1. setter, getter 사용
2. property 사용

- setter, getter
```python
# setter, getter 사용
class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self._age = age

    def get_age(self):
        return self._age

    def set_age(self, age):
        if age < 0:
            raise ValueError("Invalid age")
        self._age = age
```

```python
# property 사용
class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self._age = age

    def get_age(self):
        return self._age

    def set_age(self, age):
        if age < 0:
            raise ValueError("Invalid age")
        self._age = age

    age = property(get_age, set_age)

# 출력
## 마치 attribute 쓰는것처럼 사용
## 그러나 로직 수행해서 검증 코드 넣을 수 있음
>>> person = Person("John", "Doe", 20)
>>> person.age
20
>>> person.age = -1
ValueError: Invalid age
>>> person.age = person.age + 1
>>> person.age
21
```

```python
# 바로 위 코드와 완벽하게 동일
class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, age):
        if age < 0:
            raise ValueError("Invalid age")
        self._age = age

>>> person = Person("John", "Doe", 20)
>>> person.age
20
>>> person.age = -1
ValueError: Invalid age
>>> person.age = person.age + 1
>>> person.age
21
```

쓰는건 속성처럼 그대로 쓰는데 수정은 못하게 하고 싶다?
property의 setter 안정해주면 됨.

```python
class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self._age = age

    @property
    def full_name(self):
        return self.first_name + " " + self.last_name
>>> person = Person("John", "Doe", 20)
>>> person.full_name
'John Doe'
```

# \*args, \*\*kwargs
- *(함수 입장에서)* \*args: literal obj 대신 positional args을 받겠다.
	- 함수 안에선 **Tuple** type이다.
- *(호출하는 입장에서)* positional args를 넘기겠다.
```python
def f(*args):
    print(args)
  
f(1,2,3)
f(*[1,2,3])  # f(1,2,3)과 완전 동일
f([1,2,3])  # 함수 내에서 ([1,2,3], )인 튜플로 바뀜
f()  # 함수 내에서 ([1,2,3], ) 인 튜플


# 출력결과
(1, 2, 3) 
(1, 2, 3) 
([1, 2, 3],) 
()
```

- *(함수 입장에서)* \*\*kwargs: literal obj 대신 keyword args를 받겠다.
	- 함수 안에선 **Dict** Type이다.
- *(호출하는 입장에서)* keyword args를 넘기겠다.
```python
def f(**kwargs):
    print(kwargs)


f(a=1, b=2, c=3)
f(**{'a':1, 'b':2, 'c':3})
f(a=1, 호준=2)
f()

# 출력결과
{'a': 1, 'b': 2, 'c': 3} 
{'a': 1, 'b': 2, 'c': 3}
{'a': 1, '호준': 2} 
{}
```

# getattr

if가 너무 많아지면 간소화 가능!

```python
import numpy as np

# 완전히 같은 코드
np.array([100])
getattr(np, "array")([100])
```

attribute를 **str**로 사용 가능하다는 것.
이를 활용하면 if가 반복될 때 줄여줄 수 있다.

```python
# 직접 짠 my_models.py를 임포트
import my_models as M

# my_model에 구현된 모델을 주어진 이름에 맞춰 반환
def build_neural_network(model_name):
  if model_name == 'googlenet':
    model = M.googlenet(args)
  elif model_name == 'vgg':
    model = M.vgg(args)
  elif model_name == 'resnet':
    model = M.resnet(args)



# 아래처럼 간소화된다.
import my_models as M
def build_neural_network(model_name):
  return getattr(M, model_name)(args)
```

# yield
```python
def f_with_yield(num):
	for i in range(num):
		print(i)
		yield i

def f_with_return(num):
	for i in range(num):
		print(i)
		return i
```

yield를 이해하기 위해선 2가지를 기억
1. def 밑에있는 코드들이 실행되는게 아니라, **실행할 준비만 하고 generator가 반환된다.**
2. generator는 **마지막 yield가 실행된 상태를 기억한다.**

