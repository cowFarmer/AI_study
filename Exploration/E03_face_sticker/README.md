# EXPLORATION
### 2022.01.11
3. 카메라 스티커앱 만들기 첫걸음

---

### 2022.01.11 log

다른 일정 소화하면서 크게 진행하지 못했음.

### 2022.01.16 log

```
ValueError: operands could not be broadcast together with shapes (130,130,3) (130,130,4) (130,130,3) 
```
~~LMS에서는 제대로 돌아가는데 주피터 노트북을 이용하면 오류 발생함 해결해야함~~

~~클라우드 환경에서 PATH 문제가 있는거 같음.   
정확한 이유는 모르겠지만 파일명 바꿔서 복붙했는데 해결됐음.~~   
image의 channel값이 다르게 되어 있어서 서로 합성할 때 오류가 생긴것인데,   
프로젝트 파일을 새로 만드니 해결되어서 넘어갔다. 왜 이런 오류가 발생했는지 모르겠다.   

### 2022.01.18 log

이미지를 90도 돌렸을때나 밝을때, 어두울때 각각 2장씩 총 5장을 추가해서 detector가 제대로 되는지 확인해봤다.   
파일 안에 회고도 추가했다.



### 회고

E-01 가위바위보 하면서 이미지 처리할 때 색상 변경하는 부분이 많이 어려웠는데,   
이번 EXP 진행하면서 궁금했던 이미지 관련 내용이 나와서 많은 도움이 됐다.   
특히 cv2로 이미지를 불러올때 RGB 형식이 아닌 BGR 형식으로 불러온다는점   
또한 image를 처리할때 당연히 백터처럼 좌측 하단이 0,0에서 시작되어 x,y값을 키우면   
커지는 방향으로 생각했지만 image는 좌측 상단이 0,0으로 시작했다.   
가장 이해하기 어려웠던것은 (x, y, c) 모양의 shape가 특정한 환경에서는   
(y, x, c) 모양으로 변경되었다. 이 부분은 LMS조 내부에서도 말이 나왔는데   
넘파이로 이미지를 관리할 때 (높이, 너비, 채널) = (y, x, c)이고   
pillow로 처리하면 (x, y, c)로 된다는 얘기이다.   
이 부분은 다르게 해석하는 분들이 많아서 document를 찾아봐도 이해가 잘 되지 않는다.   
CV관련은 관심이 많았던 부분이기도 하고 앞으로도 더 깊게 배우고 싶기도 하니   
이미지가 지속적으로 나열되는 동영상 처리 프로젝트까지 해보고 싶어졌다.
