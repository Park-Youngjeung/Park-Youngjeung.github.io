---
layout: post
title:  "Simulation Analysis on the Thermal Stress Field of the Cement Burner"
date:   2017-01-22 10:15:00
---

Luo Huixin, Chen Zheng, Wang Qin, Chang Qinming, Li Yawei and Fang Young

Wuhan University of Science and Technology, Wuhan 430081, Hubei
Tongda Refractoriness Technology Co., LTD, Beijing 100000


## 요약(Abstract)

시멘트 버너의 실제 열응력 장(Thermal stress field)와 온도장(Thermal field)를 시뮬레이션하기 위하여 HYPERMESH를 이용해서 시멘트 버너의 열응력을 유한 요소 시뮬레이션으로 분석하였다.
시뮬레이션 결과를 바탕으로 본 논문은 시멘트 버너의 손상 원인을 제시하고 손상 형태를 추정한다. 이론 해석 및 실제 손상 형태를 손상 원인과 대비하여 시멘트 버너를 연구하기 위해 컴퓨터 지원 엔지니어링(Computer Aided Engineering) 유한 요소 분석을 사용하여 타당성 및 유효성을 확인하였다. 다양한 앵커 형태(U형, Y형, 웨이브형)로 시멘트 버너의 열 응력에 대한 연구가 수행되었다. 실험 결과에 기초한 초기 조건과 경계 조건이 모델에 적용되었다. 시멘트 버너가 정상적으로 작동 할 때 HYPERMESH로 각기 다른 앵커에 대해 시멘트 버너의 온도장과 열응력장을 시뮬레이션하였다. 그런 다음 최상의 앵커 형태를 결정하기 위하여 시뮬레이션에서 얻을 수있는 결과를 비교하고 분석하였다.


## 1. 개요(Forward)
시멘트 버너는 연료 연소, 회수 열교환, 화학 반응, 물질 운반 등에 주로 사용된다. 시멘트 버너에서 연료가 연소되면서 많은 에너지를 제공할 수 있으므로 매우 중요한 책임을 지고 있다[1]. 뛰어난 성능을 가진 버너만이 적절한 온도장(temperature field)을 얻기에 적절한 열을 제공하여 노(kiln) 시스템의 완전한 이용으로 고품질, 효율, 저비용, 장수명, 환경보호를 보증할 수 있다. 일반적으로 시멘트 버너의 수명은 항상 1에서 5개월이며 때로는 단지 몇 일만 사용되고 내화물 캐스타블의 탈락으로 보수 및 교체로 인하여 생산 라인의 작업을 중단할 수도 있다[3]. 그래서 손상 원인을 분석하고 해결책을 찾는 것이 중요하다. 게다가 앵커 피스의 분포와 모양은 시멘트 버너의 사용 수명에 중요한 영향을 미친다[4]. 버너에 사용되는 앵커 피스의 중요성에 대해, 이 문헌은 CAE 방법을 사용하였으며, 시멘트 버너가 사용될 때 버너 앵커의 다른 형태들에 대한 온도장(thermal field)과 열응력장(thermal stress field)를 시뮬레이션하였다[5]. 실제 사용되는 시멘트 버너 구조 설계에 대해 시뮬레이션 분석 결과에 따라, 우리는 버너의 사용 상태를 개선하기 위한 이론적 지침를 제공한다.



## 2. 시멘트 버너의 개요(The Brief Introduction of the Cement Burner)

### 2.1. 시멘트 버너 구조의 개요(The Brief Introduction of the Structure of the Cement Burner)

  현재 시멘트 버너는 캐스타블, 앵커와 버너 튜브 세 부분으로 구성된다. 앵커는 붉은 색으로 나타내었다.
캐스타블은 투명한 원통으로, 버너 튜브를 푸른색 원통으로 묘사되어 있다(Fig.1).

