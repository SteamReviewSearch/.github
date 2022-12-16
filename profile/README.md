<img src='https://github.com/SteamReviewSearch/.github/blob/main/image/SteamForYOU.jpg'>

## Project INFO
스팀 리뷰 검색 및 검색결과 기반 게임 추천

## Project Function
### 1. Elastic Search를 활용한 빠른 역색인 검색

- ngram + standard 애널라이저를 적용한 멀티 필드를 혼용하여 _score 계산, 게임 데이터를 검색.
- 선형, 이진트리로 데이터 전부를 스캔하는 SQL 인덱스와 `%LIKE%` 쿼리문 과 비교해 보다 빠르고 효율적인 검색 및 분석이 가능
- 동일한 환경(데이터 15만개)에서 검색 테스트시 SQL `%LIKE%`, 대비 약10000%(4~10s → 20~40ms), 풀텍스트 인덱스 대비 약 1000% 향상

### 2. Redis를 활용한 캐싱

- 서비스의 규모가 커짐에 따라 사용자 정보를 불러올 때 매번 DB에 접속하는 방식에서 성능적인 이슈 발생 가능성 ↑
- in-memory 형태의 No-SQL로써 Key-Value 쌍의 해쉬 맵 형태의 DB이기 때문에 disk나 rdbms에 비해 속도가 빠르다
- 메모리에 저장(캐싱)해두면 DB의 부하는 감소하고,  속도는 향상됨
- AWS Redis용 ElastiCashe는 단일노드와 여러개의 샤드가 지원되므로 확장 가능함, 실패한 노드를 자동으로 감지한 후 교체하여 인프라와 관련된 오버헤드를 줄이고 복원력이 좋은 시스템을 제공하여 DB오버로드 위험을 완화함.

### **3.유저들의 활동에 기반한 KNN알고리즘을 활용한 추천**

- 게임의 카테고리를 활용하여 유저의 게임 성향을 쌓아 저장
- 다른 유저와의 성향을 cosine similarity을 활용하여 분석
- KNN 알고리즘을 사용하여 일정 연관도를 가지고 있는 유저들이 본 게임을 바탕으로 추천
    - i의 연관도를 가진 유저 A의 게임 리스트와 j의 연관도를 가진 유저 B의 게임리스트가 있을때
        - i*[A_gameList]+j*[B_gameList]의 방식으로 리스트 생성하여 상위의 게임을 추천
- 지속적인 알고리즘 계산은 서버에 부담되기 때문에 DB에 저장하여 일정 시간이 지나지 않을 경우 DB의 정보를 꺼내서 추천, 아닐 경우 업데이트

## 기술 스택


Front: <img src="https://img.shields.io/badge/jQuery-0769AD?style=flat-square&logo=jQuery&logoColor=000000"/> <img src="https://img.shields.io/badge/Bootstrap-7952B3?style=flat-square&logo=Bootstrap&logoColor=000000"/>    

Framwork: <img src="https://img.shields.io/badge/Express-000000?style=flat-square&logo=Express&logoColor=999999"/>   

Back : <img src="https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=Node.js&logoColor=000000"/>   

DB : <img src="https://img.shields.io/badge/elastic cloud-005571?style=flat-square&logo=elastic cloud&logoColor=000000"/> <img src="https://img.shields.io/badge/Amazon RDS-527FFF?style=flat-square&logo=AMAZONRDS&logoColor=000000"/>     

Cashing: <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=REDIS&logoColor=000000"/> <img src="https://img.shields.io/badge/Amazon ElasticCash-005571?style=flat-square&logo=Amazon aws&logoColor=000000"/> 

Logging: <img src="https://img.shields.io/badge/LogStash-005571?style=flat-square&logo=LogStash&logoColor=000000"/> <img src="https://img.shields.io/badge/winston-00B8FC?style=flat-square&logo=express&logoColor=000000"/> 

Publish: <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=Git&logoColor=000000"/> <img src="https://img.shields.io/badge/Amazon EC2-FF9900?style=flat-square&logo=Amazon EC2&logoColor=000000"/>  

Data Collection: <img src="https://img.shields.io/badge/Axios-5A29E4?style=flat-square&logo=Axios&logoColor=000000"/> <img src="https://img.shields.io/badge/Lodash-3492FF?style=flat-square&logo=Lodash&logoColor=000000"/>   

## OnePage Notion
[<img src="https://img.shields.io/badge/Notion-F7A81B?style=flat-square&logo=Notion&logoColor=000000"/>](https://www.notion.so/Steam-For-U-44336c4a346f4faa925772a1d74b8473) << 링크

# GitHub
### search  
- Steam For U의 메인 기능
- [search README.md](https://github.com/SteamReviewSearch/search/blob/main/README.md)
### up-to-date 
- Steam For U의 신규 게임 데이터 수집 
- [up-to-date README.md](https://github.com/SteamReviewSearch/up-to-date/blob/dev/minjae/README.md)
### log_Life_Cycle 
- Steam For U의 로그 생명주기 
- [log_Life_Cycle README.md](https://github.com/SteamReviewSearch/log_Life_Cycle/blob/main/README.md)

# Member
|직책|이름|github|e-mail|역할|
|---|---|---|---|---|
|팀장|김재준|https://github.com/KJJDSA|게임 검색 및 리뷰 탐색, 게임 및 리뷰 데이터 관리, 프론트엔드 제작||
|팀원|김민재|https://github.com/minjjai|x.xreesespuffs@gmail.com|레디스, 최신화 서버, 로그스태시작업|
|팀원|최성영|https://github.com/cesdea|aprkvnem@gmail.com|추천 알고리즘, 로드밸런스, 로그인, 회원가입|
