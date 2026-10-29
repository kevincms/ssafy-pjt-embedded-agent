# 보드·모듈 후보 비교 (20만원 기준)

> - 작성일: 2026-10-28 · 수정일: 2026-10-29 (보유한 STM32 NUCLEO-F103RB 반영 · 후보 표에 삼성·세메스 연관 요약 추가 · 상세는 별첨)
> - 기준 자료: 팀 조사 문서 `SSAFY_관통PJT_삼성계열_임베디드_채용요건_보드후보_20261028.md`
> - 전제: STM32 NUCLEO-F103RB(보유) + 추가 장비 1종 + Jetson Nano 4GB + 서버 LLM. STM32는 후보 선택에서 제외한다.

## 읽는 법

- 20만원은 **후보 본체 가격** 기준이다. 전원·케이블·배송비·관세·부가세는 빠져 있다.
- 달러 가격은 1달러 = 1,327.75원(ECB 기준, 2026-10-27)으로 환산했다.
- Waveshare 가격은 2026-10-28에 공식몰에서 다시 확인했다. 재고는 확인하지 않았다.
- LS·Advantech·Beckhoff 가격은 조사 문서 값을 그대로 옮겼다(다시 확인하지 않음).
- 국내 판매처 가격은 공식몰과 다를 수 있다. 구매 전에 다시 확인한다.
- 후보 기호 A~G는 조사 문서와 같다. H는 조사 문서에 없는 추가 후보다.
- 표의 **연관** 줄은 삼성·세메스 직무와의 연관을 한 줄로 요약한 것이다. 근거와 주의는 별첨 A·B에 있다.
- 연관 줄의 근거 표시
  - **[직무소개]** 상시 공개된 공식 직무 설명 (합격 조건 아님)
  - **[신입]** 해당 회차 신입 공고
  - **[경력]** 경력직 공고 (신입 요건 아님)
  - **[추론]** 공식 근거에 직접 나오지 않고 조사 문서가 유추한 것

## 공통 구성 (후보와 별개)

| 항목 | 본체 가격 | 비고 | 삼성·세메스 연관 |
|---|---|---|---|
| STM32 NUCLEO-F103RB | 보유 | bxCAN(CAN 2.0B) 내장(트랜시버 별도) | 세메스 Embedded SW·펌웨어 [직무소개]<br>삼성전자 DX 시스템 SW(드라이버·펌웨어) [신입] |
| Waveshare USB TO RS485 | $10.99 (약 1.5만원) | Jetson과 RS485 장비(A·B·C·E)를 잇는 어댑터. 국번이 다르면 한 버스에 여러 장비를 연결할 수 있음 | — |
| Jetson Nano 4GB | 사용 예정 | JetPack 4.x(최대 4.6.x) · Ubuntu 18.04 · 기본 Python 3.6 (4절 참고) | 세메스 Application SW(AI·설비 데이터 분석) [직무소개]<br>삼성전자 DS 설비 진단 Agent·Edge/Cloud [경력] |

## 1. 20만원 아래