### 2.2. 시멘트 버너의 손상 형태(The Damage Form of the Cement Burner)

  중국에서 시멘트 버너의 수명은 매우 짧아 일반적으로 단지 1~5개월이다. 드물게 몇 일 사용후 캐스타블 탈락으로 교체 및 보수 필요로 사용 종료되어 생산에 차질을 주기도 한다. 시멘트 버너 손상은 주로 캐스타블 손상, 캐스타블 소실과 버너 구조적 손상을 포함한 버너 내부 조건에 의한 손상으로 야기된다. 실제 특정 형태의 손상을 Fig. 2에서 Fig. 4에 나타내었다.

### 2.3. 시멘트 버너 손상 원인(The Reasions of the Cement Burner's Damange)

시멘트 버너의 손상 원인은 주로 다음과 같습니다.
1) 캐스터 블의 재질, 두께 및 품질;
2) 앵커 부품의 재료, 용접 방법, 형상 및 배치;
3) 화학적 부식, 마모 및 열충격.

### 2.4 CAE를 사용한 시멘트 버너 손상 원인의 시뮬레이션 분석의 방법과 절차(The Method and Procedure of the Simulation Analysis of the Damage Reason of the Cement Burner using CAE)

1) 먼저 시멘트 버너의 3 차원 CAD 모델을 Solidworks로 완성한 다음 분석 전처리를 위해 HYPERMESH로 옮겼습니다. 버너의 모든 부분은 육면체 요소(hexahedral elements)로 메쉬했으며, 접촉 요소는 서로 다른 부분 사이의 접촉면에 설정하였다.
2) Castable 의 물리적 특수 변수를 얻었고, 초기 및 경계 조건은 생산 라인에서 측정된 데이터뿐만 아니라 관련 문헌에 따라 설정하였다. 성능 변수와 열 경계 조건은 3D 모델에 적용되므로 열 해석 CAE 모델을 얻을 수 있다. CAE 모델을 ANSYS로 가져 와서 킬른에서 시멘트 버너의 열 공정을 분석하고 열 시뮬레이션 분석의 관련 결과를 얻을 수 있었다.
3) 마지막 단계에서 계산된 온도 분포는 응력 해석을 위한 열장 부하(Thermal field load)로 사용되었다. 이 부하은 ANSYS의 LDREAD 명령에 의해 자동으로 응력 해석 모델에 적용되었다. 따라서 열응력장(Thermal stress field)을 계산하고 분석 할 수 있었다.
4) 시멘트 버너 전체의 열 응력을 시뮬레이션 분석 후, 버너의 앵커를 분석이 필요하다. 최적 형태의 앵커는 온도 분포 및 응력장에 대한 여러 유형의 앵커 효과를 비교하여 얻을 수 있다.



## 3. 시멘트 버너의 시뮬레이션 결과 분석(The Simulation Results Analysis of the Cement Burner)


### 3.1 유한요소 CAE 모델의 설립(The Establishment of Finite Element CAE Model)


우리는 베이징 Tongda 내화물 기술 유한 책임 회사가 제공하는 시멘트 버너의 2 차원 도면에 따라 유한 요소 모델을 설정합니다. 이 논문은 주로 CAE 방법에 의한 시멘트 버너의 손상 원인에 초점을 맞추기 때문에 가장 쉽게 손상되고 가마에 삽입되는 시멘트 버너의 끝 부분을 고려한다.
버너 끝 부분의 1/4 부분은 축 대칭 때문에 열 응력 분석을 위해 모델링되고 시뮬레이션됩니다. 유한 요소 모델을 수립하는 과정에서 모든 구조물은 6 면체 요소를 사용하여 메쉬 생성을하고, 버너, 캐스터 블 및 앵커의 강관 중 접촉부에 접촉 요소를 설정했습니다.
확립 된 시멘트 버너의 CAE 모델은 Fig. 5-7 :


### 3.2 온도장(Temperautre Field)의 시뮬레이션 분석


