# Abstract   
* CARE   
    * 환자들의 의료 기록을 활동해 환자들의 병 예측   
    * Collaborative filtering 사용하여 개인 의료 기록과 비슷한 환자들의 병을 예측   

* ICARE
    * Iterative version   
    * 향상된 성능을 위한 앙상블 개념을 통합   
    * Apply time-sensitive modifications   


# Introduction   
* 현재의 의료는 선제적 치료가 아니라 질병의 증상이 나타나면 즉시 개입하여 초기 징후에 질병을 치료하는 사후적 치료   
* genome revolution에 의해 이점을 보고 있으나 단점도 존재   
* phenotype : 표현형(表現型, phenotype) 또는 발현형질(發現形質)은 생명학에서, 생명체가 유전적인 정보를 이용하여, 세포, 조직 및 개체에 단백질과 당을 통해 생산한 기능적 형질   
* 본 논문의 목표는 표현형과 질병 이력 기반 접근이 질병 예측에 탁월하다는 것을 보여주는 것 :smiley:   

## 1.1 Contribution   
* Collaborative filtering methodology   
* Each user is a patient whose profile is a vector of diagnosed diseases(진단 병명).   
* Ratings = Binary (환자가 병이 있으면 1, 없으면 0), 음악과 영화와 달리 유저가 선택하는 것이 아님   
1. International classification of Disease code를 사용한다.   
2. 사용된 협업 필터링 방법은 이전 작업을 기반으로 하며 CARE 내에서 의미 테스트 및 앙상블 방법의 새로운 요소를 통합   
3. A time sensitive   

# Related Work   
