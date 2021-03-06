## swagger 적용하기

> django로 어플리케이션을 생성할 때 swagger를 적용, 활용하는 방법을 정리한 문서입니다.



### 0. 준비

먼저 django와 django를 설치할 가상환경을 구성해야 합니다.  가상환경은 conda, virtualenv 등 여러 개의 옵션을 선택할 수 있지만, 여기서는 python 3.4 이상에 기본적으로 제공되는 pyenv를 사용하겠습니다.



#### **가상환경 구성**

```bash
$ python -m venv env
```



#### **django 설치**

django의 버전은 어떤 버전을 선택하든 큰 상관은 없습니다. 본인의 기준이나 프로젝트에서 합의된 버전을 설치하면 됩니다. 

```bash
pip install django
```



#### django project 생성

swagger를 적용하기 위해서는 사전에 swagger를 적용할 프로젝트를 생성해야 합니다. 

```

```



#### DB 만들기

```
```



### 1.  swagger 적용

여기서는 drf-yasg를 사용해 swagger를 적용하겠습니다. 이하의 내용은 [공식 문서](https://drf-yasg.readthedocs.io/en/stable/readme.html)를 참고했습니다. 

#### drf-yasg install

```
pip install -U drf-yasg
```

#### settings.py 수정

```python
INSTALL_APPS=[
...
'django.contrib.staticfiles',
'drf_yasg'
...
]
```

#### urls.py 수정

```python
...
from rest_framework import permissions
from drf_yasg.views import get_schema_view
from drf_yasg import openapi

...

schema_view = get_schema_view(
   openapi.Info(
      title="Snippets API",
      default_version='v1',
      description="Test description",
      terms_of_service="https://www.google.com/policies/terms/",
      contact=openapi.Contact(email="contact@snippets.local"),
      license=openapi.License(name="BSD License"),
   ),
   public=True,
   permission_classes=(permissions.AllowAny,),
)

urlpatterns = [
   url(r'^swagger(?P<format>\.json|\.yaml)$', schema_view.without_ui(cache_timeout=0), name='schema-json'),
   url(r'^swagger/$', schema_view.with_ui('swagger', cache_timeout=0), name='schema-swagger-ui'),
   url(r'^redoc/$', schema_view.with_ui('redoc', cache_timeout=0), name='schema-redoc'),
   ...
]
```

