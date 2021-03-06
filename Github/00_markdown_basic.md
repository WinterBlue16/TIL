# 마크다운(Markdown)

> 일반 텍스트 형식 구문을 사용하는 마크업 언어의 일종으로 사용법이 쉽고 간결하여 빠르게 문서 정리를 할 수 있습니다. 단, 모든 HTML 마크업을 대체하지는 않습니다.



## 1. 문법

### 1.1 Header

> 헤더는 제목을 표현할 때 사용합니다. 단순히 글자의 크기를 표현하는 것이 아닌 의미론적인 중요도를 나타냅니다. 

- `<h1>`부터 `<h6>`까지 표현 가능합니다. 
- `#`의 개수로 표현하거나 `<h1></h1>`의 형태로 표현 가능합니다. 



# h1 태그입니다.

## h2 태그입니다.

### h3 태그입니다.

#### h4 태그입니다.

##### h5 태그입니다.

###### h6 태그입니다.



### 1.2 List

> 목록을 나열할 때 사용합니다. 순서가 필요한 항목과 그렇지 않은 항목으로 구분할 수 있습니다. 순서가 있는 항목 아래 순서가 없는 항목을 지정할 수 있으며 그 반대도 가능합니다. 

- 순서가 없는 목록
  * `1.`을 누르고 스페이스바를 누르면 생성할 수 있습니다.
  * `tab`키를 눌러서 하위 항목을 생성할 수 있고 `shift + tab` 키를 눌러서 상위 항목으로 이동할 수 있습니다. 

- 순서가 있는 목록
  * `-`(하이픈)을 쓰고 스페이스바를 누르면 생성할 수 있습니다.
  * `tab` 키를 눌러서 하위 항목을 생성할 수 있고 `shift + tab` 키를 눌러서 상위 항목으로 이동할 수 있습니다.



1. 순서가 있는 항목
2. 순서가 있는 항목
   	1. 순서가 있는 하위 항목
    	2. 순서가 있는 하위 항목



- 순서가 없는 항목
- 순서가 없는 항목
  - 순서가 없는 하위 항목
  - 순서가 없는 하위 항목



### 1. 3 Code Block 

> 코드 블럭은 작성한 코드를 정리하거나 강조하고 싶은 부분을 나타낼 때 사용합니다. 인라인과 블럭 단위로 구분할 수 있습니다.

- Inline
  - 인라인 블럭으로 처리하고 싶은 부분을 `(백틱)으로 감싸줍니다.

- Block 
  - 백틱을 3번 입력하고  `Enter`를 눌러 생성합니다. 



`add` 한 요소를 remote 저장소에 올리려면 `$ git push origin master`를 터미널에 입력합니다.

```shell
$ git add .
$ git commit -m "first commit"
$ git push origin master

