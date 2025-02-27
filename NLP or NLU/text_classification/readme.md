# text_classification

모델 10개 찾고 장단점 적기

## 전통적인 머신러닝에 기반한 모델(SVM/로지스틱 회귀 등)
사람이 직접 추출한(hand-crafted) 피처에 강하게 의존, 이러한 피처들은 추출하는 데 시간이 많이 소요되고 많은 경우 불완전함

## 딥러닝 모델(CNN,RNN, Recursive NN 등)
딥러닝은 많은 양의 계산과 데이터를 활용하는 기법으로, 수작업 피처 엔지니어링을 거의 하지 않아도 된다.
피처 엔지니어링이란 해당 분야의 도메인 지식을 활용하여 기계학습 알고리즘을 작동시키기 위한 입력 특징(feature)을 추출하는 과정을 말한다. 손으로 한땀한땀 만들어내는 수작업에 가깝다. 딥러닝은 이러한 피처 엔지니어링의 도움을 받지 않고도 높은 성능으로 주목을 받고 있다.
자동화된 피처 추출 및 표현(multi-level automatic feature representation learning)

단어 임베딩 : 분산표상으로 표현된 벡터(Distributional vectors) 또는 단어 임베딩(Word Embedding)은 근본적으로는 distributional hypothesis를 전제로 한다. 이 가정은 비슷한 의미를 지난 단어는 비슷한 문맥에 등장하는 경향이 있을 것이라는 내용이 핵심이다. 따라서 이 벡터들은 이웃한 단어의 특징을 잡아내고자 한다., 분산표상 벡터의 주된 장점은 이 벡터들이 단어 간 유사성을 내포하고 있다는 점이다. 코사인 유사도 같은 지표를 사용함으로써 벡터간 유사성을 측정할 수 있다.

단어 임베딩은 딥러닝 모델의 첫번째 데이터 처리 계층에 자주 사용된다. 일반적으로, 단어 임베딩은 레이블이 없는 방대한 말뭉치에서 '보조적인 목적함수(예컨대 이웃단어로 중심단어를 예측한다. 각 단어벡터는 일반적인 문법적, 의미적 정보를 내포한다)'를 최적화함으로써 사전 학습된다. 단어 임베딩은 문맥 유사도를 잡아내는 데 효율적이라는 사실이 증명되었다. 또한 임베딩 벡터의 차원이 작은 덕분에 계산이 빠르고 효율적이다. 
이러한 임베딩 벡터를 생성하는 모델은 수년간 얕은(간단한) 뉴럴네트워크였다. 좋은 임베딩을 생성하는데 있어 깊은 구조의 뉴럴네트워크가 필요하지 않았다. 그러나 딥러닝 기반의 NLP모델은 언제나 이러한 임베딩 벡터를 활용해 단어,구,문장을 표현한다. 이는 사실 전통적인 단어 빈도수 기반의 모델과 딥러닝 기반의 모델 간의 가장 큰 차이점이다. 