| 후보 | 본체 가격 | 함께 필요한 것 | 장점 | 단점 | 맞는 방향 · 연관 |
|---|---|---|---|---|---|
| **B. Waveshare Modbus RTU IO 8CH**<br>8 DI / 8 DO · RS485 | $23.99<br>(약 3.2만원) | USB-RS485<br>DC 7~36V 전원 | 가장 싸고 첫 성공이 빠름<br>RS485·Modbus RTU를 직접 다룸<br>무응답·국번 오류 같은 에러를 일부러 만들기 쉬움 | 장치 안에 시퀀스 로직이 없어 Jetson이나 STM32가 제어를 맡아야 함<br>출력이 오픈드레인(sinking)이라 릴레이 접점처럼 쓰면 안 됨 | **방향:** 적은 예산 · 산업 통신 입문 · 공통 Tool API 시연<br>**연관:** 세메스 장비 통신(Field bus·H/W Interface) [직무소개·경력]. 고속 Field bus는 아님 |
| **C. Waveshare Modbus RTU Analog Input 8CH**<br>8채널 12비트 · RS485 | $24.99<br>(약 3.3만원) | USB-RS485(B와 같은 버스 사용 가능)<br>DC 7~36V 전원<br>4–20mA 신호원 또는 트랜스미터 | 4–20mA·0–10V 계측값으로 센서 단선·범위 초과·드리프트를 진단할 수 있음<br>Edge AI 이상 탐지에 쓸 데이터를 얻음 | 입력 전용이라 출력 제어가 없음<br>신호원이 따로 필요함(가변저항은 전류 루프를 대신하지 못함)<br>정확도·샘플링 속도는 공식 자료로 확인해야 함 | **방향:** B와 묶어 설비 I/O 구성 · 데이터 진단 중심<br>**연관:** 세메스 설비 데이터 분석·예지 진단 [직무소개·경력] · 삼성SDI 검사 설비 SW [직무소개] |
| **D. Waveshare Modbus PoE ETH IO 8CH**<br>8 DI / 8 DO · Ethernet | $39.99<br>(약 5.3만원) | PoE 인젝터·스위치 또는 별도 전원<br>LAN 케이블 | Modbus TCP와 RTU를 모두 지원<br>IP로 여러 장비를 원격 진단하기 쉬움<br>RS485 배선 문제가 줄어듦 | RS485 물리계층을 배울 기회가 줄어듦<br>PoE 장비나 전원을 따로 준비해야 함 | **방향:** Agent·네트워크·복수 장비 진단 중심<br>**연관:** 세메스 설비제어 SW Platform [직무소개] · 삼성전자 DS 설비 제어 공통 플랫폼 [경력]. 고속 Field bus는 아님 |
| **H. CAN 실험 세트 (추가 후보)**<br>Waveshare USB-CAN-A + SN65HVD230 CAN Board | $23.98<br>(약 3.2만원)<br>= $18.99 + $4.99 | NUCLEO-F103RB(보유)<br>120Ω 종단저항(모듈 내장 여부 확인)·배선 | 보유한 NUCLEO-F103RB의 bxCAN을 트랜시버로 바로 버스에 연결<br>처음 아이디어의 CAN 축을 유지 | Jetson Nano에는 CAN 컨트롤러가 없어 USB-CAN이 꼭 필요함<br>USB-CAN-A 제품 페이지는 Jetson Nano(Ubuntu) 지원만 적고 SocketCAN 지원은 적지 않음 → 실측 필요 | **방향:** 차량·배터리 임베디드 · STM32 펌웨어 중심<br>**연관:** 삼성SDI 배터리·BMS SW [직무소개, CAN 연결은 추론] · 삼성전기 IT/전장 Embedded SW [경력]. 세메스 설비 제어와는 거리가 있음 |

## 2. 20만원 위