버너의 전체 시멘트 버너, 캐스터 블, 앵커 및 강관의 온도 장을 Fig. 8 ~ 10.
Fig. 8 및 그림. 도 9로부터 알 수 있듯이, 강관 내면의 저온에서 주조 재의 내면의 고온까지 균일하게 온도가 변화하는 것을 관찰 할 수있다 [6]. 더욱이, 캐스터 블의 외부 표면 온도는 왼쪽에서 오른쪽으로 (캐스터 블 엔드) 증가하는 경향이있다. 무화과. 도 10은 기저부에서 상부로 앵커를 따라 온도가 상승하는 것을 도시한다. 그리고이 온도는 976 ° C까지 올라갈 수 있습니다.


## 3.3 열응력장(Thermal Stress Field)의 시뮬레이션 분석의 결과

### 3.3.1 모델의 변위 분포 구름 차트(Displacement Distribution Cloud Charts of the Model)


무화과. 11은 전체 버너의 변위 분포를 나타냅니다.
주조 가능 단부에서의 변위 변형이 상대적으로 더 커지며, 주조 가능 파이프와 강철 파이프 사이의 계면에서 캐스터 블의 외부 표면으로 증가한다.
Fig. 도 12에 도시 된 바와 같이, 앵커가 펼쳐지는 경향이 있고 앵커 중 일부가 팽창하여 직경이 커지는 경향이 있음을 알기는 어렵지 않다.


### 3.3.2 모델들의 응력 분포 구름 차트(The stress Distribution Cloud Charts of the Models)

무화과. 도 13의 도 15는 버너 내의 캐스터 블, 앵커 및 강관의 응력 분포를 나타낸다. 위치 된 주조물에서 상대적으로 더 큰 응력이 Fig. 3에서와 같이 앵커 뿌리와의 연결부에있는 부분. 13.
이것은 앵커가 캐스터 블 [7]의 팽창 변형을 방해하기 때문이다. 이는 캐스터 블과 앵커 사이의 상호 작용이 앵커가 캐스터 블에 의해 의도적으로 늘어나 기 때문에 그림 1에 나타낸 버너의 강관에 용접 된 앵커의 뿌리 부분에 응력 집중을 유발하기 때문입니다. 14 [8]. 최대 응력은 1530 MPa까지 도달 할 수 있습니다. 더욱이, 앵커의 변형은 시멘트 버너에서 강관의 변형으로 이어져서 Fig. 15.


4. 앵커 형태에 따른 버너의 열응력 분석

4.1 열장(Thermal Field) 시뮬레이션의 분석 결과들

우리의 일상적인 제조에 널리 쓰이는 3 가지 앵커가 있습니다. 세 가지 유형 앵커는 U 유형 앵커, Y 유형 앵커 및 웨이브 유형 앵커입니다. 따라서이 백서는 작업 할 때 세 가지 유형의 앵커에 중점을 둡니다. 온도 구름은 Fig. 16.
무화과. 그림 16에서 보듯이 앵커의 온도 장과 버너의 파이프 이미지는 앵커의 종류에 따라 달라진다. 가장 높은 온도는 U와 파 앵커 시멘트 버너 용 파이프에 분포하며 Y 앵커의 가장 높은 온도는 앵커에있다 [9]. 또한 시멘트 버너가 전체적으로 고려 될 때 작동 온도는 Y가 가장 낮고 U가 가장 높습니다.

4.2 응력장(Stress Field) 시뮬레이션 분석 결과

그러나 실제 생산시, 시멘트 버너는 온도 장을 가질뿐만 아니라 응력 장 [10]을 가지고있다. 그래서 우리는 스트레스 분야를 고려할 것입니다. 그리고 그 응력장은 Fig. 17 ~ 19.
응력 등고선으로부터. 도 17 내지도 17을 참조한다. 19는 시멘트 버너가 전체적으로 고려 될 때 Y- 앵커 시멘트 버너가 가장 잘 수행되고 나머지 두 개는 더 나 빠진다는 것을 보여준다 [11]. 게다가 파이프에 휘말린 앵커의 뿌리에 가장 높은 스트레스가 들어간다는 것을 알 수 있습니다. 한마디로, 앵커의 모양은 구조 응력 분포에 큰 영향을 미칩니다. 시멘트 버너의 열 응력 해석을 바탕으로 표 1과 표 2와 같이 온도와 응력장을 구한다.