## 모델들
1. RNN
RNN은 신경망 속 셀의 현재 출력 결과가 이전의 계산 결과에 영향을 받는 인공신경망 모델이다. 다시 말해, 이전 계산 결과에 대한 메모리 정보를 가지고 있어 순차적인 데이터를 학습하는데 장점을 가지고 있다. 기본적인 RNN은 일반적으로 학습이 어려워 다양한 변형이 발생했는데, 그 중 가장 성공적인 모델은 장기-단기 기억 신경망(Long-Short Term Memory: LSTM)과 최근 각광받고 있는 회로형 순환 유닛(Gated Recurrent Units: GRU)이 있다.  
RNN은 순차적인 정보를 처리하는 네트워크다. 전통적인 뉴럴 네트워크와 달리, RNN은 모든 입력값이 독립적이라고 가정한다. 'recurrent'라는 용어는 모델이 입력 시퀀스의 각 인스턴스에 대해 같은 작업을 수행하고 아웃풋은 이전 연산 및 결과에 의존적이라는 데에서 붙었다.일반적으로 recurrent unit에 토큰을 하나씩 입력함으로써 고정 크기의 벡터가 시퀀스를 표현하기 위해 생성된다. 이런 방식으로 RNN은 이전 연산결과를 '기억'하고, 현재 연산 과정에서 이 정보를 활용한다. 이러한 템플릿은 랭귀지 모델링(Mikolov et al., 2010, 2011; Sutskever et al., 2011), 기계번역(Liu et al., 2014; Auli et al., 2013; Sutskever et al., 2014), 음성인식(Robinson et al., 1996; Graves et al., 2013; Graves and Jaitly, 2014; Sak et al., 2014), 이미지 캡셔닝(Karpathy and Fei-Fei, 2015) 등과 같은 많은 NLP 작업에 적합하다. 이로 인해 최근 수년 간 NLP 어플리케이션에 RNN이 널리 보급됐다.
RNN은 데이터를 순차적으로 처리하기 때문에, 언어에서 고유한 순차적인 성격을 포착할 수 있는 능력이 있다. 단어는 이전 단어를 바탕으로 의미를 갖게 된다. 이와 관련한 간단한 예시는 'dog'와 'hot dog'간의 의미 차이일 것이다. RNN은 이러한 문맥 의존성을 모델링하기 위해 만들어졌으며 연구자들이 CNN보다 RNN을 사용하는 강한 동기가 되었다.
RNN이 시퀀스 모델링에 적합한 다른 요인은 매우 긴 문장, 단락, 심지어 문서(Tang et al., 2015)를 포함해 다양한 텍스트 길이를 모델링할 수 있는 능력이다. CNN과 달리 RNN은 무제한 컨텍스트를 포착할 수 있는 유연한 계산 step을 가진다. 임의의 길이의 입력값을 처리할 수 있는 이러한 능력은 RNN을 사용하는 주요 연구의 셀링포인트 가운데 하나가 됐다(Chung et al., 2014). 
다수의 NLP 태스크는 또한 전체 문장에 대해 의미론적 모델링을 요구한다. 이것은 고정된 차원의 하이퍼스페이스 내에 문장의 요지(gist)를 만들어내는 것과 관련이 있다. 이들 인스턴스는 RNN에 의해 적절히 포착된다. 전체 문장이 고정된 벡터로 요약되고 나서 가변 길이의 타겟 시퀀스로 매핑되는 기계번역(Cho et al., 2014) 같은 작업에 RNN 사용이 증가했다.
RNN은 또한 시간 분산 조인트 처리(time distributed joint processing)를 위한 네트워크 지원을 제공한다. 품사태깅(Santos and Zadrozny, 2014) 같은 시퀀스 레이블링 작업의 대부분은 이러한 domain에 기반한 것이다. 보다 구체적인 사용사례는 문서분류(Chaturvedi et al., 2016), 다범주 텍스트 범주화(Chen et al., 2017), 멀티모달 감성분석(Poria et al., 2017; Zadeh et al., 2017; Tong et al., 2017), 주관성 디텍션(Chaturvedi et al., 2017) 등이 있다.
이미 서술한 사실들은 연구자들이 RNN을 선택하는 동기가 되는 몇가지 이유다. 그러나 RNN이 다른 네트워크보다 우월하다고 결론을 내리는 것은 잘못된 것이다. 최근에 여러 연구는 CNN이 RNN보다 우월하다는 증거를 제시한다. 언어모델링(Langurage modeling) 같은 RNN에 적합한 태스크일지라도, CNN은 RNN보다 경쟁력 있는 성능을 달성했다(Dauphin et al., 2016). CNN과 RNN은 문장을 모델링할 때 다른 목적(함수)를 갖는다. RNN이 경계없는 긴 문장을 생성하려고 하는 반면, CNN은 가장 중요한 n-gram을 추출하려고 한다. 둘다 n-gram 피처를 잡아내는 데 효율적이지만, 단어 순서에 대한 민감도가 지역적으로(locally) 제한되며 장기(long-term) 의존성은 보통 무시된다.
Yin et al. (2017)은 RNN과 CNN 성능에 관한 흥미있는 인사이트를 제시한다. 감성분류, QA, 품사태깅을 포함하는 여러 NLP task를 평가한 후에 그들은 ‘완전한 승자는 없다’고 결론 내렸다. 각 네트워크의 성능은 태스크가 요구하는 글로벌 시맨틱(global semantics)에 의존한다. 아래에서는 최근 연구에서 광범위하게 사용되는 RNN 모델 중 일부에 대해 설명한다.
간단한 RNN 네트워크는 악명 높은 배니싱 그래디언트 문제(Vanishing gradient problem)로 인해, 네트워크에서 이전 레이어의 파라메터를 학습하고 업데이트하는 걸 매우 어렵게 만든다. 이러한 제한은 LSTM, GRU 및 ResNet과 같은 다양한 네트워크에 의해 극복되었다.
NLP 분야에서 도전적인 과제는 자연어를 생성하는 일이다. 이는 RNN의 또다른 어플리케이션이기도 하다. 텍스트 혹은 시각적 데이터가 주어졌을 때, deep LSTM은 기계번역, 이미지 캡셔닝 등 태스크에서 합리적인 성능을 보였다. 그런 사례에서 RNN은 디코더(decoder)로 불린다(본 블로그).
입력이 순차적으로 주어지는 상황에 대해 많이 사용되는 인공신경망 모델인 RNN은 중요한 입력과 그렇지 않은 입력을 모두 동일한 정도로 읽는 단점을 갖는다. Skim-RNN은 주어진 입력을 읽는 정도를 조절하도록 하여 위의 단점을 개선한 모델이며, 분류 작업(classification task)에 대해서는 연산량을 줄이는 동시에 높은 정확도를 보인다는 것이 실험 결과로 확인된 바 있다. 


   * 장점 : 반복적이고 순차적인 데이터(Sequential data)학습에 특화, 현재의 학습과 과거의 학습이 연결, 과거의 정보를 통해 미래를 예측, 시간상의 순서가 있는 task에 적절, 이전의 정보를 현재의 문제 해결에 활용할 수 있음, 이벤트의 연속, 리스트에 관련된 문제를 해결하기 적절 
   * 단점 : 학습이 어려움, 시간이 오래 걸림, 장기 의존성 문제 해결 불가(처음 시작한 Weight의 값이 점차 학습이 될수록 상쇄됨) 

