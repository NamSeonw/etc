# api를 rest_framework를 사용해서 구성하기

> 파일 구조, root ai_api, app ai
```
├── ai
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-37.pyc
│   │   ├── admin.cpython-37.pyc
│   │   ├── models.cpython-37.pyc
│   │   ├── serializers.cpython-37.pyc
│   │   ├── urls.cpython-37.pyc
│   │   └── views.cpython-37.pyc
│   ├── admin.py
│   ├── apps.py
│   ├── migrations
│   │   ├── __init__.py
│   │   └── __pycache__
│   │       └── __init__.cpython-37.pyc
│   ├── models.py
│   ├── serializers.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
├── ai_api
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-37.pyc
│   │   ├── settings.cpython-37.pyc
│   │   ├── urls.cpython-37.pyc
│   │   └── wsgi.cpython-37.pyc
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
```

### 모듈 설치
```
$ pip install djangorestframework
```

### setting.py installed_apps에 rest_framework 추가
```
INSTALLED_APPS = [
    ...
    'rest_framework',
]
```

### serializers.py 생성
```
from rest_framework import serializers


class SimilarBooksSerializer(serializers.Serializer):

    similar_books = serializers.CharField()
    i2v_similar = serializers.CharField()
    d2v_similar = serializers.CharField()
    geometrics = serializers.CharField()
```
> db에서 모델을 사용하는 법은 따로 있으며, 위의 모델은 db모델 참조 없이 하는 코드

### root urls.py
```
from django.urls import path, include
from rest_framework import routers
from ai import views
router = routers.DefaultRouter()

router.register(r'similarbooks', views.SimilarBooksSet, basename='similarbooks')

urlpatterns = [
    path('', include(router.urls)),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```
> rest framework 모듈 사용시 각 앱의 url이 있는 형태가 아닌 메인에서 router.register로 등록하여 분기시켜주는 형태 인거같다.

### app views.py
```
from rest_framework import viewsets
from .serializers import *
from rest_framework.response import Response


class SimilarBooksSet(viewsets.ViewSet):

    def list(self, request):
        user_id = request.GET.get('user_id')
        book_seq = request.GET.get('book_seq')
        alpha = request.GET.get('alpha')
        beta = request.GET.get('beta')
        topn = request.GET.get('topn')

        data = result(user_id, book_seq, alpha, beta, topn)

        print(data)

        serializer = SimilarBooksSerializer(data, many=True)

        return Response(serializer.data)
```



### 내가 return 하고자 했던 결과 데이터 형태

```
[
  {
    'similar_books': ['207763296', '613423', '133313879', '613429', '2750505'],
    'i2v_similar': [0.5020011067390442, 0.6195163726806641, 0.4763231873512268, 0.6064468622207642, 0.4383927583694458], 
    'd2v_similar': [0.5308345556259155, 0.39557600021362305, 0.5036250948905945, 0.39555254578590393, 0.5423529744148254], 
    'geometrics': [0.516217, 0.495041, 0.489784, 0.489777, 0.48761]
  }
]
```
