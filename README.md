# Healthcare-Waiting-System
한국건강관리협회 건강증진의원의 대기 시스템 최적화

📅 **기간**:  Mar 2025 – Jun 2025  

## 📖 연구 개요

본 프로젝트는 국가건강검진 및 일반 건강검진을 제공하는 지역 보건기관인 **한국건강관리협회 건강증진의원 수원지부**를 대상으로 **시뮬레이션 모델을 구축**하고, **대기 시스템을 최적화**하는 것을 목표로 합니다. 

## 🔍 연구 필요성

- **영업 초반에 접수처에 긴 대기열 형성**: 예약 시스템이 30분 간격으로 운영되고 있지만 실제로는 고객들이 예약 시간에 맞춰 방문하기보다는 오픈 시간대에 집중되어 병목현상이 발생
- **일부 검진 항목에 긴 대기열 형성**: 일부 검진 항목은 특정 성별이나 연령대의 고객만 이용하는데, 이러한 고객들이 특정 시간대에 집중될 경우 해당 검진 항목의 대기열이 길어져 결과적으로 전체 체류시간이 길어지는 문제 발생

## 📂 프로젝트 구조

```
├── data/                        
│   ├── after/                   # DEA 분석 이후 데이터
│   │   ├── DEA results/         # DEA 결과 데이터
│   │   │   ├── cluster_1_input_BCC.csv
│   │   │   ├── cluster_1_input_CCR.csv
│   │   │   ├── cluster_1_output_BCC.csv
│   │   │   ├── cluster_1_output_CCR.csv
│   │   │   ├── cluster_2_input_BCC.csv
│   │   │   ├── cluster_2_input_CCR.csv
│   │   │   ├── cluster_2_output_BCC.csv
│   │   │   ├── cluster_2_output_CCR.csv
│   │   │   ├── cluster_3_input_BCC.csv
│   │   │   ├── cluster_3_input_CCR.csv
│   │   │   ├── cluster_3_output_BCC.csv
│   │   │   ├── cluster_3_output_CCR.csv
│   │   │   ├── clusterdata_3.csv
│   │   │   ├── final_data_1.csv
│   │   │   ├── output_model.xlsx
│   ├── before/                  # 원본 데이터
│   │   ├── 근로복지공단_고용 산재보험 가입 현황_20231231.csv
│   │   ├── 근로복지공단_고용산재보험 가입 현황_20231231(1).csv
│   │   ├── 근로복지공단_고용산재보험 가입 현황_20231231(2).csv
│   │   ├── 근로복지공단_고용산재보험 가입 현황_20231231(3).csv
│   │   ├── 근로복지공단_고용산재보험 가입 현황_20231231(4).csv
│   │   ├── 근로복지공단_고용산재보험 가입 현황_20231231(5).csv
│   │   ├── [카카오] 대규모기업집단현황공시.pdf
│   │   ├── 결측, 상장기업 제거, cluster 추가 로우데이터.xlsx
│   │   ├── 카카오 계열사 로우데이터.xlsx
├── modeling/                    
│   ├── dea_최종.R                # DEA 분석 코드
├── preprocessing/                
│   ├── cluster_final.ipynb       # 데이터 전처리 및 클러스터링 코드 
├── README.md                     # 연구 설명
```

## 📊 데이터 설명

- **데이터 수집 기간**: 2025년 5월 24일 토요일 오전 7시 30분 -오후 12시 30분
- **수집한 데이터**
  - 성별 및 연령별 검진 프로세스
  - 접수처와 수납처 창구 수
  - 각 검진별 의료진 수
  - 고객의 Inter-arrival time
  - 각 검진별 Processing time
  - 다음 검진 서버까지의 이동시간
 
## 🎯 연구 과정

### **1️⃣ 인풋 분석**
- **Inter-arrival time과 Processing time의 모집단 분포를 추정**하기 위해 **@Risk** 소프트웨어를 활용하여 각 분포에 대한 **적합도 검정(Goodness of Fit test)**을 수행
- 주어진 데이터셋에 대한 예측 오차를 추정하고 통계 모델의 상대적인 적합도를 평가하는 지표인 **AIC(Akaike Information Criterion)**를 기준으로 사용