5. 결론

CAE 시뮬레이션 분석의 결과에 따르면 :
1) 시멘트 버너의 캐스터 블, 버너의 앵커링 부 및 강관이 사다리 분포가 모두 내부에서 외부로 증가한다는 온도 필드 분포도의 시뮬레이션 결과로부터 알 수 있습니다. 이 결과는 실제로 모든 부품의 온도 조건과 동일합니다.
2) 변위 변형 구름 그래프에 따르면, 캐스터 블이 근접한 끝단의 가장 바깥 쪽 층은 가장 큰 변위 변형을 가지며 앵커링 부분과의 접촉 부분의 응력은 상대적으로 높다. 이러한 종류의 응력과 변형은 최종적으로 끝단 근처에있는 외부 캐스터 블 (castable)로 이어질 수 있습니다. 이 시뮬레이션 결과는 기본적으로 실용 엔지니어링 응용 프로그램에서 버너의 캐스터 블 엔드의 창고 형태로 계산합니다.
3) 앵커링 부의 변위 변형과 응력의 분포에 따라 앵커링 부의 근원에 앵커링 부분을 전체적으로 끌어 올릴 수있는 응력이 집중되었다. 실용적인 손상 조건 (그림 2, 그림 4)과 비교할 때, 시뮬레이션 분석 결과는 앵커링 부분의 실제 손상 상태를 나타냅니다.
4) 비록 Fig. 도 16에 도시 된 바와 같이, 앵커의 응력은 다른 부품의 응력보다 크며, 이는 앵커의 파손이 주로 버너의 손상을 야기한다는 것을 의미한다. 따라서 다양한 앵커는 시멘트 버너의 수명에 큰 영향을 미칩니다.
5) 그림 16에 따르면, 최고 온도가 캐스터 블에 있고 가장 높은 응력이 앵커에 있음을 알 수 있습니다. 3 가지 유형의 시멘트 버너의 열 응력장을 분석 한 결과, U- 앵커 시멘트 버너가 가장 잘 수행된다는 결론을 얻을 수 있습니다.


참고 문헌

References
[1]. Bai Hong-Gong, Xu Kai-Feng, Reason for destruction of castable in coal burner and its treatment, Cement Engineering, Issue 8, 2006, pp. 16-17.
[2]. Zhao Xiao-Dong, Measure of improving the service life of refractory castables in burner, Cement Engineering, Issue 1, 2001.
[3]. Wang Zhi-Gang, Numerical simulation of temperature and stress field of ladle lining on the bottom, Energy for Metallurgical Industry, Issue 4, 2004, pp. 16-19.
[4]. Wei Rui-Yan, Mechanical property test on steel structure in condition of high temperature, Journal of Fujian College Architecture, March 2002, pp. 5-9.
[5] E. S. Chen, M. H. Frechette, Thermal and thermomechanical evaluation of high-strength insulation in steelmaking ladle, in Proceedings of the Conference on Steelmaking, 1996, pp. 457-463.
[6]. Yang Shi-Ming, Tao Wen-Quan, Heat transfer, Higher Education Press, Beijing, 1998.
[7]. Zhang Guo-Zhi, Hu Ren-Xi, Chen Ji-Gang, ANSYS10.0, Thermodynamic finite element analysis, Machinery Industry Press, Beijing, 2007.
[8]. Sun Ying, Zhang Mai-Cang, Dong Jian-Xing, Q235 The deformation characteristics of steel heat, Journal of Iron and Steel Research, Issue 5, 2006.
[9]. Shao Hong-Yan, Analysis of the stress field of structural temperature field and temperature, Master's degree thesis, Xian Northwestern Polytechnical University, 2001.
[10]. Jiang Xu-Lv, The development of process and burner coal technology for cement rotary klin, The New Century Cement, 5, 2002.
[11]. Li Zu-Xi, Improvement of coal injection pipe single channel, Cement Technology, 6, 1999.