| 후보 | 본체 가격 | 함께 필요한 것 | 장점 | 단점 | 맞는 방향 · 연관 |
|---|---|---|---|---|---|
| **A. LS ELECTRIC XGB PLC XBM-DN16S** | 208,500원<br>(조사 문서 · 디바이스마트 목록) | 24V DC 전원<br>배선·퓨즈·단자대<br>스위치·LED/릴레이<br>필요 시 프로그래밍 케이블·RS485 컨버터 | MCU와 산업 제어기의 역할 차이가 분명함<br>시퀀스·알람·인터록을 배움 | 본체만으로 예산 초과<br>래더·XG5000·통신 설정에 학습 시간이 듦<br>RS485 포트가 있어도 Modbus 설정이 바로 되는 것은 아님 | **방향:** 산업 제어 중심(조사 문서 조합 1)<br>**연관:** 세메스 설비 구동부 Sequence Programming [경력] · 삼성전기 PC/PLC 제어 설계 우대 [경력]. 둘 다 신입 요건은 아님 |
| **E. Advantech ADAM-4055**<br>8 DI / 8 DO · RS485 Modbus RTU/ASCII | 약 21만원대<br>(조사 문서 · 출처 번호 없음) | DC 10–30V 전원<br>USB-RS485 | 절연·워치독을 갖춘 전문 산업용 장비<br>제품 매뉴얼을 기반으로 진단 시나리오를 짤 수 있음 | 기본 기능이 B와 겹치는데 본체 가격은 훨씬 높음 | **방향:** 예산이 넉넉할 때 B 대신<br>**연관:** B와 같음. 세메스 장비 통신 [직무소개·경력] |
| **F. Beckhoff EK1100 + EL1008 + EL2008**<br>EtherCAT 커플러 + DI/DO 단자 | $205.36 이상<br>(약 27.3만원 이상)<br>= EK1100 $148.65 + EL2008 $56.71<br>EL1008 미포함(조사 문서 · TME) | EL1008·엔드 터미널<br>24V 전원<br>EtherCAT 마스터 SW | 실시간 산업 Field bus(EtherCAT)를 직접 다룸<br>모듈형 단자라 I/O를 늘리기 쉬움 | 가격이 나온 후보 중 가장 비싸고 구성이 복잡함<br>학습 난도가 높음<br>Jetson Nano 구형 OS에서 마스터 SW 호환 위험 | **방향:** 1차 MVP 뒤 확장·도전 과제<br>**연관:** 세메스 고속 Network Protocol(Field bus)·실시간 제어 [직무소개]. 세메스 페이지에 EtherCAT이라는 이름은 없음 |

## 3. 가격 미정 (견적 뒤 분류)

| 후보 | 본체 가격 | 구성 | 장점 | 단점 | 맞는 방향 · 연관 |
|---|---|---|---|---|---|
| **G. 스테퍼 모션 세트** | 구성별 견적 필요 | NEMA17 스테퍼·드라이버·저전압 전원·리니어 슬라이드·홈/리미트 스위치<br>가능하면 엔코더 | 웨이퍼 반송·정밀 제어를 교육용 모형으로 보여 줌<br>반복성·홈 복귀 성공률 같은 정량 지표를 얻음 | 기구 제작·드라이버 정격·기계적 위험 관리가 필요함<br>스테퍼는 명령한 스텝 수가 실제 위치와 같다고 보장하지 않음 | **방향:** A 또는 B에 붙이는 확장<br>**연관:** 세메스 Motion 제어·구동부 Sequence [직무소개·경력] · 삼성전기 고정밀 모션 제어 [경력]. 초정밀을 말하려면 위치 피드백이 필요 |

## 4. Jetson Nano 공통 주의

- 기본 Python이 3.6이다. PyPI 기준으로 `pymodbus` 3.x는 Python 3.8 이상이 필요하고(최신 3.16.1은 3.10 이상), 3.6에서는 2.5.3까지만 설치된다. 2.5.3은 API가 3.x와 다르다.
- `python-can` 4.x도 Python 3.7 이상이 필요하다. `pyserial` 3.5는 PyPI에 버전 제한이 없다.
- 장비 CLI 도구를 Python으로 짤지, C/C++로 짤지, Nano에 새 Python을 설치할지는 첫 주 실측에서 정한다.

## 5. 참고: 20만원 안 조합 (본체 합계)

| 조합 | 구성 | 본체 합계 |
|---|---|---|
| 데이터 진단 (조사 문서 조합 2) | B + C + USB-RS485 | $59.97 (약 8.0만원) |
| 데이터 진단 + CAN | 위 조합 + H | $83.95 (약 11.1만원) |

STM32는 보유 중이라 합계에서 뺐다. 전원·4–20mA 신호원·배선·배송비·세금도 위 합계에 들어 있지 않다.

