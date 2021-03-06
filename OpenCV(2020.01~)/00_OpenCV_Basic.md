# 00_OpenCV_Basic

> 이하의 내용은 **『파이썬으로 만드는 OpenCV 프로젝트』(저자 이세우)**를 기반으로 한 것임을 밝힌다. 사용할 이미지 파일들은 작업파일이 있는 장소에 폴더로 저장해두는 것이 편리하다.
>
> - OpenCV 개요
>   - 영상처리와 컴퓨터 비전 처리를 위한 오픈소스 라이브러리
>   - `C`, ` C++`,  `Python` 에서 사용 가능
>   - `python`에서 `Numpy` 모듈을 이용하기 위해서는 `3.4`이상의 버전이 요구됨 
>   - `openCV`는  해당 `img`의 화소(`pixel`) 데이터를 출력
>   - 기본값은 `RGB`(Red, Green, Blue)가 아닌 `BGR` (Blue, Green, Red) 

```python
# openCV 설치 
!pip install opencv-python
!pip install opencv-contrib-python # extra 모듈 포함
```



## 1. 기본적인 입, 출력

### 1.1 `image` 입출력

```python
# openCV 불러오기
import cv2

# 새 창에 이미지 띄우기
img_file = 'img/motorbike.jpg' # 이미지 경로 입력
img = cv2.imread(img_file) # 파일로부터 이미지 읽어오기

cv2.imshow('IMG', img) # 특정 이미지를 IMG라는 이름의 윈도우 창에 출력
cv2.waitKey() # 지정 키를 누르고 창이 꺼지기까지의 대기시간 지정 
cv2.destroyAllWindows() # 화면의 모든 윈도우 창을 종료시킴

# 그레이스케일로 읽기
img_file = 'img/motorbike.jpg'
img = cv2.imread(img_file, cv2.IMREAD_GRAYSCALE)

cv2.imshow('IMG', img) 
cv2.waitKey()
cv2.destroyAllWindows()
```