### **2️⃣ Baseline 모델 구축**

<img width="940" height="415" alt="image" src="https://github.com/user-attachments/assets/c62b2f37-1b25-47a1-977d-140b2ccd2d24" />

- **Model Entity**
  
  <img width="457" height="131" alt="image" src="https://github.com/user-attachments/assets/5f677b0e-44ec-4041-8174-32d6fbdc5930" />
  
- **Source**
  
  <img width="457" height="191" alt="image" src="https://github.com/user-attachments/assets/98238dd3-f278-406d-ab64-7772ecdcd2e4" />
  
- **Server**
  
  <img width="470" height="292" alt="image" src="https://github.com/user-attachments/assets/9955d301-30a1-48e8-8e6d-554960eb2520" />
  
- **Time Path**
  
  <img width="457" height="326" alt="image" src="https://github.com/user-attachments/assets/6c491fad-cf2a-4c85-ba5c-edc734b80ade" />
  
- **Baseline 모델의 타당성 검증**
  
  <img width="320" height="128" alt="image" src="https://github.com/user-attachments/assets/f378360c-5d7c-40c5-bed1-1e9dbc310e78" />

  <img width="460" height="110" alt="image" src="https://github.com/user-attachments/assets/c4e310e4-81e9-4144-b57d-b67d96c1780d" />

### **3️⃣ Alternative 1**
- Baseline 모델은 Registration에 13명, Accounting에 3명을 각각 고정 배치 
- Alternative 1은 Registration 13명, Accounting 3명으로 기본 배치하되, 한쪽에 일이 몰릴 경우 남는 인력을 다른 쪽에 유동적으로 지원 가능

### **4️⃣ Alternative 2**
- 각 시간대에 대해 같은 특성을 가진 고객이 균등하게 배분되도록 예약 인원을 제한
  
  <img width="437" height="140" alt="image" src="https://github.com/user-attachments/assets/7e910471-35a7-426b-a126-a0a24425a6b6" />
  
- 각 엔티티에 대해 대안을 적용할지 여부를 독립적으로 설정할 수 있으므로 총 16개의 시나리오가 도출
  
  <img width="438" height="267" alt="image" src="https://github.com/user-attachments/assets/54bccf70-772c-4493-a854-3607cd1bb6c8" />

### **5️⃣ 아웃풋 분석**
- **Alternative 1**
  - Registration 서버의 병목을 해소하면서 접수처의 대기시간과 총 처리 고객 수는 개선되었지만, 시스템 전반적으로 L, W 증가
    
    <img width="442" height="186" alt="image" src="https://github.com/user-attachments/assets/8717a7e1-d451-45de-8619-78b35942c5bc" />
    
  - 유의수준 α=0.05에서 T-test를 수행한 결과, Average_W와 Sum_L에 대해서는 Alternative1과 Baseline 모델 간에 통계적으로 유의미한 차이가 없지만 Registration_Wq의 경우에는 대안 1이 기존 모델에 비해 통계적으로 유의미하게 감소
    
    <img width="437" height="107" alt="image" src="https://github.com/user-attachments/assets/b932346c-9b33-4fa0-8da2-8d16a36df941" />
- **Alternative 2**
  - 모든 엔티티에 대해 예약 인원을 균등하게 제한한 Scenario 16이 시나리오들 중 Average_W, 대장내시경을 진행하는 40세 이상의 여성의 W를 제외한 엔티티들의 W, Dental_WQ와 Registration_WQ 값이 최소
    
    <img width="438" height="184" alt="image" src="https://github.com/user-attachments/assets/52d03354-1457-42ba-bfb6-058a18a7aace" />
    
  - 유의수준 α=0.05에 대하여 T-test를 수행한 결과, Alternative2 모델이 Baseline 모델에 비해 평균 시스템 체류 시간, Dental 서버와 Registration 서버에서의 대기 시간이 통계적으로 유의미하게 감소
    
   <img width="438" height="106" alt="image" src="https://github.com/user-attachments/assets/5702052e-2bc2-4379-ba10-32bb4022695f" />

