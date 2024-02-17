# Data_Neonadeuri
# 1. 목적 & 배경

- 인공지능 기술을 활용한 디지털 신기술을 접목한 신규 비즈니스 모델 및 사회 문제해결 아이디어 제시
- 어린이 사고율은 매년 꾸준히 발생(5년간 60건)했다. 
사회의 이슈로 대두된 적도 많고 이를 해결하기 위해서 정부에서도 관련 지침을 내리는 등 관심이 쏠리고 있는 상황이다. 
이런 사회적 이슈를 해결하고 정부의 고민에 동참하기 위해서 “어린이 교통사고 예방 알리미”를 제안했다.

# 2. 주최 / 주관 & 팀원

- 주최 : 정보통신산업진흥원
- 주관 : 부산정보산업진흥원, 울산정보산업진흥원, 경남테크노파크, 한국정보통신진흥협회
- 팀원 : 이진, 정근오, 박시현

# 3. 프로젝트 기간

- 2023.03.03 ~ 2023.08.23 (약 6개월)

# 4. 프로젝트 소개

1. 개요
    
    스쿨존 근방에는 골목길, 보차혼용도로가 많다. 
    신호등이 없고 있는 교통사고 안전 예방 시설은 볼록거울이 대부분이다. 
    하지만 아직 도로의 흐름을 이해하지 못하는 어린이들에게 그리고 상대적으로 체구가 작아 주차된 차량에 가려진 어린이들에 대한 차량 사고는 기존 안전 시설에 효과를 많이 받지 못하고 꾸준한 사고율을 기록했다. 
    
    따라서 CCTV에서 수집한 영상 정보에서 어린이(사람)와 근처 차량(또는 오토바이, 전동킥보드 등)를 탐지하고 추적하는 알고리즘을 개발했다. 
    

1. 아이디어 구현
#### 움직이는 객체, 움직이지 않는 객체 구분
        
아이디어를 구현하기 위해서는 도로내 주차된 차량과 움직이는 차량을 구분해야 했다. 우선적으로 탐지와 추적하는 것이 필요했는데 이는 YOLOv8의 기본 기능으로 해결했다. 

그리고 YOLOv8이 탐지하고 추적한 객체마다. 경계 박스 위치, 객체의 종류, 추적 ID 정보를 얻을 수 있는데, 이 정보들을 활용해서 **객체의 종류별 박스의 변화들을 수집해 매 프레임 마다 평균을 계산했고 다음 프레임에서는 이전 프레임의 움직임 평균과 비교하는 방식**으로 정지한 객체(주차된 차량),  움직이는 객체(주행중인 차량)을 구분하는 알고리즘을 개발하고 적용했다.


<img width="226" alt="image" src="https://github.com/Data-Neonadeuri/Data_Neonadeuri/assets/113752645/b7095215-fbaf-4c7a-a29c-92a775be8f4a">
<img width="472" alt="image" src="https://github.com/Data-Neonadeuri/Data_Neonadeuri/assets/113752645/9780f6a5-51a6-4eee-b1fc-606a13948a8f">
      
#### 알림 규제
        
도로의 다양한 상황은 알고리즘의 신뢰성을 저하시킬 수 있다. 예를 들면 바람에 CCTV가 미세하게 흔들리더라도 객체를 인식하는 것이 달라지고 위에서 적용한 알고리즘이 정상적으로 작동하지 않는 경우이다.  따라서 다양한 환경에서도 경고 알림의 신뢰성을 높여 효과적인 사고예방을 위해 추가적인 알림 규제를 포함했다. 

 CCTV가 촬영하는 영상에서 **움직이는 객체가 특정 구간 내에 들어와야만 알림이 발생하도록 한 것**이다. 제한된 실험 환경으로 한정된 영상으로 실험을 진행했지만 기대했던 성능에 매우 가까워진 것을 확인했다.
 
<img width="478" alt="image" src="https://github.com/Data-Neonadeuri/Data_Neonadeuri/assets/113752645/2bad985b-2c2c-498c-87eb-3b8b22bcf28b">
        
#### 학교 위치 자동 인식
        
GPS의 위도, 경도 정보를 사용해서 자동으로 근방 학교를 인식하는 알고리즘을 개발, 적용했다.

<img width="471" alt="image" src="https://github.com/Data-Neonadeuri/Data_Neonadeuri/assets/113752645/174869c9-8124-4cc8-8fd2-375a3a1ea947">
  
#### 영상
   - https://youtu.be/Gpa8G2YvxPw?si=0OsVc0q-YxuWwC4_

결과  
    - 제 4회 ICT 비즈니스 모델 아이디어 경진대회 - 최우수상  
    - 2023년 울산광역시 공공데이터 활용 창업경진대회 '제품 및 서비스 부문' - 장려상  
    - 2023학년도 공공빅데이터와 AI 활용 실전 문제 해결 프로그램 - 우수상  
    - 특허 출원