![IMG](https://user-images.githubusercontent.com/58945760/72335263-09acc000-3702-11ea-8424-9ad76d314d8b.PNG)

![IMG2](https://user-images.githubusercontent.com/58945760/72335723-d0288480-3702-11ea-9b01-4657b897d747.PNG)

```python
# jupyter notebook에 바로 이미지 출력
import matplotlib.pyplot as plt
import cv2

img = cv2.imread('img/motorbike.jpg')

plt.axis('off') # x, y축의 숫자눈금을 표시하지 않음. default는 on
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.show()
```

```python
# 이미지 저장하기
import cv2

img_file = 'img/motorbike.jpg'
img = cv2.imread(img_file, cv2.IMREAD_GRAYSCALE)
cv2.imwrite('img/motorbike_gray.jpg', img)
```

```python
# 예제) 이미지를 흑백 새창으로 열고, 저장한 후 창 닫기
img_file = 'img/street.jpg'
img = cv2.imread(img_file, cv2.IMREAD_GRAYSCALE) # 그레이스케일로 열기
cv2.imshow('IMG_GRAYSCALE', img) # 새창 열기 

cv2.imwrite('img/street_grayscale.jpg', img) # street_grayscale로 다른 이름 저장
cv2.waitKey()
cv2.destroyAllWindows() # 아무 키나 누르면 창 종료
```



## 1.2 동영상 파일 읽기

> 동영상은 이미지 프레임의 모음이며 계속적인 재생이 필요하다는 점을 기억한다.
>
> - 기본적인 단어, 용어 설명
>   - `file_path`: 동영상 파일 경로
>   - `index`: 카메라 장치 번호(0부터 차례로 증가함)
>   - `cap`: `VideoCapture` 객체
>   - `ret`: 1. 초기화 여부=> `True` /`False `(isOpened)
>     2. 프레임 읽기 성공 혹은 실패 여부 => `True` /`False`(read)
>   - `img`: 프레임 이미지 => `numpy` 배열/`None`

```python
# 라이브러리 불러오기
import cv2

# 동영상 파일 불러오기 
video_file = 'img/big_buck/avi'
cap = cv2.VideoCapture(video_file)

if cap.isOpened():# 객체 초기화 
    while True: # 이미지 프레임을 계속해서 읽어올 수 있도록 함
        ret,img = cap.read()
        if ret:
            cv2.imshow(video_file, img)
            cv2.waitKey(25) # 얼마 후 다음 이미지 프레임을 재생할 것인지 지정(영상 재생속도 조절)
        else:
            break
else:
    print('동영상을 열 수 없습니다.')
    
cap.release()
cv2.destroyAllWindows()
```



### 1.3 그림그리기

> - 직선, 사각형, 원까지 원하는 도형을 화면에 그려본다. 

#### 1.3.1 직선그리기

> - `cv2.line(img, start, end, color, thickness, lineType)` 
>   - `img`: 그림을 그릴 이미지(`Numpy`배열)
>   - `start`: 선이 시작되는 지점의 좌표(x, y)
>   - `end`: 선이 끝나는 지점의 좌표(x, y)
>   - `color`: 선의 색깔(`BGR` 형식, 0~255)
>   - `thickness` : 선의 두께(`default` = 1)
>   - `lineType`: 선 타입

```python
# 라이브러리 불러오기
import cv2
import matplotlib.pyplot as plt
import numpy as np

# 그림 그릴 도화지 만들기
image = np.full((512, 512, 3), 255, np.uint8) # 배경 및 크기 설정 => 가로, 세로, 세 개의 채널, 색깔 넣기)
image = cv2.line(image, (0, 0), (255, 255), (0, 255, 0), 30, cv2.LINE_AA)

plt.imshow(image)
plt.show()
```

![graph](https://user-images.githubusercontent.com/58945760/72436650-45b85180-37e4-11ea-8330-7bce98e6e3d7.PNG)

#### 1.3.2 사각형 그리기

> - `cv2.rectangle(img, start, end, color, thickness, lineType)`
>   - `start`: 사각형 좌측 상단 꼭짓점(x, y)
>   - `end`: 사각형의 우측 하단 꼭짓점(x, y)
>   - `thickness`: 선 두께
>     - `-1`: 채우기

```python
# 예시 1
# 라이브러리 불러오기
import cv2
import matplotlib.pyplot as plt
import numpy as np

# 사각형 그릴 도화지 만들기
image = np.full((512, 512, 3), 255, np.uint8)
image = cv2.rectangle(image, (20, 20), (255, 255), (0, 0, 255), 10)

plt.imshow(image)
plt.show()

# 예시 2
img = cv2.imread('img/blank_500.jpg') # 흰 바탕 이미지 파일 불러오기
cv2.rectangle(img, (50, 50), (150, 150), (255, 0, 0), -1) # -1을 주면 사각형 안이 색으로 채워짐.

cv2.imshow('ractangle', img) # 'ractangle' 새 창으로 열기
cv2.waitKey()
cv2.destroyAllWindows()
```

![graph2](https://user-images.githubusercontent.com/58945760/72437095-5917ec80-37e5-11ea-8fe4-d32152894576.PNG)



#### 1.3.3 다각형 그리기

> - `cv2.polylines(img, isClosed, color, thickness, lineType)`
>   - `points`: 꼭짓점 좌표, `Numpy`배열 리스트
>   - `isClosed`: 닫힌 도형 여부(`True`/`False`)

```python
# 예시 1
# 라이브러리 불러오기
import cv2
import matplotlib.pyplot as plt
import numpy as 

image = np.full((512, 512, 3), 255, np.uint8) # 새 도화지 만들기
points = np.array([[5, 5], [128, 258], [483, 444], [400, 150]]) # 꼭짓점 좌표 지정
image = cv2.polylines(image, [points], True, (255, 0, 0), 4)

plt.imshow(image)
plt.show()


# 예시 2
img = cv2.imread('img/blank_500.jpg')

# 번개 모양 선 좌표
pts1 = np.array([[50, 50], [150, 150], [100, 140], [200, 240]], dtype=np.int32)
# 삼각형 모양 좌표 
pts2 = np.array([[350, 50], [250, 200], [450, 200]], dtype=np.int32)
# 오각형 모양 좌표
pts3 = np.array([[350, 250], [450, 350], [400, 450], [300, 450], [250, 350]], dtype=np.int32)

# 그리기 
cv2.polylines(img, [pts1], False, (255, 0, 0))
cv2.polylines(img, [pts2], False, (0, 0, 0), 10)
cv2.polylines(img, [pts3], True, (0, 0, 255), 10)
cv2.polylines(img, [pts4], True, (0, 0, 0))

# 새 윈도우 창으로 열기
cv2.imshow('polyline', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![graph3](https://user-images.githubusercontent.com/58945760/72437755-cbd59780-37e6-11ea-8ecf-9a9c4d4ed832.PNG)



#### 1.3.4 원 그리기

> - 원 그리는 함수 : `cv2.circle`(`img`, `center`, `radius`, `color`, `thickness`, `lineType`)
>   - `center`: 중심점 좌표(x, y)
>   - `radius`: 원의 반지름

```python
# 간단한 원 그리기

import cv2
import matplolib.pyplot as plt
import numpy as np

image = np.full((512, 512, 3), 255, np.uint8)
image = cv2.circle(image, (255, 255), 100, (0, 0, 0), -1)

plt.imshow(image)
plt.show()
```

![원](https://user-images.githubusercontent.com/58945760/72665640-ccbc3280-3a4d-11ea-82d4-ab230975dd68.PNG)

### 1.4 텍스트 출력하기

> - 새창에 텍스트를 그려주는 함수: `cv2.putText`(`img`, `text`, `position`, `font_type`, `font_scale`, `color`)
>   - `position`: 글자가 출력될 위치 좌표
>   - `scale`: 글씨 크기 가중치 

```python
import cv2
import matplotlib.pyplot as plt
import numpy as np

image = np.full((512, 512, 3), 255, np.uint8)
image = cv2.putText(image, 'What a beautiful day', (0, 200), cv2.FONT_ITALIC, 2, (255, 0, 0))

cv2.imshow('text', image)
cv2.waitKey()
cv2.destroyAllWindows()
```



### 1.5 창 조절하기

> - 창 이름 지정하는 함수: `cv2.nameWindow`(`title`, `option`)
>   - `option`: 창 옵션 지정
>     - `cv2.WINDOW_NORMAL`: 임의 크기의 창 열기. 창 크기 조정 가능
>     - `cv2.WINDOW_AUTOSIZE`:  이미지와 같은 크기의 창 열기. 창 크기 조정 불가능
>   - `cv2.moveWindow`(`title`, `x`좌표, `y`좌표) : 창 위치 이동
>   - `cv2.resizeWindow`(`title`, `width`, `height`): 창 크기 변경
>   - `cv2.destroyWindow`(`title`): 창 닫기
>   - `cv2.destroyAllWindows()`: 열린 모든 창 닫기

```python
import cv2

# 이미지 불러오기
img = cv2.imread('img/pistol.jpg')
img_gray = cv2.imread('img/pistol.jpg', cv2.IMREAD_GRAYSCALE)

# 창 이름 정하기
cv2.namedWindow('origin')
cv2.namedWindow('gray', cv2.WINDOW_NORMAL)
cv2.imshow('origin', img)
cv2.imshow('gray', img_gray)

# 창 위치 변경
cv2.moveWindow('origin', 0, 0)
cv2.moveWindow('gray', 100, 100)

# 창 크기 변환
cv2.waitKey() # 아무 키나 눌렀을 때
cv2.resizeWindow('origin', 200, 200)  
cv2.resizeWindow('gray', 400, 400)

cv2.waitKey()
cv2.destroyAllWindows()
```



### 1.6 키보드 입력으로 창 움직이기

> - 키보드의 `w`, `a`, `s`, `d` 키를 이용해 그림이 띄워진 윈도우 창이 상하좌우로 움직이도록 조정할 수 있다. 
>
> - `q`나 `Esc`를 누르면 종료되도록 설정한다.
>
>   
>
> - `cv2.waitkey(delay 시간)`: `0.001`초 단위로 숫자를 전달하면, 해당 시간동안 프로그램을 멈추고 대기, 키보드의 눌린 키에 대응하는 코드값을 정수로 반환
>
>   - 0: 무한대
>   - ex) `Esc`를 누를 경우 27 출력(`ASCII`코드)
>
> - `ord()`: 문자의 아스키코드 출력

```python
import cv2

img_file = 'img/mountain.jpg'
img = cv2.imread(img_file)
title = 'IMG' # 창 이름 지정
x, y = 100, 100 # 최초 좌표 표시

while True:
    cv2.imshow(title,img)
    cv2.moveshow(title, x, y)
    key = cv2.waitKey(0)
    
    if key == ord('a'): # 왼쪽 이동
        x -= 10
    elif key == ord('s'): # 위로 이동
        y += 10
    elif key == ord('w'): # 아래로 이동
        y -= 10
    elif key == ord('d') # 오른쪽으로 이동
    	x += 10
    elif key == ord('q') or key == 27 # 마우슨 오른쪽 버튼만 누르면 창이 종료된다. 
    	break
        
cv2. destroyAllWindows()        
```



### 1.7 사용자 마우스 입력 처리하기

> - `callback`함수를 활용하여 마우스 입력에 따른 결과들을 조정할 수 있다.  아래의 내용을 참조한다.
>   - `cv2.setMouseCallback`(`win_name`, `onMouse`, [, `param`]) : `win_name`함수에 `onMouse`함수 등록
>     - `win_name`: 이벤트 등록할 윈도우 이름
>     - `onMoouse`: 이벤트 처리를 위해 미리 선언해 놓는 콜백 함수
>     - `param` : 필요에 따라 onMouse 함수에 전달할 인자
>   - `MouseCallback`(`event`, `x`, `y`, `flags`, `param`): 콜백 함수 선언
>     - `event`: 마우스 이벤트 종류
>       - `cv2.EVENT_MOSEMOVE`: 마우스 움직임
>       - `cv2.EVENT_LBUTTONDOWN`: 왼쪽 버튼 누름
>       - `cv2.EVENT_RBUTTONDOWN`: 오른쪽 버튼 누름
>       - `cv2.EVENT_MBUTTONDOWN`: 가운데 버튼 누름
>       - `cv2.EVENT_LBUTTONUP`: 왼쪽 버튼 뗌
>       - `cv2.EVENT_RBUTTONUP`: 오른쪽 버튼 뗌
>       - `cv2.EVENT_MBUTTONUP`: 가운데 버튼 뗌
>       - `cv2.EVENT_LBUTTONDBLCLK`: 왼쪽 버튼 더블클릭
>       - `cv2.EVENT_RBUTTONDBLCLK`: 오른쪽 버튼 더블클릭
>       - `cv2.EVENT_MBUTTONDBLCLK`: 가운데 버튼 더블클릭
>       - `cv2.EVENT_MOUSEWHEEL`: 마우스 휠 스크롤
>     - `x`, `y`: 마우스 좌표
>     - `flags`: 마우스 동작과 함께 일어난 상태
>       - `cv2.EVENT_LBUTTONDOWN(1)`: 왼쪽 버튼 누름
>       - `cv2.EVENT_RBUTTONDOWN(2)`: 오른쪽 버튼 누름
>       - `cv2.EVENT_MBUTTONDOWN(4)`:  가운데 버튼 누름
>       - `cv2.EVENT_FLAG_CTRLKEY(8)`: `Ctrl` 키 누름
>       - `cv2.EVENT_FLAG_SHIFTKEY(16)`: `Shift`키 누름
>       - `cv2.EVENT_FLAG_ALTKEY(32)`: Alt 키 누름
>     - `param`: `cv2.setMouseCallback()` 함수에서 전달한 인자

#### 1.7.1 마우스로 동그라미 그리기

```python
import cv2

window = 'mouse event' # 창 이름 지정
img = cv2.imread('img/blank_500.jpg')
cv2.imshow(window, img)

def onMouse(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN: # 왼쪽 버튼을 누를 경우
        cv2.circle(img, (x, y), 50, (255, 0, 255), -1) 
        # 지름 50 크기의 핑크색 원을 해당 좌표에 표시
        cv2.imshow(window, img)
        
cv2.setMouseCallback(window, onMouse) 

while True:
    if cv2.waitKey(0):
        break
        
cv2.destroyAllWindows()
```

![원 그리기](https://user-images.githubusercontent.com/58945760/72789685-8b0ed000-3c77-11ea-8ff0-8d49b5eccddf.png)



#### 1.7.2 플래그를 이용한 `if`문으로 동그라미 그리기

> - `if`문을 사용해 조건을 지정할 경우, 복잡한 조건이 먼저 나와야 다음 조건에 영향을 주지 않는다.

```python
import cv2

title = 'mouse event' # 창 이름 지정
img = cv2.imread('img/blank_500.jpg') # 도화지가 될 백색 이미지 불러오기
cv2.imshow(title, img) # 백색 이미지 표시

colors = {'black': (0, 0, 0), # 색상 미리 지정해주기
         'red': (0, 0, 255),
         'blue': (255, 0, 0),
         'green': (0, 255, 0)}

def onMouse(event, x, y, flags, param):
    color = colors['black']
    if event == cv2.EVENT_LBUTTONDOWN: # 왼쪽 버튼을 누를 경우
        
        if flags & cv2.EVENT_FLAG_CTRLKEY and flags & cv2.EVENT_FLAG_SHIFTKEY:
            color = colors['green'] # ctrl 키와 Shift키를 동시에 누를 경우 녹색 원
            
        elif flags & cv2.EVENT_FLAG_CTRLKEY:
            color = colors['red'] # ctrl 키만 눌렀을 때는 빨간 원
            
        elif flags & cv2.EVENT_FLAG_SHIFTKEY:
            color = colors['blue'] # shift 키만 눌렀을 때는 파란 원
            
        cv2.circle(img, (x,y), 50, color, -1) # 원 그리기
        cv2.imshow(title, img)
        
cv2.setMouseCallback(title, onMouse)

while True:
    if cv2.waitKey(0):
        break

cv2.destroyAllWindows()        
```

- 그냥 클릭할 때

![1](https://user-images.githubusercontent.com/58945760/72796613-fdd17880-3c82-11ea-865b-bfcc1cbffeb0.PNG)



- `ctrl`키 & `shift`키 누른 상태에서 클릭

![2](https://user-images.githubusercontent.com/58945760/72796617-ff02a580-3c82-11ea-981c-0ec529fe66d4.PNG)

- `ctrl`키만 누른 상태에서 클릭

![3](https://user-images.githubusercontent.com/58945760/72796621-00cc6900-3c83-11ea-848f-91e7afe244a7.PNG)

- `shift`키만 누른 상태에서 클릭

![4](https://user-images.githubusercontent.com/58945760/72796626-01fd9600-3c83-11ea-98d8-e3c0a5dcad76.PNG)



#### 1.7.3 콜백함수 이용하여 이미지 자르기

> - 모든 image 원점 좌표 `(0, 0)`는 일반 좌표처럼 좌측 하단이 아닌 좌측 상단에 위치한다는 점을 기억할 것.
>
> ![tempsnip](https://user-images.githubusercontent.com/58945760/72795160-7e42aa00-3c80-11ea-9613-5304a6139918.png)

```python
import cv2
import numpy as np

image = cv2.imread('img/lion_face.jpg') # 이미지 불러오기
image_to_show = np.copy(image) 

mouse_pressed = False
s_x = s_y = e_x = e_y = -1

def mouse_callback(event, x, y, flags, param): # 함수 선언
    global image_to_show, s_x, s_y, e_x, e_y, mouse_pressed
    
    if event == cv2.EVENT_LBUTTONDOWN:# 마우스 왼쪽 버튼 클릭할 때
        mouse_pressed = True # 클릭 O
        s_x, s_y = x, y # 시작 좌표 설정
        image_to_show = np.copy(image)
        
    elif event == cv2.EVENT_MOUSEMOVE: # 마우스를 움직일 때
        if mouse_pressed:
            image_to_show = np.copy(image)
            cv2.rectangle(image_to_show, (s_x, s_y),
                         (x, y), (0, 255, 0), 1) # 지정한 부분에 초록색 사각형 그려주기
            
    elif event == cv2.EVENT_LBUTTONUP: # 마우스 왼쪽 버튼에서 손을 뗄 때
    	mouse_pressed = False # 클릭 X
        e_x, e_y = x, y # 끝 좌표 설정
        
cv2.namedWindow('image') # 창 이름 설정
cv2.setMouseCallback('image', mouse_callback) # 이미지에 마우스 콜백 함수 적용 

while True:
    cv2.imshow('image', image_to_show) 
    k = cv2.waitKey(1) 
    
    if k == ord('c'): # 'c' 버튼을 누르면
        if s_y > e_y: # 시작 지점의 y좌표가 끝 지점의 y좌표보다 클 때 
            s_y, e_y = e_y, s_y # 두 좌표의 위치 바꿈
        if s_x > e_x: # 시작 지점의 x좌표가 끝 지점의 x좌표보다 클 때
            s_x, e_x = e_x, s_x # 두 좌표의 위치 바꿈
            
        if e_y - s_y > 1 and e_x - s_x > 0: 
            # 끝 지점의 y좌표에서 시작 지점의 y좌표를 뺀 값이 1보다 크고, 
            # 끝 지점의 x좌표에서 시작 지점의 x좌표를 뺀 값이 0보다 클 때
            image = image[s_y:e_y, s_x:e_x] # 지정한 부분의 이미지만 뽑아내기
            image_to_show = np.copy(image)
            
        elif k == 27: # Esc를 누르면
            break
            
cv2.destroyAllWindows() # 모든 창 종료
```

- 마우스로 영역 지정 

![영역 지정](https://user-images.githubusercontent.com/58945760/72793246-9107af80-3c7d-11ea-94a2-3a68fa74222e.png)



- 지정한 부분 잘라내기

![자름](https://user-images.githubusercontent.com/58945760/72793250-936a0980-3c7d-11ea-8fcd-7d92ebe2e9d5.PNG)



### 1.8 트랙바를 이용한 이미지 색 조정

> - `cv2.createTrackbar`(`trackbar_name`, `win_name`, `value`, `count`, `onChange`) : 트랙바 생성 함수
>   - `trackbar_name`: 트랙바 이름 지정
>   - `win_name`: 트랙바가 있는 창 이름 
>   - `value`: 트랙바의 시작 지점 값(`0`~ `count` 사이)
>   - `count`: 트랙바 눈금의 갯수, 트랙바가 표시할 수 있는 최댓값
>   - `onChange`: `TrackbarCallback`, 트랙바 이벤트를 조정하는 함수
> - `TrackbarCallback`(`value`): 트랙바 이벤트 콜백 함수
>   - `value`: 트랙바가 움직인 새 위치 값
> - `pos` = `cv2.getTrackbarPos`(`trackbar_name`, `win_name`)
>   - `trackbar_name`: 찾고자 하는 트랙바 이름
>   - `pos`: 트랙바 위치 값

```python
win_name = "Trackbar_train"

img = cv2.imread('img/blank_500.jpg')
cv2.imshow(win_name, img)

def onChange(x):
    
    r = cv2.getTrackbarPos('R', win_name)
    g = cv2.getTrackbarPos('G', win_name)
    b = cv2.getTrackbarPos('B', win_name)
    
while True:
    if cv2.waitKey(1) == 27:
        break
        
cv2.destroyAllWindows()
```

![트랙바](https://user-images.githubusercontent.com/58945760/72796248-581e0980-3c82-11ea-95b6-59bc01cbeff1.PNG)