2. bi-LSTM, LSTM-GRNN
LSTM은 긴 순차적인 정보를 회로 메커니즘(gating mechanism)을 통해 저장하고 출력할 수 있따. 이 회로 메커니즘은 RNN의 학습을 방해하는 가장 큰 원인인 vanishing gradient 문제를 완화시켜 성능을 크게 향상시켰다. 
LSTM(Hochreiter and Schmidhuber, 1997; Gers et al., 1999, 그림 10)은 간단한 RNN에 forget gate를 추가했다. 이러한 독특한 매커니즘을 통해 배니싱 그래디언트 문제, 익스플로딩 그래디언트 문제(exploding gradient problem_를 모두 극복할 수 있다(본 블로그).
vanilla RNN과 달리 LSTM을 사용하면 오차가 무제한적인 time step에 역전파될 수 있다. 3개의 gate, 즉 input/forget/output gate로 구성되며 히든 스테이트는 아래 식에 따라 계산된다.

    * 장점 : cell gate를 통한 RNN의 장기 의존성 문제 해결(Weight를 계속 기억할지 결정하여 Gradient Vanishing 문제를 해결), 과거의 data를 계속해서 update 하므로, RNN보다 지속적, Cell State는 정보를 추가하거나 삭제하는 기능을 담당, 각각의 메모리 컨트롤 가능, 결과값 컨트롤 가능 
    * 단점 : 메모리가 덮어씌워질 가능성(더 자세히?), 연산속도가 느리다(파라미터 수를 생각해도), 파라미터 수가 많다.

3. CNN-char, CNN-word (Convolutional Neural Networks)
CNN은 사람의 시신경망에서 아이디어를 얻어 고안한 모델로, 다양한 패턴 인식 문제에 사용되고 있다. CNN은 컨볼루션 층, subsampling층(또는 max-pooling층)이라는 두 층을 번갈아가며 수행하다가 마지막에 있는 fully-connected층을 이용하여 분류를 수행한다. 컨볼루션 층은 입력에 대해 2차원 필터링을 수행하고, subsampling층은 매핑된 2차원 이미지에서 최댓값을 추출한다. 이러한 계층구조 속에서 역전파(backpropagation)을 이용, 오차를 최소화하는 방향으로 학습해나간다. 주로 비전 분야에서 얼굴 인식, 필기체 인식 등에 많이 사용되어 왔으나 최근에는 자연어 처리분야에서도 널리 활용되고 있다.
CNN은 텍스트 길이에 따라 성능이 달라진다. 이런 상이함은 Johnson and Zhang(2015)와 같은 많은 연구에 나타난다. 장문의 텍스트에 대한 CNN 모델의 성능은 좋았던 반면 짧은 텍스트에선 반대였다. Wang et al.(2015b)는 짧은 텍스트의 표현(representation)을 모델링하는 데 CNN을 제안했다. 저자들은 단문의 외부적 지식이 사용된 multi-scale semantic units를 도입한 의미론적 클러스터링(semantic clustering)을 제안했다. CNN은 이러한 유닛들을 결합하고 전체적인 표현(represention)을 만들어내는 데 쓰인다.
기계번역 같은 작업에는 순차적인 정보와 장기 의존성에 대한 인내(perseverance)가 필요하다. 따라서 구조적으로 이러한 작업들은 이러한 피처들을 잃어버리는 CNN 네트워크에 적합하지 않다. 
CNN은 본질적으로 로컬 연결성(local connectivity), 가중치 공유, 풀링 등의 특징이 있다. 이러한 속성은 많은 task에서 고도로 요구되는 불변성(invariance)을 어느 정도 보장한다. 음성 인식 또한 이러한 불변성을 필요로 한다. 이 때문에 Abdel-Hamid et al. (2014)는 하이브리드 CNN-HMM 모델을 사용했다. 이 변동성은 종종 화자 차이에 기인한 음성 신호에서 종종 발견된다. Abdel-Hamid et al. (2014)는 또한 파라메터를 줄여 계산복잡성을 낮췄다. Palaz et al. (2015)는 CNN 기반의 음성 인식 시스템에 대한 집중적인 분석을 수행했다. 그들은 원시 입력(raw input)과 음성(phone) 사이의 관계를 직접적으로 모델링하는 CNN의 능력을 입증했고, 강건한(robust) 자동 스피치 인식 시스템을 만들어냈다.
맥스풀링 전략은 문장에서 가치 있는 정보를 종종 잃어버린다. 다중 이벤트 모델링(multiple-event modeling)에서 이러한 정보 손실 문제를 극복하기 위해, Chen et al. (2015b)는 수정된 풀링 전략, 즉 dynamic multi-pooling CNN(DMCNN)을 제안했다.
전반적으로, CNN은 contextual window 내에 있는 의미적 단서를 추출하는 데 고도로 효율적이다. 그러나 CNN은 매우 많은 데이터를 필요로 한다. CNN 모델은 방대한 양의 데이터를 요구하는 다수의 학습 파라메터를 포함한다. CNN은 데이터가 부족할 때는 문제가 된다. CNN의 다른 이슈는 먼 거리의 문맥 정보를 모델링하기가 불가능하고 그들의 표현(repesentation)에서 시퀀셜한 순서를 보존할 수 없다는 것이다. 문장 모델링의 Kalchbrenner et al. (2014), 기계번역의 Tu et al. (2015)가 약간 다뤄지긴 했지만, 이 문제는 여전히 중요한 이슈로 남아있다. 따라서 Recursive NN과 같은 네트워크가 이런 학습에 적합하다.
    * 장점 : 데이터에서 feature 추출하여 패턴 파악에 용이, layer size 감소로 Parameter 갯수 효과적으로 축소, 노이즈 상쇄, 미세한 부분에서 일관적인 특징을 제공
    * 단점 : 장거리 의존성(long distance dependencies)를 모델링할 수 없다. 텍스트의 길이에 따라 성능이 달라진다. 방대한 데이터 필요, 다수의 학습 파라메터, 데이터가 적으면 성능이 낮음, 표현(representation)에서 시퀀셜한 순서를 보존할 수 없다. 

4. GRU(Gated Recurrent Unit)
2014년에 LSTM과 동일한 회로 메커니즘을 사용하지만 파라미터 수를 줄인 GRU가 제안되었다. GRU는 리셋 게이트와 업데이트 게이트로 구성되어 있으며, 두 게이트의 상호작용을 통해 학습한다. LSTM보다 적은 파라미터를 사용하기 때문에 이론적으로는 학습 속도가 조금 더 빠르고 완전한 학습에 필요한 데이터가 LSTM보다 적게 필요하다. 그러나 실제 성능으로는 특정 작업에서는 더 뛰어나기도 하고 뒤쳐지기도 한다.
GRU(Cho et al., 2014)라 불리는 RNN의 변형은 대부분의 task에서 LSTM과 경험적으로 유사한 성능을 내면서 구조적으로는 더 간단하다(본 블로그). GRU는 reset gate와 update gate의 두 개 gate로 구성되며 LSTM처럼 메모리를 보호한다. GRU는 LSTM보다 효율적인 RNN이 될 수 있다. GRU의 작동은 다음과 같다.

    * 장점 : LSTM 개선하여 더 단순화됨(Update gate(과거의 상태를 반영하는 Gate)와 Reset gate(현시점 정보와 과거시점 정보의 반영 여부를 결정)를 추가하여 과거의 정보를 어떻게 반영할 것인지 결정), 연산속도가 빠르며 메모리가 LSTM처럼 덮여 씌여질 가능성이 없음, LSTM보다 학습속도가 조금 더 빠르고 완전한 학습에 필요한 데이터가 적게 필요하다.
    * 단점 : 메모리와 결과값의 컨트롤이 불가능

5. LEAM(Label Embedding Attentive Model)
Label Embedding Attentive Model로서 label을 word와 똑같은 space에서 embedding한다. Text sequences와 labels의 compatibilit를 측정하는데 attention framework를 사용한다.  

    * 장점 : Interpretable, 적은 파라미터 수, 빠른 학습시간
    * 단점 : 

6. PTE(Predictive Text Embeddings , Tang et al 2015)

7. SWEM

8. Bi-BloSAN
“Bi-Directional Block Self Attention Network” (Bi-BloSAN) 이 현재 9개의 NLP 분야에서 SoTA를 기록하고 있네요.
주어진 시퀀스를 여러 개의 Block 으로 나누고 intra-block SAN으로 local context 를 모델링한 뒤, inter-block SAN으로 long-range dependency 를 모델링했습니다. 이로써 기존의 Self-Attention Network (SAN) 이 너무 메모리를 많이 쓰는 점을 개선했습니다.
    * 장점 : 성능이 좋음, 메모리 개선
    * 단점 : 데이터가 많이 필요, 파라미터 수가 많음, 학습시간이 오래 걸림
    
9. SVM(Support Vector Machine)(가장 기초적 classification, linear) TextFeatures
SVM은 각 클래스간 거리를 최대로 하는 경계선 또는 경계면(hyperplane)을 찾는다. 그리하여 새로운 데이터가 들어 왔을 때 일반화 오류를 최소화하는 모델이다. 이 때 각 클래스에서 데이터까지의 최소 거리를 마진(Margin), 그리고 경계선으로부터의 최소 거리인 데이터벡터를 서포트 벡터(Support Vector)라고 한다. 
    * 장점 : 해석 용이, 적은 Data에서도 적절한 결과가 나온다. 인공 신경망에도 크게 뒤지지 않는 성능을 낸다.
    * 단점 : 주로 단어의 빈도수를 feature로 사용하였기 때문에 해당 단어가 그 문장, 혹은 문단에서 어떤 의미로 쓰였는지 알기 힘들었다. 

10. HAN(Hierachical Attention Network) HN-ATT
attention mechanism-기존의 인코더-디코더 프레임워크가 직면한 하나의 잠재적인 문제는 인코더가 때로는 해당 작업과 완전히 관련되지 않은 정보까지도 인코딩해야 한다는 사실이다. 입력값이 길거나 정보가 아주 많은 경우, 그리고 선택적인 인코딩이 불가능할 경우 문제가 발생한다.
예를 들면, 문서 요약 작업은 입력값은 오리지날 텍스트이고 출력은 축약된 버전으로 하는 시퀀스 간(seqeunce-to-sequence) 학습 문제로 풀 수 있다. 길이가 매우 길 수도 있는 텍스트의 모든 정보를 고정 크기의 벡터로 인코딩하는 것은 직관적으로 기대하기 어렵다. 기계 번역에서도 비슷한 문제가 보고되었다(Bahdanau et al., 2014).
반면에, 텍스트 요약과 기계 번역 같은 작업에서 입력 텍스트와 출력 텍스트 사이에 일정한 정렬(alignment)이 존재한다. 요약이나 번역에서 각 토큰 생성 단계는 입력 텍스트의 특정 부분과 매우 관련이 있다.
어텐션 매커니즘은 디코더가 입력 시퀀스를 다시 참조할 수 있게 하여 위의 문제를 완화하려고 시도한다. 디코더는 마지막 히든 스테이트와 생성된 토큰에 더하여 ‘context’ 벡터에 대해 조건부화된다.
Bahdanau et al. (2014)는 기계 번역에 어텐션 매커니즘을 처음으로 적용했다. 어텐션 매커니즘은 특히 긴 시퀀스에 대해 모델의 성능을 향상시킨다. 그들의 연구에서, 입력된 히든 스테이트 시퀀스에 대한 어텐션 시그널은 디코더의 마지막 계층에 의해 다층 퍼셉트론으로 결정된다. 어텐션 시그널을 시각화하면 소스와 타겟 랭귀지 간의 명확한 정렬(alignment)를 보여줄 수 있다(그림14).

Hierachical Attention Network는 계층적 Attention Mechanism을 사용한다. 이는 문서의 계층적 구조를 반영한다. 이 Network에선 sentence와 word level의 두 attention mechanism을 사용한다.

    * 장점 : 문서의 계층적 구조 반영

11. BoW TFIDF, BoW 방법을 이용한 Naive Bayesian Classifier
    * 장점 : 
    * 단점 : 주로 단어의 빈도수를 feature로 사용하였기 때문에 해당 단어가 그 문장, 혹은 문단에서 어떤 의미로 쓰였는지 알기 힘들었다. 

12. Decision Tree

13. N-gram
    * 장점 : 단어의 의미적 문맥적 정보를 파악, 모든 문서 속 단어들의 의미적, 문맥적인 정보를 완벽하게 파악하지 않아도 적절한 성능이 나옴
    * 단점 : 단순히 여러 단어를 보는 것만으로는 텍스트의 모든 의미 파악하는데 한계 존재, N 값이 커질수록 계산량이 급격히 늘어나는 단점

14. Naive Bayes Classifier
각 사건들이 서로 독립이라는 가정을 한 후, Bayes's theorem을 이용하여 확률을 계산, 분류하는 모델이다. 따라서 두 확률의 결합 확률(Joint Probability)을 두 확률의 곱으로 표현해버리지만, 상당히 강력한 성능을 보이고 있어서 널리 사용된다. Naive Bayesian Classifier는 feature들간의 조건부독립 성질을 이용하는 반면, Multinomial Naive Bayesian Classifier는 feature들이 다항 분표(multinomial distribution)를 따른다는 정보를 활용한다.
    * 장점 : 간단
    * 단점 : 독립이 아닐 수 있는 사건들을 독립으로 가정하므로 한계 존재

15. Recursive Neural Networks
Recurrent Neural Network는 시퀀스(순차적인 데이터) 모델링에 강점을 지닌 기법이다. 그러나 자연언어는 단어와 단어가 계층적인 방식으로 구(phrase)로 결합되는 재귀적인(recursive) 구조를 나타낸다. 이러한 구조는 문장 구성성분 분석 트리(constituency parsing tree)로 표현될 수 있다. 이 때문에 문장의 문법적 구조 해석을 보다 용이하게 하기 위해 트리 구조 모델이 사용되었다(Tai et al., 2015). 특히 Recursive Neural Network에서 각 노드는 자식 노드의 표현(representation)에 의해 결정된다(본 블로그).
Socher et al. (2013)은 구문(pharase), 문장 수준 감성 예측에 이 모델을 적용했다(본 블로그). 저자는 이 연구에서 그림 17과 같이 파싱 트리의 모든 노드(단어)에 대해 감성 스코어를 시각화했다. 여기에선 전체 문장의 감성에 큰 영향을 미치는 ‘not’ 또는 ‘but’ 같은 단어에 대한 모델의 민감도가 나타난다.
LSTM은 Tai et al. (2015)가 제안한 트리 구조에도 적용되었다(본 블로그). 그래디언트 배니싱 문제(Gradient Vanishing Problem)를 피하기 위해서다. 이 모델은 감성 분석(Sentiment analysis)과 문장 관련성 테스트(sentence relatedness test)에서 linear LSTM 모델보다 개선됐다.

16. 로지스틱 회귀(Logistic Regression)
바이너리 값을 예측할 때 (예/아니오, 스팸/햄, 수락/거절 등)
    * 장점 : 간단한 방법이지만 예측의 신뢰도를 평가하는 데 사용할 수 있는 가능성을 계산해낼 수 있음
    * 단점 : 선형관계에 있다고 가정해야함.(선형회귀와 동일)
    
17. CART(Classification And Regression Tree)
카테고리 분류에 사용(별점평가 1-5점, 사기/팔기/홀딩 등)
    * 장점 : 선형관계에 있지 않은 데이터를 다룰 수 있음, 설명과 해석이 쉬움
    * 단점 : 데이터가 충분히 커야 함
    
18. Random Forest
CART와 동리
    * 장점 : 정확도가 CART보다 나음
    * 단점 : CART처럼 명확하게 설명하기 어려움


## 1. 논문 : Hierarchical Attention Networks for Document Classification
https://www.cs.cmu.edu/~hovy/papers/16HLT-hierarchical-attention-networks.pdf

## 2. 논문 : 윤킴 Convolutional Neural Networks for Sentence Classification
https://arxiv.org/abs/1408.5882

## 3. 논문 : 순환 신경망 기반 대용량 텍스트 데이터 분류 기술
https://pdfs.semanticscholar.org/d0e4/aebbe0dcb6a014ecbd70562878e22bb888b5.pdf

문서 분류 문제는 오랜 기간 동안 자연어 처리 분야에서 연구되어 왔다. 우리는 기존 컨볼루션 신경망을
이용했던 연구에서 더 나아가, 순환 신경망에 기반을 둔 문서 분류를 수행하였다. 순환 신경망에서는 가장
성능이 좋다고 알려져 있는 장기-단기 기억 (Long-Short Term Memory; LSTM) 신경망과 회로형 순환 유
닛(Gated Recurrent Units; GRU)을 활용하였다. 실험 결과, 분류 정확도는 Multinomial Naive Bayesian
Classifier, SVM, LSTM, CNN, GRU의 순서로 나타났다. 따라서 텍스트 문서 분류 문제는 시퀀스를 고려하
는 것 보다는 문서의 feature를 뽑아 분류하는 문제에 가깝다는 것을 추측할 수 있었다. 그리고 GRU가
LSTM보다 문서의 feature 추출에 더 적합하다는 것을 알 수 있었으며 적절한 feature와 시퀀스 정보를 함
께 활용할 때 가장 성능이 잘 나온다는 것을 확인할 수 있었다.

과거의 연구 방향이자, 지금도 뛰어난 성능으로 많이 사용되고 있는 Bag-of-Words[3] (BoW) 방법을 이용한 Naive Bayesian Classifier[4], 서포트 벡터 머신(Support Vector Machine; SVM)[5] 등은 주로 단어의 빈도수를 feature로 사용하였기 때문에 해당 단어가 그 문장, 혹은 문단에서 어떤 의미로 쓰였는지 알기 힘들었다. 이를 극복하려는 시도로 한 번에 여러 단어를 보는 N-gram 방법을 통해 단어의 의미적, 문맥적 정보를 파악하려 했으나, 단순히 여러 단어를 보는 것만으로는 텍스트의 모든 의미를 파악하는데 한계가 있었다. 또한, N 값이 커질수록 계산 량이 급격히 늘어나는 단점도 있었다. 그러나 모든 문서 속 단어들의 의미적, 문맥적인 정보를 완벽하게 파악하지 않아도 적절한 성능이 나왔기 때문에 여전히 BoW 방법은 널리 사용되고 있다. 
이를 극복하려는 시도로 한 번에 여러 단어를 보는 N-gram 방법을 통해 단어의 의미적, 문맥적 정보를 파악하려 했으나, 단순히 여러 단어를 보는 것만으로는 텍스트의 모든 의미를 파악하는데 한계가 있었다. 또한, N 값이 커질수록 계산 량이 급격히 늘어나는 단점도 있었다. 그러나 모든 문서 속 단어들의 의미적, 문맥적인 정보를 완벽하게 파악하지 않아도 적절한 성능이 나왔기 때문에 여전히 BoW 방법은 널리 사용되고 있다.

3. 실 험
 데이터 전처리와 Naive Bayesian Classifier, SVM은 Python2.7, CNN과 RNN은 Torch7의 nn, rnn패키지[16]를 이용하여 구현하였다.
 
 3.1 데이터
 대분류로는 9개, 소분류로는 68개 분야에 분포되어 있는 인터넷에서 수집한 623,303개의 뉴스 데이터를 준비하였으며 학습 데이터, 검증 데이터, 테스트 데이터는 각각 70%, 15%, 15%의 비율로 나누었다. 데이터의 분야별 분포는 표 1과 같다. 
 
3.2 설 계
 비교모델로 TF-IDF (Term Frequency-Inverse Document Frequency)[17]를 사용한 Multinomial Naive Bayesian classifier와 SVM을 사용하였다. CNN의 경우, 먼저 각 문서들을 형태소 분석기로 나눈 후 빈도수 기준 상위 n개의 단어로 lookup 테이블을 만든다. 그 다음 컨볼루션 커널을 슬라이드 하여 적절한 파라미터를 학습한다. 이때 커널의 가로와 세로 크기는 각각 단어 임베딩 크기, N-gram과 같이 동시에 학습하는 단어 크기와 같다. 활성 함수 (activation function)으로는 ReLU[18]를 사용했으며, logSoftMax를 이용하여 각 문서들이 특정 주제에 속할 확률을 출력하였다. 그 중 가장 높은 값을 가진 카테고리를 정답으로 예측하였다. RNN의 경우, 마찬가지로 lookup 테이블을 생성하고, 테이블을 단어 벡터 단위로 쪼개어 순환 신경망의 입력으로 넣는다. lookup 테이블을 업데이트하면서 계속 해서 학습, 최종 은닉 층을 출력한다. CNN과 동일하게 ReLU와 logSoftMax를 이용하여 예측을 수행하였다.

3.3 실험 결과
각 모델 정확도는 표 2, 표 3과 같다.
Model Accuracy (Top-1,3,5)
MNB 0.641 0.911 0.958
SVM 0.795 0.960 0.991
CNN 0.856 0.986 0.997
LSTM 0.811 0.965 0.994
GRU 0.886 0.992 0.999
표 2 모델 별 대주제 실험 정확도

Model Accuracy (Top-1,3,5)
MNB 0.399 0.679 0.794
SVM 0.614 0.851 0.906
CNN 0.700 0.920 0.962
LSTM 0.670 0.895 0.942
GRU 0.725 0.937 0.971
표 3 모델 별 소주제 실험 정확도

 실험 결과, GRU가 가장 뛰어난 성능을 보였다. LSTM은 SVM과 CNN 사이의 성능을 보였다.
 
4. 결 론

 본 논문은 인터넷에서 수집한 텍스트 문서를 여러 알고리즘을 이용하여 정해진 카테고리에 맞게 분류하는 내용을 담고 있다. 총 623,303개의 문서를 대분류 9개, 소분류 68개에 분류하였을 때, 분류 정확도는 Multinomial Naive Bayesian Classifier, SVM, LSTM, CNN, GRU의 순서로 나타났다. 이 결과는 다음과 같이 해석할 수 있다:
 
(1) LSTM보다 CNN의 성능이 더 뛰어난 것으로 보아 문서 분류 문제는 전체 글의 시퀀스를 학습하는 것 보다는 글의 feature를 통해 학습하는 것이 더 올바른 문제 접근법이라고 생각할 수 있다. 따라서, (2) LSTM과 GRU의 성능을 비교했을 때, LSTM에 비해 GRU가 feature를 더 잘 추출했다고 볼 수 있다. 마지막으로, (3) GRU가 CNN보다 성능이 더 좋은 것으로 보아, 문서 분류 문제는 feature와 시퀀스 두 가지를 모두 적절히 고려할 때 성능이 가장 잘 나온다는 것을 확인할 수 있었다. 추후 연구에서는 LSTM과 GRU에서 추출된 feature와 embedding 결과를 비교, 분석하여 어떤 차이가 GRU의 성능을 더 뛰어나게 만들었는지 확인해보고자 한다.

## 4. 논문 : Recent Trends in Deep Learning Based Natural Language Processing
https://arxiv.org/pdf/1708.02709.pdf
딥러닝 기반 자연어처리 연구트렌드 정리한 논문
한국어 번역 : ratsgo's blog : https://ratsgo.github.io/natural%20language%20processing/2017/08/16/deepNLP/

딥러닝 기법은 데이터의 계층적인 표현(hiarchical representation)을 학습하는 다층 레이어(multiple processing layer)를 사용한다. 
지난 수십년간 NLP 문제를 풀기 위한 머신러닝의 접근은 고차원이면서 sparse한 피처(feature)를 학습한 ‘얕은 모델(shallow models, 예: SVM/로지스틱 회귀)’에 기반한 것이다. 최근 수 년간 dense vector representation에 기반한 뉴럴네트워크가 다양한 NLP task에서 우수한 성능을 보여줬다. 이러한 트렌드는 워드 임베딩(Milokov et al., 2010, 2013a)과 딥러닝 기법(Socher et al., 2013)의 성공에 힘입은 것이다. 딥러닝은 자동화된 피처 추출 및 표현(multi-level automatic feature representation learning)을 가능하게 한다. 그러나 전통적인 머신러닝에 기반한 NLP 시스템은 사람이 직접 추출한(hand-crafted) 피처에 강하게 의존한다. 이러한 피처들은 추출하는 데 시간이 많이 소요되고 많은 경우 불완전하다.  

## 5. 논문 : A Convolutional Neural Network for Modelling Sentences
http://www.aclweb.org/anthology/P14-1062
Kim(2014)는 감성, 주관성, 질문유형 분류를 포함한 다양한 문장 분류 문제에 이미 기술한 아키텍처를 실험했다. 이 연구는 간단하지만 효율적인 네트워크여서 아마추어 연구자들에 의해 빠르게 적용되었다. 특정 과업 학습 후 랜덤하게 초기화된 콘볼루션 필터는 목적하는 태스크에 유용한 특정한 n-gram 피처 감지기(detector)가 됐다. 그러나 Kim(2014)의 아키텍쳐는 장거리 의존성(long distance dependencies)을 모델링할 수 없는 등 많은 단점을 지닌다. 이러한 이슈는 Kalchbrenner et al.(2014)에 의해 효과적으로 처리된다. 이들은 문장의 의미를 모델링하기 위한 dynamic convolutional neural network(DCNN)을 제안했다. 이들은 dynamic k max pooling 전략을 제안했다. 이는 시퀀스 p가 주어졌을 때 가장 활동적인(active) k개의 피처를 뽑는 방법이다. 선택은 피처의 순서를 보존하지만, 특정 위치에는 민감하지 않다. DCNN의 서브그래프 dynamic k max pooling을 사용하면 상위 계층의 작은 너비의 필터가 입력문장에서 관계된 구문을 멀리 떨어뜨릴 수 있다. 
Kalchbrenner et al.(2014)는 문장 모델을 만들기 위해 TDNN의 개념을 기반으로 dynamic k max pooling 전략을 추가했다. 둘의 조합은 작은 폭의 필터가 입력문장의 긴 범위를 커버할 수 있게 한다. 그림8에서 상위의 피처는 집중적이고 짧거나, 전역적이고 입력문장처럼 길 수도 있는 매우 가변적인 범위를 가진다. 이들은 감성 분류, 질의 유형 분류를 포함한 다양한 task에 이 네트워크를 적용했고, 의미있는 결과를 얻었다. 요컨대 이 연구는 문맥적 의미를 모델링하는 데 있어 개별 필터의 범위(range)에 대해 언급했고, 필터의 도달 범위를 확장하는 방법론을 제안했다.


## 선형성 모델
선형 분류 알고리즘은 클래스를 직선(또는 고차원의 아날로그)으로 구분할 수 있다고 가정, linear regression, SVM
데이터가 직선을 따르는 경향이 있다고 가정함. 이러한 가정은 일부 문제에 대해서는 그다지 나쁘지 않지만 어떤 면에서는 정확도가 떨어질 수 있음(선형으로는 절대 분류를 못 하는 데이터가 있다), 너무 단순하게 표현함
장점으로는 가장 먼저 시도해보기 좋을만큼 간단하고 학습 시간이 빠른 경향이 있다.
선형성 모델은 다중 클래스 분류에 매우 취약, 2클래스 분류에 적절, text classification에는 적합하지 못 함

## 모델이 얼마나 좋으냐 평가할 때 사용할 것
* 매개 변수 수
알고리즘의 동작에 영향을 주는 숫자, 알고리즘의 학습 시간 및 정확도에 크게 영향을 줌, 일반적으로 매개 변수가 많은 알고리즘의 경우 적절한 조합을 찾기 위해 대부분 시행착오와 오류를 겪어야 함, 
매개변수가 많을 때의 장점으로는 알고리즘의 유연성이 향상된다는 것, 정확도가 높아질 수 있다. 적절한 수의 매개변수를 선택하는 것이 중요

임베딩 추가
1. fast text
2. 엘리스 오 subword



