<p align="center">
  <img src="resource/Hyndai.jpg" alt="Hyndai" height="280" />
</p>

# 🚘 블루핸즈 통합 검색 서비스 (Bluehands Finder)

사용자의 현재 위치 또는 선택한 지역을 기반으로 **현대자동차 블루핸즈(Bluehands)** 정비소를 조회하고, 원하는 정비 옵션(전기차, 수소차, 판금 등)별로 필터링하여 지도와 목록으로 보여주는 웹 애플리케이션입니다.

## ✨ 주요 기능

* **🗺️ 지도 시각화**: Folium 지도를 통해 지점의 위치를 마커로 표시하고, 클릭 시 상세 정보를 제공합니다.
* **🔍 상세 필터링**:
    * **지역 선택**: 시/도 단위로 검색 범위를 설정할 수 있습니다.
    * **서비스 옵션**: 전기차, 수소차, 판금, N-Line 전담 등 특수 정비 가능 여부로 필터링합니다.
* **📃 깔끔한 결과 목록**: 커스텀 HTML/CSS가 적용된 테이블과 페이지네이션 기능을 통해 검색 결과를 보기 쉽게 제공합니다.
* **📱 반응형 UI**: 사이드바를 활용하여 PC와 모바일 환경 모두에서 편리하게 사용할 수 있습니다.

## 🛠️ 기술 스택 (Tech Stack)

