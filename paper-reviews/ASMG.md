# Adaptive Sequential Model Generation   

* Reviewer : 김가윤   
* Date : 2022-05-13   
   
## ABSTRACT   
* ASMG framework generates a better serving model from sequence of historical models via a meta generator, 메타 생성기를 통해 모델 히스토리를 가지고 더 나은 모델을 생성한다.   
* 메타 생성기를 만들 때 Gated Recurrent Units, GRUs 사용 해서 long term dependencies 포착해 ability를 최대화한다   

## INTRODUCTION   
* 업데이트가 중요해진 요즘, 새로운 데이터가 나타날 때마다 시기적으로 업데이트를 하는 것이 중요   
* 이전 연구에서는 새롭게 나타난 데이터 (incremental update)만 혹은 슬라이딩 윈도를 사용해 w 시기만을 업데이트 가능 (batch update), incremetal update가 주로 많이 사용 = BUT, forgetting problem   
* Main focus : How to effectively transfer past knowledge especially useful for future predictions?   
* 문제 해결을 위해 