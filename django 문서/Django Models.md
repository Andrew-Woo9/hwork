# *Django
<br>
#Models

<br>
## 기본사용법

> 장고 code  

```python
form django.db import models

class person(models.Model)
	first_name = models.CharField(max_length=30)
	second_name = models.CharField(max_length=30)
```
장고는 데이터베이스를 직접 생성하여 준다. 위와 같은 코드를 작성하면 아래와 같이 
SQL Query 문을 작성하여 준다.

> SQL Query  

```python
CREATE TABLE myapp_person (
	"id" serial NOT NULL PRIMARY KEY,
	"first_name" varchar(30) NOT NULL,
	"last_name"varchar(30) NOT NULL
);
```

<br>
## model 사용하기 
기본사용법을 통해  model을 만들고 이를 사용하기 위해서는 models.py를 포함하고 있는 모듈의 이름을 INSTALLED_APPS 세팅을 통해 추가해야 합니다. 

*MyappConfig 는  `Apps.py` 참조  

```python
INSTALLED_APPS = [
	#...
	'myapp.apps.MyappConfig'
	#...
]
```
###field option
[필드옵션 참조](https://docs.djangoproject.com/en/1.10/ref/models/fields/#model-field-types)

* **choices**
필드값을 튜플로 저장하여 활용할 수 있습니다. 

실제 DB에 저장되어지는 값음 S,M,L이지만  화면에 보여질때에는 저장값을 참조하여
'S'일때는 Small을 'M'일때는 Medium식으로 보여줍니다. 

```python
from django.db import models

class Person(models.Model):
    SHIRT_SIZES = (
        ('S', 'Small'),
        ('M', 'Medium'),
        ('L', 'Large'),
    )
    name = models.CharField(max_length=60)
    shirt_size = models.CharField(max_length=1, choices=SHIRT_SIZES)
```

* **help_text**  

```python
name = models.CharField('이름', max_length=60, help_text="성과 이름을 붙여 적어주세요.")
```  

### verbose field name

*ForeignKey*, *ManyToManyField*, 그리고 *OneToOneField*를 제외한 각각의 필드 첫 위치에 (`"설명"`,속성,속성)을 주어 별도의 verbose name을 정하기 않는다면 필드 속성으로 인식합니다.  
> 첫 위치에 `"설명"`을 이용한 경우  
 
```python
first_name = models.CharField("person's first name", max_length=30)
```

그런데 왜! ForeignKey, ManyToManyField, OneToOneField 는 첫 위치에`"설명"`을 사용할 수 없는까요 그것은 이 것들이 첫 위치체 특정값을 이미 다른 이유로 사용하고 있기 때문입니다 그래서  `verbose name`을 이용하여 설명을 넣어 줄 수 있습니다. 
  
> `verbose name`을 이용한 경우

```python
sites = models.ManyToManyField(Site, verbose_name="list of sites")
```


### Relationships
장고는 세가지 관계형 데이터베이스 테이블을 정의하는 방법을 제공합니다.   

1. 다 대 일 ( many to one )
2. 다 대 다 ( many ot many )
3. 일 대 일 ( one to one )

**Many-to-one relationships**
다대일 을 사용하려면 ForeignKey 를 사용합니다 .
ForeignKey에는 위치인수(a positional argument)가 필요합니다.   
예를 들어 학생들(Students)은 한명의 선생님(Teacher)을  갖는다면.
아래와 같습니다.  

> * 쪽수가 많은 쪽에서 하나인 쪽을 `ForeignKey`로 잡아준다.

```python
from django.db import models

class Teacher(models.Model)
	name = models.CharField(max_length=100)
	
	
class Students(models.Model)
	teacher = models.ForeignKey(Teacher, on_delete=models.CASCADE)
	name = models.CharField(max_length=100)	
```

**Many-to-Many relationships**

> * 둘중 어느 곳에  `ManyToManyField`를 사용할 수 있지만 이왕이면
> 조금 더 포함관계가 높은 곳이 좋다.

```python
from django.db. import models

class Topping(models.Model):
	#...

class pizza(models.Model):
	#...
	toppings = models.ManyToManyField(Topping)
```
* Extra field on many-to-manyfield  
**때로는** 다대가 관계일 때 표준 ManyToManyField만으로 처리할 수 있습니다. 그러나 두모델 간의 관계에 데이터를 연결해야 할 경우가 있습니다. 
 
> 중개모델지정 `through` 

단순한 다대다 관계를 떠나 예를 들자면 이런 경우가 있을 수 있습니다.
피자를 만들때 피자에 토핑이 추가되어 만들어진 시간의 경우 별도의 그룹을 `'through'` 설정 옵션(토핑이 추가되어 진 시간)을 통해 중개모델을 설정 /추가 /관리할 수 있습니다. 

```python
from django.db import models

class Topping(models.Model)
	name = models.CharField(max_length=100)
	
	def __str__(self):
		return self.name
		
class Pizza(models.Model)
	name = models.CharField(max_length=100)
	toppings = models.ManyToManyField(Topping, through='Products')
	
	def __str__(self):
		return self.name
		
class Products(models.Model)
	topping = models.Foreignkey(Topping, on_delete=models.CASCADE)
	pizza = models.ForeignKey(Pizza, on_delete=models.CASCADE)
	make_date = models.DateField()
		
```
> 중개모델의 몇가지 제한사항  

 1. 두개를 초과하는 `ForeignKey` 지정시에는 `through_fields` 사용하여 지정해야 합니다.
 2. 중간자 모델은 반드시 하나 외부키(외부클래스)를 가지거나. `ManytoManyField.through_fields`를 사용하여 외부적으로 지정하여야 합니다. 그렇지 않으면 검증 오류가 일어납니다. 
 3. 자기 자신을 통해 다대다 관계를 정의 할때는 중간자 모델을 사용하세요. 그리고 symmetrical=False를 사용해야 합니다. [필드참조](https://docs.djangoproject.com/en/1.10/ref/models/fields/#manytomany-arguments)

 
     
  `through_fields=('A', 'B')`  
  
```python
from django.db import models

class Topping(models.Model)
	name = models.CharField(max_length=100)
	
	def __str__(self):
		return self.name
		
class Pizza(models.Model)
	name = models.CharField(max_length=100)
	toppings = models.ManyToManyField(
		Topping,
		through='Products',
		through_fields=('Pizza', 'Topping'),
	)
	
	def __str__(self):
		return self.name
		
class Products(models.Model)
	topping = models.Foreignkey(Topping, on_delete=models.CASCADE)
	pizza = models.ForeignKey(Pizza, on_delete=models.CASCADE)
	cook = models.ForeignKey(
		Pizza,
		on_delete = models.CASCAED,
		related_name = "products_cook",
	) 
	make_date = models.DateField()
		
```

**One-to-One relationships**







**Abstract base classes**  
추상 클래스는 코드상 남아 있으며 하위 클래스에서 
추상 클랙스 속성들을 하위 클래스에 동일하게 생성하여 준다. 



Meta in heritance





#Qusries  

* 일반적인 경우는 객체.`save()`를 해주어야 한다.

```python
>>> from blog.models import Blog
>>> b = Blog(name='Beatles Blog', tagline='All the latest Beatles news.')
>>> b.save()
```

```python
b5.name = 'New name'
b5.save()
```

**만약** 자동으로 저장을 하기 위해서는 `create()`를 사용하여야 한다.

* ManyToManyField 는  add()로  save() 까지 같이 한다. 

```python
>>> from blog.models import Author
>>> joe = Author.objects.create(name="Joe")
>>> entry.authors.add(joe)
```
* 여러개의 ManyToManyField 를 한번에 저장하기

```python
>>> john = Author.objects.create(name="John")
>>> paul = Author.objects.create(name="Paul")
>>> george = Author.objects.create(name="George")
>>> ringo = Author.objects.create(name="Ringo")
>>> entry.authors.add(john, paul, george, ringo)
```