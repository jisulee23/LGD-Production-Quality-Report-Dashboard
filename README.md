# LGD-Production-Quality-Report-Dashboard

# LG디스플레이 생산·품질 업무 보고서 대시보드

## 제목

**LG디스플레이 생산·품질 업무 보고서 및 3D 설비 모니터링 웹 서비스**

## 날짜

**09월 14일**

## 사용 라이브러리

| 라이브러리 / 기술      | 용도                                    |
| --------------- | ------------------------------------- |
| Python          | 웹 서버 실행 및 데이터 처리                      |
| Flask           | 생산·품질 데이터 조회 및 REST API 구현            |
| Werkzeug        | Flask 웹 서버 실행                         |
| HTML5           | 웹 페이지 구조 구성                           |
| CSS3            | 대시보드 UI 및 반응형 화면 구성                   |
| JavaScript      | 조회, 보고서 생성, 저장 등의 화면 기능 구현            |
| Three.js        | 패널 검사·이송 설비의 3D 모델링 및 시각화             |
| OrbitControls   | 마우스를 이용한 3D 화면 회전 및 확대/축소             |
| JSON            | 보고서 및 근거 데이터 저장                       |
| Cloudflared     | Google Colab에서 실행되는 웹 서버의 외부 접속 주소 생성 |
| IPython.display | Colab에서 웹 서비스 접속 링크 출력                |

## 설명

본 프로젝트는 **LG디스플레이 생산·품질 업무를 이해하기 위한 교육용 웹 서비스**입니다.

Google Colab 환경에서 Python과 Flask를 이용하여 웹 서버를 실행하고, HTML/CSS/JavaScript를 활용해 생산 및 품질 데이터를 조회할 수 있는 대시보드를 구현했습니다.

사용자는 날짜와 생산라인을 선택하여 생산량, 목표량, 생산 달성률, 검사 수량, 불량 수량, 불량률 등의 정보를 확인할 수 있습니다.

### 주요 기능

* 날짜별 생산·품질 데이터 조회
* 생산라인 A / B / 전체 조건 조회
* 생산량과 목표 생산량 비교
* 생산 달성률 자동 계산
* 검사 수량 및 불량 수량 조회
* 불량률 자동 계산
* LOT별 생산·품질 기록 확인
* 일자별 불량률 그래프 표시
* 설비 이상 및 알림 이력 확인
* Three.js 기반 패널 검사·이송 설비 3D 시각화
* 마우스를 이용한 3D 설비 회전 및 확대/축소
* 생산·품질 데이터를 기반으로 업무 보고서 초안 생성
* 생성된 보고서 수정 및 검토 상태 저장
* 보고서 TXT 파일 다운로드
* 보고서 근거 데이터 JSON 파일 다운로드
* Cloudflared를 이용한 외부 웹 접속

### 3D 설비

Three.js를 이용하여 디스플레이 패널의 검사 및 이송 과정을 표현했습니다.

3D 화면에는 다음 요소가 포함되어 있습니다.

* 패널 이송 롤러
* 디스플레이 패널
* 검사 헤드
* 검사 설비 프레임
* 반투명 보호 패널
* 작업자 모니터
* 설비 상태등
* 조명 및 그림자

OrbitControls를 적용하여 사용자가 마우스로 설비를 회전하거나 확대·축소하여 확인할 수 있도록 구현했습니다.

### 생산·품질 데이터 계산

생산 달성률은 다음과 같이 계산합니다.

```text
생산 달성률 = 실제 생산수량 ÷ 목표 생산수량 × 100
```

불량률은 다음과 같이 계산합니다.

```text
불량률 = 불량수량 ÷ 검사수량 × 100
```

검사수량이 0인 경우에는 잘못된 계산을 방지하기 위해 불량률을 별도로 표시하지 않습니다.

### 보고서 기능

조회한 생산·품질 데이터와 설비 사건 기록을 근거로 업무 보고서 초안을 생성할 수 있습니다.

생성된 보고서에는 다음 정보가 포함됩니다.

* 조회 기간
* 조회 생산라인
* 생산수량
* 목표수량
* 생산 달성률
* 검사수량
* 불량수량
* 불량률
* 조회된 LOT 개수
* 조회 기간 중 발생한 설비 사건
* 현재 모의 설비 상태
* 추가 확인이 필요한 사항

보고서는 사용자가 내용을 수정한 후 검토 여부와 함께 저장할 수 있으며 TXT 형식으로 다운로드할 수 있습니다.

또한 보고서 작성에 사용된 생산·품질 원본 근거는 JSON 형식으로 별도 다운로드할 수 있도록 구성했습니다.

## 실행 환경

본 프로젝트는 **Google Colab** 환경을 기준으로 제작했습니다.

Flask 서버를 Colab에서 실행한 후 Cloudflared Tunnel을 생성하여 외부 브라우저에서도 웹 서비스에 접속할 수 있도록 구성했습니다.

Cloudflared의 임시 주소를 사용하기 때문에 Colab 런타임을 다시 시작하거나 프로그램을 다시 실행하면 접속 주소가 변경될 수 있습니다.

## 프로젝트 목적

이 프로젝트의 목적은 실제 생산 시스템을 구축하는 것이 아니라 LG디스플레이의 생산·품질 업무 흐름을 웹 서비스 형태로 구현하면서 다음 내용을 학습하는 것입니다.

* 생산 데이터 조회 및 집계 과정 이해
* 생산 목표와 실적 비교
* 품질 및 불량률 계산
* 설비 알림 정보 확인
* 생산·품질 데이터 기반 보고서 작성
* Flask 기반 웹 서비스 구조 이해
* REST API와 Front-end 간 데이터 통신 이해
* Three.js를 활용한 3D 설비 시각화
* Cloudflared를 이용한 외부 웹 서비스 접속

> 본 프로젝트에서 사용되는 생산량, LOT, 불량 데이터 및 설비 상태는 학습을 위한 **교육용 가상 데이터**입니다.

## 참고 문헌

1. **Python 공식 문서**
   https://docs.python.org/3/

2. **Flask 공식 문서**
   https://flask.palletsprojects.com/

3. **Three.js 공식 문서**
   https://threejs.org/docs/

4. **Three.js OrbitControls 문서**
   https://threejs.org/docs/#examples/en/controls/OrbitControls

5. **Three.js GitHub Repository**
   https://github.com/mrdoob/three.js

6. **Cloudflare Tunnel 공식 문서**
   https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/

7. **Cloudflared GitHub Repository**
   https://github.com/cloudflare/cloudflared

8. **Google Colab**
   https://colab.research.google.com/

---

### Repository

`LGD-Production-Quality-Report-Dashboard`

### 프로젝트 구분

LG디스플레이 직무 이해 및 웹 개발 실습용 프로젝트