```



### 1.4 Image

> 로컬에 있는 이미지를 삽입하거나 이미지 링크를 활용하여 이미지를 나타낼 때 사용합니다.

- `![]()`을 작성하고 `()`안에 이미지 주소를 입력합니다. `[]`안에는 이미지 파일의 이름을 작성합니다.
- 로컬에 이미 파일을 저장한 경우 절대 경로가 아닌 상대 경로를 사용하여 이미지를 저장합니다. 



![](https://i.gzn.jp/img/2015/04/07/10-years-git-linus-torvalds/00-top.png)            <img src="http://pngimg.com/uploads/github/github_PNG20.png" style="zoom:20%;" />


 - `width`를 이용하여 업로드한 이미지의 크기를 `resize`할 수 있다. 
   - 100%
     <img src="http://pngimg.com/uploads/github/github_PNG20.png" width="100%">
   
   - 50%
     <img src="http://pngimg.com/uploads/github/github_PNG20.png" width="50%">
   
   - 25% 
     <img src="http://pngimg.com/uploads/github/github_PNG20.png" width="25%">
   
   
   
 - html에서의 `p`/`center` 태그로 이미지를 가운데 정렬할 수 있다. 
   - 가운데 정렬 적용 전
   <img src="http://pngimg.com/uploads/github/github_PNG20.png" width="25%">
   
   - 가운데 정렬 적용 후
   <p align="center"><img src="http://pngimg.com/uploads/github/github_PNG20.png" width="25%"></p>


### 1.5 Link

> 특정 주소로 링크를 걸 때 사용합니다.

- `[]()`을 작성하고 `()`안에 링크 주소를 작성하고 `[]`안에 어떤 링크 주소인지 작성합니다.



[git 공식문서](https://git-scm.com/)

[github 공식문서](https://github.com/)



### 1.6 Table

> 표를 작성하여 요소를 구분할 수 있습니다.

- 한 셀을 만들 때마다 `|`(파이프) 사이에 컬럼을 작성하고 줄을 바꿀 때마다 `Enter`를 입력합니다.
- 마지막 컬럼을 작성하고 뒤에 `|`를 붙여줍니다.
- 일단 표를 작성하고 나면 버튼으로 앞뒤에 열, 행을 추가하는 것이 가능합니다.



| working directory | stating area | remoe repo |
| ----------------- | ------------ | ---------- |
| working tree      | index        | history    |
| working copy      | cache        | tree       |

- 입력 방법으로 각 열을 왼쪽/가운데/오른쪽 정렬로 지정할 수 있습니다. 

| working directory | stating area | remoe repo |
| :----------------- | :------------: | ----------: |
| working tree      | index        | history    |
| working copy      | cache        | tree       |

- 셀 안에서 값을 볼드 처리하거나 색을 바꾸는 것도 가능합니다.
  - 볼드체(진하게)<br>

| working directory | stating area | remoe repo |
| ----------------- | ------------ | ---------- |
| **working tree**      | index        | **history** |
| working copy      | **cache**        | tree       |

   - 이탤릭체<br> 

| working directory | stating area | remoe repo |
| ----------------- | ------------ | ---------- |
| _working tree_      | index        | _history_ |
| working copy      | _cache_        | tree       |

- 마크다운 문법에서는 <span> 태그를 활용해 글자색을 변경하는 것도 가능하다고 알려져 있으나([설명 참고](https://inasie.github.io/it%EC%9D%BC%EB%B0%98/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4-%ED%91%9C-%EB%A7%8C%EB%93%A4%EA%B8%B0/)), Github에서는 글자색 변경이 적용되지 않습니다. 예로 로컬에서 마크다운 문서의 글자색이 변한 것을 확인할 수 있어도, Github 페이지에서 열어봤을 때는 검은색 글자 그대로 출력됩니다. 



### 1.7 수식 

> 함수나 집합, 공식 등을 입력해야 할 때 사용한다.

수식은 메뉴 바에서 본문 > 수식블록을 클릭하여 손쉽게 입력할 수 있습니다. 수식 블록 활용 시 [튜토리얼 1](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference), [튜토리얼 2](https://dev-lagom.tistory.com/35), [튜토리얼3](https://ko.wikipedia.org/wiki/%EC%9C%84%ED%82%A4%EB%B0%B1%EA%B3%BC:TeX_%EB%AC%B8%EB%B2%95)을 참고해 입력합니다. 수식 블록을 통해 입력한 수식은 기본적으로 가운데 정렬이며, 한 줄을 차지합니다. 따라서 문장 사이에 수식을 넣는 것은 typora에서는 불가능합니다. 아래는 수식 블록을 통해 입력한 수식의 예시입니다.
$$
y=ax+b \\
y=ax^2+bx+c
$$
 띄어쓰기는 \, 줄바꿈은 \ 연속 두 개로 할 수 있습니다. 문법은 기본적으로 TeX_문법에 따릅니다.



### 1.8 기타

**특수문자 입력**

> 아래의 표를 참고하여 입력

<img src="https://user-images.githubusercontent.com/58945760/111019049-1610d380-8400-11eb-912c-de40f56f5854.png" alt="FireShot Capture 168 - 마크다운 문서에서 특수문사 사용하기 (How to use symbolic character in markdown)_ - 4urdev tistory com" style="zoom:80%;" />



**인용문**

- `>`를 입력하고 `Enter`키를 누릅니다.

> git은 컴퓨터 파일의 변경사항을 추적하고 여러 명의 사용자들 간에 해당 파일들의 작업을 조율하기 위한 분산 버전 관리 시스템이다.

- 인용문 안에 인용문을 작성하면 중첩해서 사용할 수 있습니다.

> $ git add .
>
> > $ git commit -m "first commit"
> >
> > > $ git push origin master



**수평선**

- `---`, `***`, `___`을 입력하여 작성합니다.

Working Directory

---

Staging Area

***

Remote Repository

___



**강조**

- 이탤릭체는 해당 부분을 `*` 혹은 `_`(언더바)로 감싸줍니다.
- 보드체는 해당 부분을 `**`혹은`__`(언더바 2개) 로 감싸줍니다.
- 취소선은 `~~` (물결)로 감싸줍니다.

이것은 *이탤릭체*입니다.

이것은 **보드체**입니다.

이것은 ~~취소선~~입니다.



**줄바꾸기와 문단 바꾸기**

- `Spacebar`를 두 번 누르면 줄을 바꿀 수 있습니다.
- `Enter`를 두 번 하는 것으로 단락을 바꿀 수 있습니다.



**줄 공백 주기**

- `<br>`태그를 활용하여 줄간격을 제어할 수 있습니다.



※ 참고 사이트

마크다운 특수문자 표 인용 : https://4urdev.tistory.com/62, https://ascii.cl/htmlcodes.htm