---

## 별첨 A. 회사별 관련 직무 (상세)

이 별첨은 후보 표의 연관 줄이 어떤 공고·직무 설명에서 나왔는지 정리한다. 합격 가능성이나 기업의 특정 장비 사용을 보장하지 않는다. 삼성·세메스의 내부 BOM, 납품사, 특정 보드 사용 사실은 확인하지 못했다.

- 근거 표시는 "읽는 법"과 같다. [경력]에는 마감된 과거 공고도 포함한다.
- "맞닿는 점" 칸은 조사 문서와 이 문서의 추론이다. 기업의 공식 우대사항이 아니다.

| 회사 · 근거 | 관련 직무·업무 | 맞닿는 점(추론) | 재확인 |
|---|---|---|---|
| **세메스** · [직무소개] S1 S/W설계 | Embedded SW: 실시간 제어, 초정밀·초고속 Motion 제어, 신호처리, Firmware 설계·평가·성능 최적화<br>Middleware SW: 설비제어 SW Platform(Cluster 공정·Display 설비·검사설비·Robot 등), 고속 Network Protocol(Field bus), 실시간 OS, Device Driver<br>Application SW: AI 기반 ML/DL, 음성·자연어·영상 처리, 설비 Big Data 분석(생산·수리 예측)<br>SW Engineering: 개발 인프라·툴, 자동화, SW 분석·품질관리<br>Requirements: C/C++/C#/Python/Java 등 프로그래밍·알고리즘 역량, 요구사항에 맞는 SW 설계·구현<br>Pluses: SW·HW 플랫폼 경진대회 수상·프로젝트 수행 경험, 영어·중국어 회화 | 펌웨어·장비 통신·설비 데이터 분석·자동 테스트가 모두 직무 설명에 있음 | 2026-10-29 |
| **세메스** · [경력] S2 | 초정밀 장비제어 SW: Fieldbus & H/W Interface, 제어 SW(Sensor/Motion 제어), Platform 기반 SW, WPF·C# 응용<br>설비 예지 진단: 부품·성능 이상 진단, 이상 예측·분석 모델, 자동 진단 | 장비 통신 진단, 센서 이상 탐지 | 2026-10-29 |
| **세메스** · [경력] S3 | CTC(Cluster Tool Controller): 설비 Scheduling SW, 설비 UI/GUI, Fab Automation SW<br>PMC(Process Module Control): 설비 모듈·Unit 구동 제어 SW<br>구동부(모터·액추에이터·밸브) 또는 공정 제어용 Sequence Programming 경력 | PLC 시퀀스, 모션 모형 | 2026-10-29 |
| **삼성전자 DS** · [경력] D1(외국인 경력 R&D) | Edge/Cloud Computing, 설비 제어 공통 플랫폼, 설비 데이터 분석·진단 통합 플랫폼, 설비 상태 진단 Agent, RAG·LLM 평가·vLLM/SGLang<br>2년 이상 유관경력 | 하이브리드 Edge/Server 구조, 현장 진단 Agent | 안 함 |
| **삼성디스플레이** · [신입] SD1(2026 하반기 3급 SW개발) | Smart Factory 제어 시스템 설계·SW 개발, 영상처리·AI 기반 검사 설비 SW 개발<br>PLC·Fieldbus·STM32 우대는 적혀 있지 않음 | 설비 제어 SW, 이상 탐지 | 안 함 |
| **삼성전기** · [경력] SE1·SE2 | MLCC 설비개발: 자동화 설비 제어, 고정밀 모션 제어. 5년 이상 경력, PC/PLC 제어 설계·모션제어 SW 우대<br>S/W 개발: AI, IT/전장 Embedded SW, 머신비전 검사 SW. 2년 이상 경력<br>설비개발: 제어/계측, PLC 제어, SW. 2년 이상 경력 | PLC, 모션, 임베디드 SW | 안 함 |
| **삼성SDI** · [직무소개] SI1 S/W 개발 | 스마트 팩토리 제어 시스템·검사 설비 SW 개발, 배터리 모듈/팩 SW·BMS 알고리즘 개발 | 설비 I/O 진단, CAN·BMS 실험 | 2026-10-29 |
| **삼성전자 DX** · [신입] DX1(2026 하반기 시스템 소프트웨어) | 하드웨어 제어를 위한 드라이버·컴파일러·펌웨어 등 시스템 SW<br>MCU·RTOS·PLC 우대는 적혀 있지 않음 | STM32 펌웨어, UART·인터럽트, 통신 드라이버 | 안 함 |