* **Python**: 3.10+
* **Web Framework**: [Streamlit](https://streamlit.io/)
* **Database**: MySQL (8.0+)
* **Libraries**:
    * `folium`, `streamlit-folium`: 지도 시각화
    * `mysql-connector-python`: DB 연동
    * `streamlit-js-eval`: GPS 위치 정보 수집
    * `pandas`: 데이터 처리

## ⚙️ 설치 및 실행 방법

### 1. 환경 설정 및 패키지 설치
```bash
# 필수 라이브러리 설치
pip install streamlit mysql-connector-python pandas folium streamlit-folium streamlit-js-eval
```

### 2. 데이터베이스 설정 (MySQL)
프로젝트 실행을 위해 MySQL에 데이터베이스와 테이블이 생성되어 있어야 합니다.
```sql
CREATE DATABASE IF NOT EXISTS bluehands_db;
USE bluehands_db;

-- 1. 지역 테이블
CREATE TABLE regions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL
);

-- 2. 블루핸즈 테이블
CREATE TABLE bluehands (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    address VARCHAR(255),
    phone VARCHAR(50),
    latitude DOUBLE,
    longitude DOUBLE,
    region_id INT,
    is_ev TINYINT(1) DEFAULT 0,        -- 전기차 전담
    is_hydrogen TINYINT(1) DEFAULT 0,  -- 수소차 전담
    is_frame TINYINT(1) DEFAULT 0,     -- 판금/차체
    is_cs_excellent TINYINT(1) DEFAULT 0, -- 우수 협력점
    is_n_line TINYINT(1) DEFAULT 0,    -- N-Line 전담
    FOREIGN KEY (region_id) REFERENCES regions(id)
);
```
### 3. DB 연결 정보 수정
.env파일을 생성한후 MySQL 환경에 맞게 수정해주세요.

### .env (또는 해당 파일의 생성 및 수정)
```env
    MYSQL_HOST=localhost
    MYSQL_PORT=3306
    MYSQL_USER=root                  # 본인의 MySQL 유저명
    MYSQL_PASSWORD="your_password"   # 본인의 MySQL 비밀번호
    MYSQL_DB=bluehands_db
```

### 4. 애플리케이션 실행
```
DB/crawler.py -> DB/schema.sql -> DB/import_csv_to_mysql.py
```
```terminal
streamlit run final.py # 최종 실행 파일은 final.py 입니다.
 ```

```📂 프로젝트 구조
📦 bluehands-finder
 ┣ 📜 final.py         # 메인 애플리케이션 소스 코드
 ┣ 📜 resource         # css,html,image 파일
 ┣ 📜 funtion          # 기능 구현
 ┗ 📜 README.md        # 프로젝트 설명서
```
---

# 실행 결과 

## 메인 화면 
![main](resource/main.png)
## 위치 확인 시그널
![location](resource/location.png)
## 사이드바 검색 기능
![research](resource/research.png)
## 검색결과는 하단부 테이블출력
![research_1](resource/research_1.png)

## 옵션 검색
<p align="center">
  <img src="resource/option.png" alt="option" />
</p>

## 해당되는 센터만 출력 
![option_search](resource/option_search.png)

## 지도 마커 클릭시 기록 저장
![clicked](resource/clicked.png)

## 🫱🏻팀원 회고

<table style="width: 100%; border-collapse: collapse; border: 1px solid #ddd; margin-bottom: 30px;">
    <thead>
        <tr style="background-color: #f8f9fa;">
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">작성자</th>
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">대상자</th>
            <th style="border: 1px solid #ddd; padding: 10px;">회고 내용</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="5" style="text-align: center; font-weight: bold; border: 1px solid #ddd;">전승권</td>
            <td style="text-align: center; border: 1px solid #ddd;">김용욱</td>
            <td style="border: 1px solid #ddd; padding: 10px;">발표 기반 PPT를 전담해서 준비해주셨습니다. 결과물을 전달 가능한 형태로 정리하는 역할은 프로젝트 마무리의 핵심인데, 그 부분을 책임지고 처리해줘서 발표 준비 부담이 크게 줄었습니다. “만들었다”에서 끝나지 않고 “설명할 수 있는 결과”로 완성시키는 데 기여했습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">김이선</td>
            <td style="border: 1px solid #ddd; padding: 10px;">검색 기능 구현을 하시며 DB의 구조를 확실히 파악 그리고 자신이 해야할것도 뛰어 넘어 더 하는 열정적인 모습을 보여주셨습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">위희찬</td>
            <td style="border: 1px solid #ddd; padding: 10px;">구조 설계 파트를 맡아 크롤링.py와 스키마, DB 테이블 기초 구축을 책임졌습니다. 기반틀이 빠르게 완성된 덕분에 후속 작업이 막히지 않고 진행됐습니다. 초반 설계를 제대로 잡아준 것이 전체 일정 안정화에 크게 기여했습니다. 그리고 코드 안정화에도 도움을 많이 주셨습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">이선호</td>
            <td style="border: 1px solid #ddd; padding: 10px;">처음부터 완벽하게 따라오기보다는, 부족한 부분을 인지하고 학습으로 메우려는 태도로 열정적으로 공부하면서 팀 흐름에 맞추려 노력해주셨습니다. 자신이 부족하다고 생각하지 않으셨으면 좋을거같습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전종혁</td>
            <td style="border: 1px solid #ddd; padding: 10px;">프로젝트 기여도가 압도적으로 높았습니다. 전체 개발의 90% 이상을 실질적으로 밀어붙였고, Streamlit 활용 능력도 상당했습니다. 코드를 작성하자마자 바로 실행하면서 코드 리뷰를 함께 진행하시고 속도와 열정 모두 팀을 끌어올린 핵심 요인이었습니다.</td>
        </tr>
    </tbody>
</table>

<table style="width: 100%; border-collapse: collapse; border: 1px solid #ddd; margin-bottom: 30px;">
    <thead>
        <tr style="background-color: #f8f9fa;">
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">작성자</th>
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">대상자</th>
            <th style="border: 1px solid #ddd; padding: 10px;">회고 내용</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="5" style="text-align: center; font-weight: bold; border: 1px solid #ddd;">김용욱</td>
            <td style="text-align: center; border: 1px solid #ddd;">전승권</td>
            <td style="border: 1px solid #ddd; padding: 10px;">개발과정이나 초기 설정 과정에서 서로 헷갈릴 수 있는 부분을 차분하게 세세하게 알려주면서 팀원이 이해를 하면서 진행해 나갈 수 있게 잘 도와주셨습니다. 그리고 제작 과정에서 나오는 기술적 이슈를 잘 정리해주셨고 프로젝트 내 진행방향을 어떻게 잡아가야할 지 잘 정해주셨습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">김이선</td>
            <td style="border: 1px solid #ddd; padding: 10px;">검색 기능과 누적 데이터 처리  등 프로젝트의 핵심 기능을 주도적으로 맡아주셨습니다. 프로젝트 기간 동안 직접 코드를 입력해보고 오류값을 잡아가면서 성장하시는 모습을 보여주셨고 그 외에도 추가하면 좋은 점에 대해 얘기해주면서 좋은 아이디어를 많이 제시해주면서 적극적인 모습을 보였습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">위희찬</td>
            <td style="border: 1px solid #ddd; padding: 10px;">초기 구조 설계와 크롤링 코드, DB 테이블 구축을 안정적으로 완성해 주셔서 프로젝트 기반을 단단히 잡아주셨습니다. 그 후에 조원들의 코드를 한 번 씩 봐주면서 잘못된 부분을 자세하게 잘 설명해주셔서 초기에 따라가기 힘들었던 부분도 점점 따라갈 수 있게 잘 도와주셨습니다. </td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">이선호</td>
            <td style="border: 1px solid #ddd; padding: 10px;">프로젝트 진행 과정에서 포기하지 않고 끝까지 따라오려는 노력과 성장이 인상적이었고, 제작 과정에서도 배움의 자세를 가지시면서 성장해 나가는 모습을 보여주셨고 이로부터 팀의 흐름을 따라오시려는 모습이 매우 인상에 남았습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전종혁</td>
            <td style="border: 1px solid #ddd; padding: 10px;">초반 데이터베이스 테이블 제작에서 초보들도 이해하기 편하게 좋은 예시를 보여주면서 진도를 맞춰나갈 수 있게 해주셨습니다. UI 제작에서도 많은 기여도를 보여주면서 완성도 높은 streamlit을 만들 수 있게 하면서 팀의 사기와 속도를 모두 복돋아주면서 팀의 화합을 더 이끌어주셨습니다.  </td>
        </tr>
    </tbody>
</table>

<table style="width: 100%; border-collapse: collapse; border: 1px solid #ddd; margin-bottom: 30px;">
    <thead>
        <tr style="background-color: #f8f9fa;">
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">작성자</th>
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">대상자</th>
            <th style="border: 1px solid #ddd; padding: 10px;">회고 내용</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="5" style="text-align: center; font-weight: bold; border: 1px solid #ddd;">김이선</td>
            <td style="text-align: center; border: 1px solid #ddd;">김용욱</td>
            <td style="border: 1px solid #ddd; padding: 10px;">개인 사정으로 하루 부재가 있었음에도 복귀 후 빠르게 프로젝트 흐름을 따라잡고, 발표 자료를 높은 완성도로 정리해 주셨습니다. 특히 결과물을 단순히 제작하는 데 그치지 않고, 발표용으로 전달 가능한 구조로 재정리한 점이 인상적이었습니다. 프로젝트 마무리 단계에서 PPT를 전담해 준비해 주신 덕분에 발표 준비 부담이 크게 줄었고, 팀 전체의 완성도를 끌어올리는 데 중요한 역할을 해주셨습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전승권</td>
            <td style="border: 1px solid #ddd; padding: 10px;">개발 과정에서 발생한 다양한 오류와 문제를 해결하는 데 중요한 역할을 해주셨습니다. 기술적 이슈를 차분하게 정리하고 방향을 바로잡아 주신 덕분에 프로젝트가 흔들리지 않고 안정적으로 마무리될 수 있었습니다. 팀의 중심을 잡아주는 역할을 수행해 주셨다고 생각합니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">위희찬</td>
            <td style="border: 1px solid #ddd; padding: 10px;">초기 구조 설계와 크롤링 코드, DB 테이블 구축을 안정적으로 완성해 주셔서 프로젝트 기반을 단단히 잡아주셨습니다. 또한 팀원들이 각자 작성한 코드를 하나의 시스템으로 통합하는 과정에서 중심적인 역할을 해주셨습니다. 서로 다른 코드 흐름을 정리하고 연결해 준 덕분에 프로젝트가 하나의 완성된 결과물로 정리될 수 있었습니다. 개발 중에도 방향성을 차분하게 잡아주셔서 팀이 흔들리지 않도록 도와주셨습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">이선호</td>
            <td style="border: 1px solid #ddd; padding: 10px;">자신의 현재 역량을 객관적으로 인식하고, 부족한 부분을 개인 학습으로 보완하려는 태도가 돋보였습니다. 프로젝트 진행 과정에서 포기하지 않고 끝까지 따라오려는 노력과 성장이 인상적이었으며, 이러한 태도는 팀 분위기에도 긍정적인 영향을 주었습니다. 완벽함보다 성장에 초점을 두고 끊임없이 배우려는 자세가 앞으로 더 큰 발전으로 이어질 것이라 생각합니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전종혁</td>
            <td style="border: 1px solid #ddd; padding: 10px;">프로젝트 전반을 주도적으로 이끌며 높은 기여도를 보여주셨습니다. 특히 Streamlit UI 전반을 설계하고 구현하며 사용자 흐름과 화면 완성도를 크게 끌어올렸습니다. 개발 과정에서 제가 해맬 때마다 방향을 제시해주시고 문제를 함께 해결해주셔서 큰 도움을 받았습니다. 실행력과 속도 면에서도 팀 분위기를 끌어올리는 핵심 역할을 해주셨습니다.</td>
        </tr>
    </tbody>
</table>

<table style="width: 100%; border-collapse: collapse; border: 1px solid #ddd; margin-bottom: 30px;">
    <thead>
        <tr style="background-color: #f8f9fa;">
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">작성자</th>
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">대상자</th>
            <th style="border: 1px solid #ddd; padding: 10px;">회고 내용</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="5" style="text-align: center; font-weight: bold; border: 1px solid #ddd;">위희찬</td>
            <td style="text-align: center; border: 1px solid #ddd;">김용욱</td>
            <td style="border: 1px solid #ddd; padding: 10px;">전제적으로 안뒤쳐지고 프로젝트 흐름을 이해하시고 프로젝트 내용의 핵심을 ppt에 잘녹아들게 정리해주셔서 신경써야 할부분이 많이 줄고 덕분에 완성도가 올라갔습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">김이선</td>
            <td style="border: 1px solid #ddd; padding: 10px;">검색 기능과 누적 데이터 처리, 그리고 파이썬 워드클라우드 구현 등 프로젝트의 핵심 기능을 주도적으로 맡아주셨습니다. 매일 남아서 추가적으로 작업하시는 모습도 있었고 ppt를 예쁘게 할줄아는 사람이 조에 없었는데 폰트도 다운받아 적용하는 등의 모습도 있었습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전승권</td>
            <td style="border: 1px solid #ddd; padding: 10px;">깃허브 관리와 코딩 과정에 문제가 있을때 함께 해결하였습니다, 프로젝트 후반부에 전체적인 폴더 정리와 보안적인 부분을 통틀어 리팩토링을 해주셨습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">이선호</td>
            <td style="border: 1px solid #ddd; padding: 10px;">프로젝트 진행 과정에서 포기하지 않고 끝까지 따라오려는 노력을 하며 성장하셨습니다, 제작 과정에서도 배움의 자세를 가지시면서 성장해 나가는 모습을 보여주셨고 이로부터 팀의 흐름을 따라오시려는 모습이 매우 인상에 남았습니다</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전종혁</td>
            <td style="border: 1px solid #ddd; padding: 10px;">저희 조의 주제를 정할떄 방향성을 제시해주셨고 노션정리와 README정리 등으로 후속작업이 편하게 만들어주셨습니다. 코딩 또한 대부분을 주작업이 시작되기 이전에 찾아서 해보시면서 막히는 부분이 없게 해주셨습니다. </td></td>
        </tr>
    </tbody>
</table>

<table style="width: 100%; border-collapse: collapse; border: 1px solid #ddd; margin-bottom: 30px;">
    <thead>
        <tr style="background-color: #f8f9fa;">
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">작성자</th>
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">대상자</th>
            <th style="border: 1px solid #ddd; padding: 10px;">회고 내용</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="5" style="text-align: center; font-weight: bold; border: 1px solid #ddd;">이선호</td>
            <td style="text-align: center; border: 1px solid #ddd;">김용욱</td>
            <td style="border: 1px solid #ddd; padding: 10px;">작성해주실곳</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">김이선</td>
            <td style="border: 1px solid #ddd; padding: 10px;">작성해주실곳</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">위희찬</td>
            <td style="border: 1px solid #ddd; padding: 10px;">작성해주실곳</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전승권</td>
            <td style="border: 1px solid #ddd; padding: 10px;">작성해주실곳</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전종혁</td>
            <td style="border: 1px solid #ddd; padding: 10px;">작성해주실곳</td>
        </tr>
    </tbody>
</table>

<table style="width: 100%; border-collapse: collapse; border: 1px solid #ddd; margin-bottom: 30px;">
    <thead>
        <tr style="background-color: #f8f9fa;">
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">작성자</th>
            <th style="width: 15%; border: 1px solid #ddd; padding: 10px;">대상자</th>
            <th style="border: 1px solid #ddd; padding: 10px;">회고 내용</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="5" style="text-align: center; font-weight: bold; border: 1px solid #ddd;">전종혁</td>
            <td style="text-align: center; border: 1px solid #ddd;">김용욱</td>
            <td style="border: 1px solid #ddd; padding: 10px;">개인 사정으로 하루 부재가 있어 진도를 맞추기 부담스러우셨을 텐데도, 복귀 후 흐름을 빠르게 파악하고 발표 자료를 훌륭하게 완성해 주셨습니다. 끝까지 책임감 있게 참여해 주셔서 감사합니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">김이선</td>
            <td style="border: 1px solid #ddd; padding: 10px;">검색 기능과 누적 데이터 처리, 그리고 파이썬 워드클라우드 구현 등 프로젝트의 핵심 기능을 주도적으로 맡아주셨습니다. 프로젝트 기간 동안 기술적으로 크게 성장하시는 모습이 매우 인상적이었습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">위희찬</td>
            <td style="border: 1px solid #ddd; padding: 10px;">마커 기능 구현과 UI/UX 등 시각적인 부분에서 큰 기여를 해주셨습니다. 특히 기획 단계에서 핵심 기능에 대한 다양한 아이디어를 적극적으로 제시해 주셔서 프로젝트의 방향성을 잡는 데 큰 도움이 되었습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">이선호</td>
            <td style="border: 1px solid #ddd; padding: 10px;">자신의 현재 역량을 객관적으로 파악하고, 부족한 부분은 개인 학습을 통해 채워나가려는 열정이 돋보였습니다. 포기하지 않고 끝까지 따라오며 성장하려는 태도가 팀 분위기에 긍정적인 영향을 주었습니다.</td>
        </tr>
        <tr>
            <td style="text-align: center; border: 1px solid #ddd;">전승권</td>
            <td style="border: 1px solid #ddd; padding: 10px;">개발 중 발생하는 크고 작은 오류들을 해결하는 데 중추적인 역할을 해주셨습니다. 팀이 잘못된 방향으로 가지 않도록 중심을 잡아주신 덕분에 프로젝트를 안정적으로 마무리할 수 있었습니다.</td>
        </tr>
    </tbody>
</table>
