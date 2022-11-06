---
layout: mathpost
title:  "메타프로그래밍: 극한"
date:   2022-11-07 20:45:00 +0900
published: false
tags: category-theory limit
---

## 뿔
### 직관

우리는 카테고리 $$C$$와 $$D$$사이의 관계를 $$C$$에서 점 두 개, $$D$$에서 점 두 개를 골라 사각형의 관계를 정의하는 함자$$F:C \rightarrow $$의 정의를 통해 살펴보았다. 마치 컴퓨터 디자인에서는 사각형을 사용하지만 컴퓨터 렌더링에서는 삼각형을 사용하듯이, 우리의 정의를 삼각형의 관계로 바꾸어 보려고 한다. 이를 통해, 카테고리 $$C$$가 함자 $$F$$를 통해 $$D$$에서 어떻게 표현되는가 뿐만 아니라, $$C$$ 전체를 $$F$$를 통해 $$D$$의 한 점으로 표현하고자 한다.

뿔(cone)의 정의에는 두 개의 카테고리가 등장한다. 첫 번째 카테고리는 지금까지 해왔듯 일반적인 카테고리이고, 두 번째 카테고리는 대개 유한 개, 많아야 집합 개의 점을 가지는 쬐끄만한 카테고리이다.

들어가기 전에, 영어로는 cone이라 원뿔이라고 번역하고 싶으나, [여러](https://dl1.cuni.cz/pluginfile.php/1387491/mod_resource/content/1/Category%20Theory%20by%20Steve%20Awodey.pdf) [교재에서](https://bartoszmilewski.com/2015/04/15/\limits-and-co\limits/) 이미 이를 설명하기 위해 여러 면의 각뿔(many-sided pyramid)이라고 고쳐 부르고 있다. 따라서 일단 머릿속에서는 원뿔이 아닌 각뿔을 상상하기 바란다.

### 정의

카테고리 $$I$$와 $$C$$, 그리고 그 사이의 함자 $$F: I\rightarrow C$$ 주어졌다고 하자. 또한 $$I$$의 점 $$x, y$$ 사이의 화살표 $$f$$가 있다고 하자. $$F$$로의 뿔$$(a, \alpha$$)를 아래와 같이 정의한다.

### 구성요소

1. $$C$$의 한 점 $$c$$. "각뿔의 꼭지점"(apex) 이라고 부른다.
2. $$I$$의 각 점 $$x$$에 대응되는 화살표들 $$\alpha_x: c \rightarrow F(x)$$의 모임 $$\alpha$$. 각뿔의 변(edge)이라고 부른다.

### 만족해야 할 조건

1. $$I$$의 화살표 $$f$$에 대해, $$F(f)\circ \alpha_x = \alpha_y$$이다. 각뿔의 면(face)이라고 부른다.

### 명칭
- $$I$$를 "각뿔의 밑면" 이라고 부른다.

### 성질

만족해야 할 조건은 자연변환의 정의와 매우 비슷하다.

가장 자명한 뿔은 함자 화살표의 모임이 $$\alpha_i=(i\mapsto 1_c)$$일 때일 것이다. 모든 점과 화살표를 한 점과 $$1$$로 보내는 함자 $$\Delta_c: I\rightarrow C$$를 생각해 보자. 즉 $$\Delta_c(i)=c$$, $$\Delta_c(f)=1_c$$이다. 그러면 뿔을 자연변환 $$\alpha: \Delta_c \Rightarrow F$$로 identify할 수 있다.

### 뿔의 카테고리
함자 $$F: I\rightarrow C$$가 주어졌을 때, 뿔의 카테고리는 다음으로 정의된다.

1. 점은 뿔 $$(c, \alpha)$$이다.
2. $$(c, \alpha)$$에서 $$(c', \alpha')$$로의 화살표는 자연변환 $$\Delta(c') \Rightarrow \Delta(c)$$이다.
3. 합성은 자연변환의 합성으로 정의된다.
4. 뿔 $$(c, \alpha)$$의 항등 화살표는 $$(i\mapsto 1_c)$$로 정의된다.

뿔의 카테고리를 $$\Delta \downarrow F$$라고 표기한다.

## 극한

### 직관

"가장 단순한 뿔"을 찾기 위해서, 뿔의 카테고리에서 "가장 단순한 점"을 찾으면 된다. 카테고리에서 가능한 가장 단순한 점은 $$C(x, x) = {1_x}$$인 경우이다. 뿔의 카테고리에서 이러한 뿔을 **universal cone**이라고 부른다.

조금 더 풀어서 생각해보면, universal cone은 $(c, \alpha)$$은 다른 모든 뿔 $$(c', \alpha')$$ 에 대해 $$C(c, c')$$가 유일하다. universal cone의 apex를 극한이라고 정의한다.

### 정의

카테고리 $$I$$와 $$C$$, 그리고 그 사이의 함자 $$F: I^{op}\rightarrow C$$ 주어졌다고 하자.
#### 정의 1
어떤 뿔 $$(c, \alpha)$$가 다른 모든 뿔 $$(c', \alpha')$$에 대해 $$ \alpha(i) \circ f = \alpha'(i)$$를 만족하는 $$C$$의 화살표 $$f:c'\rightarrow c$$가 유일하게 존재할 때, $$c$$를 함자 $$F$$의 극한이라고 부른다.

#### 정의 2
어떤 뿔 $$(c, \alpha)$$가 $$(\Delta \downarrow F)((c,\alpha), (c, \alpha)) = {1_c}$$를 만족하면, 이 뿔의 점 $$c$$를 $$F$$의 극한이라고 한다.

함자 $$F: I\rightarrow C$$의 극한을 $$\lim_{i\in I} F(i)$$ 혹은 $$\lim_I F$$ 혹은 $$\lim F$$라고 표기한다.

### 예시

#### Product

### 성질

#### 극한과 hom-functor의 교환

카테고리 $$I$$와 $$C$$, 그리고 그 사이의 함자 $$F: I^{op}\rightarrow C$$ 주어졌다고 하자. $$\lim F$$가 존재하면, $$\lim_{i\in I} C(c, F(i)) = C(c, \lim_{i\in I} F)$$이다.

#### 극한 사이의 교환

카테고리 $$I$$와 $$C$$, 그리고 그 사이의 함자 $$F: (I^{op} \times I'^{op})\rightarrow C$$ 주어졌다고 하자. $$\lim_I (\lim_{I'} F) = \lim_{I'} (\lim_I F) = \lim_{I\times I'} F$$이다 (존재하면).