재확인 칸의 날짜는 공식 페이지를 직접 열어 내용을 대조한 날이다. "안 함"은 조사 문서 내용을 그대로 옮긴 것이다. 삼성채용 공고 SE1은 정적 페이지로 본문이 열리지 않았고, 나머지 공고는 열어 보지 않았다.

## 별첨 B. 후보별 연관 근거 (상세)

| 후보 | 맞닿는 직무 기술 | 근거 | 주의 |
|---|---|---|---|
| 공통: STM32 NUCLEO-F103RB | C/C++ 펌웨어, UART·인터럽트, Device Driver | 세메스 S1(Embedded SW·Requirements) · 삼성전자 DX1 | 기업이 STM32를 쓴다는 뜻이 아님 |
| 공통: Jetson Edge AI + 서버 LLM | 설비 데이터 분석, 이상 진단, 진단 Agent | 세메스 S1(Application SW) · S2(설비 예지 진단) · 삼성전자 DS D1 | 진단 성능은 실험으로 검증해야 함. D1은 경력 공고 |
| A. LS PLC | 시퀀스·인터록, 구동부 Sequence Programming | 세메스 S3 · 삼성전기 SE1·SE2 | 근거가 모두 경력 공고라 신입 요건이 아님. 해당 기업이 LS PLC를 쓴다는 근거 없음 |
| B. Waveshare RTU IO | Field bus·H/W Interface, 장비 통신 진단 | 세메스 S1(Middleware) · S2 | Modbus RTU는 Field bus 입문 수준이라 "고속 Network Protocol"을 직접 보여 주지는 못함. 세메스가 Modbus를 쓴다는 근거 없음 |
| C. Waveshare Analog Input | 센서 계측, 설비 데이터 분석, 예지 진단 | 세메스 S1(Application SW) · S2(설비 예지 진단) · 삼성SDI SI1(검사 설비 SW) | 4–20mA는 일반 산업 계측 인터페이스이고 반도체 전용이 아님 |
| D. Waveshare PoE ETH IO | 다중 장비 네트워크 진단, 설비 제어 플랫폼 | 세메스 S1(Middleware) · 삼성전자 DS D1 | Modbus TCP는 EtherCAT 같은 고속 Field bus가 아님 |
| E. ADAM-4055 | B와 같음 + 절연·워치독을 갖춘 산업 장비 | 세메스 S1 · S2 | 가격이 높다고 세메스가 쓴다는 뜻이 아님 |
| F. Beckhoff EtherCAT | 고속 Field bus, 실시간 제어 | 세메스 S1(Middleware "고속 Network Protocol(Field bus)") · S2 | 세메스 S1·S2·S3 페이지에 EtherCAT이라는 이름은 없음 |
| G. 스테퍼 모션 세트 | Motion 제어, 구동부 Sequence, 센서 제어 | 세메스 S1(Embedded SW) · S2 · S3 · 삼성전기 SE1 | 개루프 스테퍼는 "초정밀 Motion"이 아님. 정밀도를 말하려면 위치 피드백이 필요 |
| H. CAN 실험 세트 | 차량·배터리 임베디드 통신, BMS | 삼성SDI SI1(배터리 모듈/팩 SW·BMS) · 삼성전기 SE2(IT/전장 Embedded SW) | 확인한 SI1 페이지에 CAN이라는 단어는 없음. BMS·전장과의 연결은 조사 문서의 추론 |

