## 가상환경 생성  
* 가상 환경은 아무 곳에서나 생성할 수 있다.  

`pyenv virtualenv` + 가상환경명  
`pyenv virtualenv   myDjango`


가상환경 지정  

* 가상환경 지정은 해당 디렉토리에서 지정한다.

`pyenv local` + 생성한 가상환경명  
`pyenv local myDjango `

## Dajngo설치
`pip install Django`



## project 생성
* mysite 라는 프로젝트를 생성합니다.  
`django-admin startproject mysite`

## 타임존 설정

mysite/setting.py  
`TIME_ZONE = 'Asia/Seoul'`


## 데이터베이스 생성하기
`python manage.py migrate`


## 서버실행
`python manage.py runserver`  

* 기본으로 8000번 포트로 접속한다.  
 
> http://127.0.0.1:8000/  

`python manage.py runserver 8001`  

* 8001번 포트로 접속할 수 있다.  

>http://127.0.0.1:8001/

## App 만들기
프로젝트 안에 app을 만들어 각각의 기능을 나눌 수 있습니다.  
여기서 blog라는 app을 만들어 봅니다.
   
1. blog app 생성  
`python manage.py startapp blog`

2. 생성된 blog 장고에서 사용을 명시  
 > mysite/setting.py
 
 ```
 INSTALLED_APPS = (
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        
        'blog.apps.BlogConfig',
    )
 ```



## model 만들기

1. `blog/models.py`에 생성할 코드를 작성합니다. 
 

## 데이터베이스 만들기
모델을 통해 작성된 코드를 데이터베이스에 방영할 수 있도록   
`python manage.py makemigrations blog`를 실행하여 줍니다.

데이터베이스에 적용합니다.   
`python manage.py migrate blog`


**참고** (데이터베이스 꼬이면 중요)
> * 특정한 곳으로 되돌리기  
 appname은 프로젝트 이름   
`python manage.py migrate` `appname` `__001`  
> * 모두 되돌리기  
`python manage.py migrate` `appname` `zero`




##장고관리자 생성하기
`python manage.py createsuperuser`  

아이디와 패스워드를 입력후 관리자 로그인 정보를 생성합니다.

`blog/admin.py`post app을  연결하여줍니다. 

```
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

## URl설정하기




## 뷰 생성하기
<br><br><br><br><br><br>

2017.02.09

* 여러 필드에서 ForeignKey를 가지면  makemigration 에서 오류가 남
그렇기 때문에 각각의 related_name=''을 지정해 주어야 함