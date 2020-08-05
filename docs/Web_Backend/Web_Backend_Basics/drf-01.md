---
layout: default
title: drf 01
parent: Backend Basics
grand_parent: Web Backend
nav_order: 7

---


- generic
    - django.views.generic.list, django.views.generic.detail, django.views.generic.edit 에서 import 할 수 있는게 많다!  
    

```python
```


```python
//views.py

class BlogCreate(CreateView):
    model = ClassBlog //나는 모델에서 ClassBlog를 쓰고싶어!
    fields = ['title','body'] //모델 필드 지정할거야! 이건 내가 입력할거야~
    success_url = reverse_lazy('list') //블로그 글이 성공적으로 만들어지면 list이름을 가진 url로 redirect 해준다


```
reverse_lazy 외에 get_absolute_url() 또는 reverse() 알아두기


html 템플릿 연결하기
ListView 를 상속받은거는 (소문자모델)_list.html

form입력공간을 가지고 있는 html : (소문자모델)_form.html

상세 페이지를 담은 html: (소문자모델)_detail.html

DeleteView: (소문자모델)_confirm_delete.html

근데 그냥 마음대로 지어도됨 그러려면 template_name = 'classcrude/list.html' 을 views.py의 class 안에 써주면 됨

그리고 pk값은 Object에 다 저장된다. 
for blog in object_list
이렇게 프런트에서 불러온다.

근데 object_list를 여러개 불러오고 싶다면??

이것 또한 views.py 의 class에서 고유한 object_list 이름을 설정해주면 된다! 
context_object_name = 'blogpost' 
이렇게 하면
for blog in blogpost 
이렇게 프런트에서 쓸 수 있다! 


REST : HTTP를 이용해 통신하는 네트워크상에서 정한 약속, 분산 하이퍼미디어 시스템을 위한 소프트웨어 설계형식

Representation: 자원을 대표하는 단어, 식별자로
State Transfer: 자원의  상태를 전송하는 방법

자원: 인터넷에서 제공하고 얻을 수 있는 모든 것

자원을 이름으로 구분하여 상태를 전송하는 방법

이것이 왜 필요할까? 왜 REST?
- 웹의 독립적인 운용과 발전의 측면에서 필요하다. 
- 우리의 인터넷은 발전하는데, hTTP를 활용한 프로토콜도 발전을 해나가야하는데, 새 패치버전이 나왔다고 해서 모든 웹과 서버에 알려줄 수는 없다. 따라서 하휘 호환을 깨뜨리지 않고 패치를 하고 업데이트를 할 수 있기 위해 도와주는 설계방법이 REST이다.  

REST 설계 조건: REST가 되기 위한 필요충분조건  
- Server -client
- STATELESS: client의 이전 상태를 기록하지 않는 것을 의미함 
- CACHE: 캐시처리기능
- Uniform Interface :일관된 인터페이스
- Layered System : 다층적인 시스템
- Code - on - Demand: js처럼 원격제에서 

API
Application Program Interface

- 서버가 요리사라면, Api는 손님client에게 요리를 가져다 주는 웨이터 역할이다. 
- 그리고 형식에 맞추어서 rerquest를 받고 response를 가져다 준다. 이러한 형식은 API 문서 라고 비유할 수 있다.  

REST API는 무엇일까?
REST 아키텍쳐 스타일을 따르는 API
이러한 API를 RESTful 하다, 라고 표현한다.  

json
- 모든 태그가 만들어져 있는 것도 아님
- 만든이가 정의하기 나름이어서..
- 그것만 봐서는 무슨 뜻인지 이해가 안갈 수도 있다. 

RESTful 하기는 어렵다! uniform Interface는 어려워~
- self-descriptive emssages
    - 메세지는 그 하나만으로 모든 것이 설명되어야한다. 예를 들어 편지에는 목적지, 송신지, 어떤 언어,문법으로 되어있는, 등등이 있어야한다. 즉, Host 도메인, content type 헤더, json 명세 등등을 가지고 있는 json이 가장 바람직하다. 하지만 대부분의 RESTful들은 이런것들을 모두 가지고 있지는 않음.
    요즘 API는 self-descriptive 하지 않아~
    - HATEOAS를 잘 지키고 있지 못하다!  


(Model)From vs (Model)Serializer
Django에는 Form/ModelForm
DRF에는 Serializer/ModelSerializer.
이 둘 모두 Model 로부터 Field를 읽어온다, 그리고 읽어온 데이터의 유효성 검사를 해준다. 
그 차이는 장고의 form은 HTML Form을 읽어오고, DRF는 Json을 가져온다.


Serializer 파일 안에는?
두가지를 import 해야함
1. from .models import Post
2. from rest_framework import serializers

Serializer가 있는 views.py는?
1. from rest_framework import viewsets
2. from .models import Post
3. .serializer import PostSerializer



