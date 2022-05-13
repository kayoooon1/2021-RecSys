# Adaptive Sequential Model Generation   

* Reviewer : 김가윤   
* Date : 2022-05-13   
   
## ABSTRACT   
* ASMG framework generates a better serving model from sequence of historical models via a meta generator, 메타 생성기를 통해 모델 히스토리를 가지고 더 나은 모델을 생성한다.   
* 메타 생성기를 만들 때 Gated Recurrent Units, GRUs 사용 해서 long term dependencies 포착해 ability를 최대화한다   

## INTRODUCTION   
* 업데이트가 중요해진 요즘, 새로운 데이터가 나타날 때마다 시기적으로 업데이트를 하는 것이 중요   
* 이전 연구에서는 새롭게 나타난 데이터 (incremental update)만 혹은 슬라이딩 윈도를 사용해 w 시기만을 업데이트 가능 (batch update), incremetal update가 주로 많이 사용되지만 = BUT, forgetting problem   
* Main focus : How to effectively transfer past knowledge especially useful for future predictions?   
* 문제 해결을 위한 2가지 방법 : sample-based approach, model-based approach = long-term sequential patterns를 무시한다는 한계가 있다.    
    * Continual learning에서 고안한 방법들
    * 해결을 위해 ASMG 고안
    * 과거 지식을 뽑아서 다음 시기 데이터에 최적화 하도록 train   
    * long term dependencies 강화하기 위해 GRUs 사용

## RELATED WORK   
### Continual Learning   
* Continual learning 종류 3가지 : Experience replay, Regularization-based, Model Fusion    
    * Continual learning : 현 데이터만 학습하게 되는 (과거 데이터를 기억하지 못하는) 문제점을 해결하기 위한 연구 분야
1. Experience Replay    
    *  업데이트 시 새로운 데이터와 과거 샘플들을 같이 재사용하면서 forget 문제를 해결    
2. Regularization based   
    * 중요도에 따라 파라미터 업데이트를 제한해 과거 지식을 얻는 것    
3. Model fusion    
    * 점진적으로 sub-networks를 포함하면서 continual learning    

= RS에서도 잘 작동시키기 위해 여러 방법 고안 중

### Sample-based Approach   
* RSs incremental update에서 생기는 forgetting issue 해결 방법 중 하나, continual learning에서 착안   
* Short term interest & Long term memory 사이에서 aiming to find the balance
* Reusing historical samples 하기 때문에 1번과 유사하다고 볼 수 있음   
* Reservoir(keep a random sample of history)
* Heuristics : Designed to Reservoir에서 샘플들 골라서 모델 업데이트, 새로운 데이터 우선시 할지 or 과거 데이터 버릴지...    
* *문제점* : individual samples, 전체 분포의 큰 그림을 재현하기 충분치 않다. = 전체를 충분하게 대표하지 못한다   
    -> past, present models 사이에서 knowledge transfer하는 model based approach 등장   

### Model-based Approach   
* Regularization based와 유사, 모델 파라미터 업데이트 위해 knowledge distillation loss 사용하기 때문   
* 그러나 제한만 한다고 해서 knowledge가 future prediction에 useful하다고 볼 수 없다.   
* 이에 관련해 고안된 *Sequential Meta Learning(SML)* !!   
    - 이전 모듈을 과거와 현재 모델에 결합하도록 설계하고, 순차적 방식으로 적응적으로 훈련하여 향후 서비스를 최적화   
* *문제점* : ONLY 연속적인 periods들의 transfer만 고려한다.   

## METHODOLOGY   