## 별첨 C. 보드 밖 연관 요소

- **SECS/GEM**(SEMI E5·E37·E30): 반도체 장비와 상위 호스트 사이의 통신 표준이다. 보드 없이 시뮬레이터로 개념을 구현할 수 있다. 표준 인증을 받은 구현이라고 주장하지 않는다(조사 문서 5.2절).

## 출처

- Waveshare 공식몰 (2026-10-28 확인)
  - Modbus RTU IO 8CH: https://www.waveshare.com/modbus-rtu-io-8ch.htm
  - Modbus RTU Analog Input 8CH: https://www.waveshare.com/modbus-rtu-analog-input-8ch.htm
  - Modbus PoE ETH IO 8CH: https://www.waveshare.com/modbus-poe-eth-io-8ch.htm
  - USB TO RS485: https://www.waveshare.com/usb-to-rs485.htm
  - USB-CAN-A: https://www.waveshare.com/usb-can-a.htm
  - SN65HVD230 CAN Board: https://www.waveshare.com/sn65hvd230-can-board.htm
- 조사 문서의 출처를 그대로 옮긴 것 (다시 확인하지 않음)
  - LS XGB 제품 자료 [P4]: https://www.ls-electric.com/upload/customer/download/8c43827b-9984-4962-b1ec-890a4d9814a3/XGB_E_151005.pdf
  - 디바이스마트 LS XBM-DN16S [P5]: https://www.devicemart.co.kr/goods/brand?category_code=0004&code=2041&iframe=&popup=&sort=popular
  - TME Beckhoff [P6]: https://www.tme.com/kr/ko/katalog/ipch-ullyok-sst-em-mit-mdyul_118409/params/b2131_t-ongsin-p-rt-k-ol/p1791398_ethercat/
  - Advantech ADAM-4055 [P7]: https://www.advantech.com/ko-kr/products/gf-5vwk/adam-4055/mod_fd19e628-4ea5-4c16-915c-5ceeef2fb65c
- 환율 (ECB 기준, 2026-10-27): https://api.frankfurter.dev/v1/latest?base=USD&symbols=KRW
- PyPI: https://pypi.org/project/pymodbus/ · https://pypi.org/project/python-can/ · https://pypi.org/project/pyserial/
- 직무·채용 (2026-10-29 공식 페이지에서 다시 확인)
  - [S1] 세메스 S/W설계 직무안내: https://www.semes.com/ko/careers/job-introduction/view
  - [S2] 세메스 경력 채용(초정밀 장비제어 SW·설비 예지 진단): https://semes.com/ko/careers/job-opening/detail/7
  - [S3] 세메스 경력 채용(CTC·PMC·Sequence Programming): https://semes.com/ko/careers/job-opening/detail/13
  - [SI1] 삼성SDI S/W 개발 직무소개: https://www.samsungcareers.com/subsid/detail/C31
- 직무·채용 (조사 문서 출처를 그대로 옮긴 것 · 다시 확인하지 않음)
  - [D1] 삼성전자 DS부문 R&D 외국인 경력사원 공고: https://www.samsungcareers.com/hr/?no=22880
  - [SD1] 삼성디스플레이 2026년 하반기 3급 신입 SW개발 공고: https://www.samsungcareers.com/hr/?no=22985
  - [SE1] 삼성전기 경력 MLCC 설비개발 공고: https://www.samsungcareers.com/hr/?no=23175
  - [SE2] 삼성전기 경력 SW·설비개발 공고: https://www.samsungcareers.com/hr/?no=22841
  - [DX1] 삼성전자 DX 2026년 하반기 신입 시스템 소프트웨어 공고: https://www.samsungcareers.com/hr/?no=23055