class ViewSet(ViewSetMixin, views.APIView): //ViewSetMixin, views.APIView 이 두개를 묶어준다
    """
    The base ViewSet class does not provide any actions by default.
    """
    pass


class GenericViewSet(ViewSetMixin, generics.GenericAPIView): //ViewSetMixin, generics.GenericAPIView 이 두개를 묶어준다 
    """
    The GenericViewSet class does not provide any actions by default,
    but does include the base set of generic view behavior, such as
    the `get_object` and `get_queryset` methods.
    """
    pass

class ReadOnlyModelViewSet(mixins.RetrieveModelMixin,
                           mixins.ListModelMixin,
                           GenericViewSet):
    """
    A viewset that provides default `list()` and `retrieve()` actions.
    """
    pass

1. RetrieveModelMixin
retrive() 메소드 

2. mixins.ListModelMixin
list() 메소드

즉,ReadOnlyModelViewSet 는 특정 레코드를 가져다 주는 것을 일단 수행하고, list를 통해 레코드들의 목록을 가져다주는 일을 수행한다. 특정 레코드들을 읽을 수 있게 도와준다.  
읽기 기능만 필요하면, 
class UserViewSet(viewsets.ReadOnlyModelViewSet):
    """
    This viewset automatically provides `list` and `detail` actions.
    """
    queryset = User.objects.all()
    serializer_class = UserSerializer

이렇게 써주면 된다. 


class ModelViewSet(mixins.CreateModelMixin,
                   mixins.RetrieveModelMixin,
                   mixins.UpdateModelMixin,
                   mixins.DestroyModelMixin,
                   mixins.ListModelMixin,
                   GenericViewSet):
    """
    A viewset that provides default `create()`, `retrieve()`, `update()`,
    `partial_update()`, `destroy()` and `list()` actions.
    """
    pass


from rest_framework.decorators import action
from rest_framework.response import Response //response 임포트 

class SnippetViewSet(viewsets.ModelViewSet):
    """
    This viewset automatically provides `list`, `create`, `retrieve`,
    `update` and `destroy` actions.

    Additionally we also provide an extra `highlight` action.
    """
    queryset = Snippet.objects.all()
    serializer_class = SnippetSerializer
    permission_classes = [permissions.IsAuthenticatedOrReadOnly,
                          IsOwnerOrReadOnly]

    @action(detail=True, renderer_classes=[renderers.StaticHTMLRenderer]) //Response를 어떤 형식으로 Rendering 시킬 것인가!
    def highlight(self, request, *args, **kwargs):
        snippet = self.get_object()
        return Response(snippet.highlighted)

    def perform_create(self, serializer):
        serializer.save(owner=self.request.user)

- ViewSet는 CRUD가 두줄로 끝난다, 하지만 다른 Logic (CRUD외의) 들은 어떻게 하는것일까.
- 임의의 View 설계는 액션 데코레이터가 필요하다!
```
@action()
def func()
...
```
이렇게 하면 된다!

그리고, 일단 내가 보내는 response로 와야하니까 response를 import!
Custom API의 Default Method 는 GET!!!
하지만, action의 format 인자는 지정 가능

method를 post 로 하고싶으면,
@action(method=['post'])

얍을 띄우는 custom api는, 

@action(detail=True, renderer_classes=[renderers.StaticHTMLRenderer])
def highlight(detail=True, request, *args, **kwargs):
        return HttpResponse("얍")

**notification 
https://www.django-rest-framework.org/community/3.8-announcement/#deprecations
list router, detail router 는 action 으로 통합되었음


Path() 묶어주기
== path 함수의 두번째 인자를 묶어야한다!
이 일을 .as_view()가 해준다.
이것은 dictionary 형식으로 인자를 받는다!
as_view({'http_method':'처리할_함수'})
```
PostViewSet.as_view({
    'get':'retrieve',
    'put':'update',
    'patch':'partial_update',
    'delete':'destroy'
})

위는 보통의 관례인데, 

이거를 다 자동으로 매핑해주는 것이 Default Router이다!  
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from snippets import views

# Create a router and register our viewsets with it.
router = DefaultRouter()
router.register(r'snippets', views.SnippetViewSet) //첫번째 인자 snippets는 ~.com/snippets의 의미이다. 그리고 두번째는 함수이다! 
router.register(r'users', views.UserViewSet)

# The API URLs are now determined automatically by the router.
urlpatterns = [
    path('', include(router.urls)),
]


Filtering vs Search
Filtering: request 걸러서 보내기
Search: Response를 전달받고, 특정 모델의 column을 대상으로 문자열 검색 진행 

## 내가 보낸 http request 참조하기

내가보낸 리퀘: self.request
내가 보낸 리퀘의 user: Self.request.user

내가보낸 GET request: Self.request.GET = self.reqeust.query_param
내가 보낸 POST: Self.reqeust.POST


## 필터링해보기
def get_queryset(self):
    #여기 내부에서 퀴리셋을 지지고 볶은 ㄷㅏ음에
    #예를 들어 qs를 쿼리셋이라고 하면
    return qs

이렇게 한다!

def get_queryset(self):
    #여기 내부에서 퀴리셋을 지지고 볶은 ㄷㅏ음에
    qs = super().get_queryset()
    qs = qs.filter(author__id=3)
    #.filter 아니면 .exclude를 써도 된다
    return qs

만약 지금 로인한 사람의 글만 필터링 하는것은?

def get_queryset(self):
    qs=super().get_queryset()
    #만약 로그인이 되어있다면 유저의 글 필터링
    if self.request.user.is_authenticated:
        qs=qs.filter(author=self.request.user)
    #로그인 안되어 있다면 비어있는 쿼리셋을 리턴해라!
    else:
        qs=qs.none()
    


검색은
from rest_framework.filters import SearchFilter 
를 임포트하고,

class UserPostViewSet(viewsets.ModelViewSet):
    queryset = UserPost.objects.all()
    serializer_class = UserSerializer

    filter_backends = [SearchFilter]
    search_fields=('title',)


Authentication 설정은 1. 전역으로 2. 뷰단에서 할 수 있다.  


Basic Authentication?
- HTTP 자체 기본인증에 기반한 ㅇ니증 방식
- HTTP 제어 헤더로 넘긴 ID, PW를 base 64 encoding하는 방식으로 구현함

TokenAuthentication
- client가 인증요처을하면, 그 사람에게 유일한 key값을 준다. 이 과정은 Token 헤더로 이루어진다!

SessionAuthentication
- basic 과 더불어 장고의 기본 인증 시스템
- 로그인이 될 때 마다의 세션을 관리한다
- 로그인 될 때 마다 reqeust 속의 session 정보를 참조해서 인증을 참조한다


permission?
view 호출시 가장 먼저 체킹한다! 
authentication을 기반으로 체크한다. 
reqeust.user, request.auth를 기반으로 체크한다!

permission 설정
1. settings.py 전역 설정
2. view 마다 설정

- AllowAny(default): 인증 안되어도 전부 허용
- is Authenticated : 인증된 해들만 허용
- isAdminUser : staff user만 요청 허용, User.is_staff ==True 일 때만 허용한다
- isAuthenticatedOrReadOnly: 비인증 요청에 대해서는 읽기만 허용하겠다. 

other:
DjangoModelPermissions ... 
django.contrib.auth 참고하기


token authentication 수행과정
1. Username, password 와 1:1 매칭되는 고유 key 생성, 발급
(User instance의 생성에 따라 자동으로 생성되는 것은 아니다!) 
 1) rest_frameworkd/authtoken/views.py의 ObtainAuthToken을 이용한 생성
 2) python 명령어를 통한 토큰 발급 생성 ---> python manage.py drf_create_token<username>
 python manage.py drf_create_token -r<username>


rest_framework.authtoken을 app에도 추가해줘야함!
python manage.py migrate
도 해줘야한다!
그 이유는, authtoken/models.py의 OneToOneField를 이용해 Token 을 발급해야하기 때문이다..

자동으로 토큰을 생성하게 하려면?
signal을 이용한 Token 획득을 하도록 한다!
from django.db.models.signals import post_save

@receiver(post_save, sender=setting.AUTH_USER_MODEL)
def create_auth_token(sender, instance=None, created=False, **kwargs):
    if created:
        Token.objects.create(user=instance)
**post_save: DB에 뭔가가 저장된 직후에 특정 동작 수행 

생성한 Token의 획득:
 token을 획득을 할 수 있는 url path 지정
 -> 그 url에 대해 POST 요청을 보냄으로써 획득한다. 이는 obtain_auth_token으로 할 수 있다!

 2. 발급받은 Token을 API 요청에 담아 인증처리 


 글을 작성하거나, 이런 활동마다 발급받은 토큰을 보내려면 
 http 요청에서 Authorization: Token ~~~ 
 를 같이 보내주면 된다

 

 step by step

 pip install djangorestframework

```
# settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework'
]
```

앱에 rest_framework 추가

app 하나 만들기
python3 manage.py startapp mystorage

startapp안에 urls.py 파일 하나 만들기


```
#drfproj/urls.py

from django.contrib import admin
from django.urls import path, include
from mystorage import urls

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',include('mystorage.urls')),
]

``` 

새로운 앱의 urls.py와 연결

```
#mystorage/urls.py
from rest_framework.routers import DefaultRouter
from django.urls import path, include
from mystorage import views

router = DefaultRouter()
router.register('essay/', views.PostViewSet) 

urlpatterns=[
    path('', include(router.urls))
]
```

새로운 앱 urls.py에서도 연결해주기,
