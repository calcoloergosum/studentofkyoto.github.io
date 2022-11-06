---
layout: mathpost
title:  "카테고리 이론에서의 극한 (번역)"
date:   2022-11-07 20:45:00 +0900
published: true
tags: category-theory limit
toc: true
---

원문: [LIMITS IN CATEGORY THEORY by SCOTT MESSICK](https://math.uchicago.edu/~may/VIGRE/VIGRE2007/REUPapers/FINALAPP/Messick.pdf)


---


# 카테고리 이론에서의 극한
{:.no_toc}

Scott Messick

2007년 8월 17일

초록. 나는 카테고리 이론에 대한 어떠한 지식도 가정하지 않을 것이며, 극한의 논의를 시작하기 위해 필요한 모든 개념을 설명할 것이다. 두 개의 중요한 정리로 끝마칠 것이다: 곱(product)과 동등자(equalizer)가 구비된 카테고리는 완전하다(complete)는 것과, 임의의 카테고리의 극한은 자연 변환을 이용해 홈셋(hom-set)의 극한으로 귀납된다는 것이다.

* Placeholder
{:toc}

## 1. 카테고리

카테고리 이론은 고도로 추상적으로, 그리고 수학적으로 수학의 구조를 다루는 방법론(scheme)이다. 카테고리 이론의 기본 요소는 카테고리이다.

**정의 1.1.** 카테고리는 세 요소로 구성된다.
1. 객체(object[^1])의 모임 $$Ob(\mathscr C)$$. $$C\in Ob(\mathscr C)$$ 대신, $$C\in \mathscr C$$로 쓰기도 한다.
2. 사상(morphism)의 모임 $$Ar(\mathscr C)$$과, 각 사상 $$f$$에 정의된 정의역(domain) 객체 $$\text{dom} f$$와 공역(codomain) 객체 $$\text{cod} f$$. 정의역이 $$A$$이고 공역이 $$B$$인 사상들의 집합을 $$\text{Hom}_{\mathscr C}(A, B)$$ 혹은 간단하게 $$\mathscr C (A, B)$$ 라고 쓰고, 사상집합(hom-set)이라고 부른다. 사상은 정의역에서 출발해 공역으로 끝나는 화살표로 볼 수 있다. 사실, 나는 "사상"이라는 단어와 "화살표"라는 단어를 같은 의미로 사용할 것이다. $$A$$와 $$B$$가 $$\mathscr C$$의 객체라는 것이 분명할 때, $$f\in \mathscr C (A, B)$$ 대신 $$f:A\rightarrow B$$라고 쓰기도 한다.
3. 합성 법칙; 즉 모든 사상집합의 쌍 $$\mathscr C(A, B)$$와 $$\mathscr C(B, C)$$에 대해, 이항 연산 $$\circ: \mathscr C(A, B) \times \mathscr C(B, C) \rightarrow \mathscr C(A, C)$$이다. 합성을 $$\circ(f, g)$$라고 쓰는 대신 $$g\circ f$$ 혹은 $$gf$$라고 쓴다. 합성은 다음 두 개의 공리를 만족하여야 한다.

  * 결합법칙(associativity); $$f\in \mathscr C(A, B)$$이고 $$g\in \mathscr C(B, C)$$이고 $$h\in \mathscr C(C, D)$$이면, $$h\circ(g\circ f)=(h\circ g)\circ f = h\circ g \circ f = hgf$$
  * 항등사상(identity): 모든 객체 $$C\in\mathscr C$$에 대해, 항등사상 $$1_C\in\mathscr C(C, C)$$가 존재해서, 모든 화살표 $$g\in \mathscr C(A, C)$$와 $$h \in \mathscr C(C, B)$$에 대해 $$1_C\circ g=g$$이고 $$h\circ 1_C = h$$이다.


카테고리의 예:

| Category | Objects | Morphisms |
|:---|:---|:---|
| $$\textbf{Set}$$ | 집합 | 함수 |
| $$\textbf{Top}$$ | 위상 공간 | 연속 사상 |
| $$\textbf{Grp}$$ | 군 | 군 준동형 사상 |
| 임의의 부분순서집합 | 집합의 원소 | 각 $$\le$$당 화살표 하나 |


카테고리의 전형적인 예는 집합의 카테고리인 $$\textbf{Set}$$이다. 객체의 모임은 모든 집합이고 화살표는 두 집합 사이의 모든 함수이며, 합성은 평범한 함수 합성이다. 위상 공간 및 군의 카테고리도 유사하다. 사실, 수학의 거의 모든 분야에 대해 이와 같이 카테고리들이 있다. 객체의 모임은 어떤 구조를 가지고 있으며, 화살표는 그 구조를 보존하는 사상이다.

함수의 합성에 관한 두 가지 공리는 다음과 같이 diagram으로 기술할 수도 있다. 모든 객체 C에 대해 다음 diagram이 모든 g, h에 대해 commute하도록 하는 항등 화살표 $$1_C$$가 존재한다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/1.png)

객체 $$A, B, C, D$$와 그 사이의 사상이 주어졌을 때, 다음의 diagram은 항상 commute한다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/2.png)

Diagram이 commute한다는 것은, 두 점 사이의 어떤 경로를 따라 합성해도 그 결과가 같다는 것이다. 이 diagram은 카테고리 이론에서의 개념을 표현하는 방법의 예시이기도 한데, 객체를 그래프의 점으로, 사상을 그 사이의 화살표로 쓴다.

다음의 개념은 중요하다.

**정의 1.2.** 사상 $$f: A\rightarrow B$$는, 어떤 사상 $$g: B\rightarrow A$$가 존재해서 $$f\circ g=1_B$$이고 $$g\circ f=1_A$$이면, 동형 사상(isomorphism)이라고 부른다. 이 때 $$A, B$$가 동형(isomorphic)이라고 한다.

거칠게 말하면, 동형인 점들은 카테고리에서 "같다"고 본다. 왜냐하면 한 점에서의/점으로의 화살표는 동형 사상을 통해 다른 점에서의/점으로의 화살표로 유일하게 대응되기 때문이다. 그러므로 카테고리의 구조의 관점에서 그 두 점은 구별할 수 없다. 예를 들어, 집합 사이의 함수만을 생각한다면, 동일한 기수의 두 집합은 $$\textbf{Set}$$에서 동형이다. 전단사 사상의 일반화도 가능하지만 현재의 논의에서는 불필요하다.

## 2. 함자와 자연변환

카테고리는 부분적으로 수학적인 객체의 개념은 두 객체 사이의 사상의 개념과 함께 제공되어야 한다는 아이디어를 구현한다. 집합에는 함수가, 군에는 동형사상이, 위상 공간에는 연속 사상이 따라오는 등이다. 마찬가지로, 카테고리에는 함자(functor)가 따라온다.

**정의 2.1.** 함자 $$F: C\rightarrow D$$는 각 객체 $$C \in \mathscr C$$를 객체 $$F(C) \in \mathscr D$$으로, 그리고 각 화살표 $$f\in \mathscr C(C_1, C_2)$$에 대해 $$F(f)\in \mathscr D(F(C_1), F(C_2))$$로 연관짓는 사상으로, 합성과 항등사상을 다음과 같이 보존한다:
- 모든 객체 $$C\in \mathscr C$$에 대해, $$F(1_C) = 1_{F(C)}$$이다.
- $$\mathscr C$$의 화살표 $$h, g, f$$가 $$h=g\circ f$$일 때, $$F(h)=F(g)\circ F(f)$$이다.

괄호를 생략하여 $$C\mapsto FC$$와 $$f\mapsto Ff$$로 쓰기도 한다.
함자의 수많은 예가 있겠다. $$\textbf{Grp}$$, $$\textbf{Top}$$에서 $$\textbf{Set}$$으로의 forgetful 함자는 각 객체를 구조를 정의하기 전의 집합(underlying set)으로 보내고, 자유 함자(free functor)는 그 반대이다. 예를 들어, 각 집합에 자명한 위상을 주는 등이다. 작은 카테고리를 공역의 diagram으로써 고르는 함자 (나중에 중요하게 다룬다) 등도 있다. 중요한 함자 중 하나는 사상 집합이다. $$\mathscr C$$가 카테고리이고 $$C$$가 객체라고 할 때, $$\text{Hom}_{\mathscr C}(C, -)$$는 함자 $$H: C\rightarrow \textbf{Set}$$가 된다. 이 함자는 화살표를 왼쪽 합성으로 보낸다. 즉 $$f: A\rightarrow B$$가 주어지면 $$Hf: \text{Hom}_{\mathscr C}(C, A)\rightarrow \text{Hom}_{\mathscr C} (C, B)$$는 $$(Hf)(g) = f\circ g$$로 정의된다.

나아가서, 자연변환은 함자의 화살표이다. 함자 $$F, G: C\rightarrow D$$가 주어졌을 때 $$F$$의 치역을 상상해 보면 $$\mathscr D$$위에 놓인 객체의 모임과 그 사이의 화살표들이다. 비슷하게 $$G$$의 치역은 다른 객체의 모임이다. 거칠게 말하면, 자연 변환은 첫 객체 모임을 $$\mathscr D$$에서 정의된 화살표를 사용해 두 번째 객체 모임으로 "자연스럽게" 바꾸는 방법이다; 즉 모든 객체에 대해 같은 식으로 바꾼다.

**정의 2.2.** 함자 $$F, G: \mathscr C\rightarrow \mathscr D$$가 주어졌을 때, 자연변환 $$\eta: F\rightarrow G$$는 $$\mathscr D$$의 화살표의 모임으로, 정확히는 $$\mathscr C$$의 객체 $$X$$ 하나 당 $$\eta_X$$라는 화살표[^2] 하나로 바꾸어 다음의 diagram이 각 $$X, Y\in \mathscr C$$에 대해 commute한다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/3.png)

**정의 2.3.** 모든 화살표가 동형사상인 자연 변환을 자연 동형(natural isomorphism)이라고 한다.

## 3. 극한

카테고리 이론에서 극한이라는 개념은 수학의 다양한 영역에서 발생하는 다양한 유형의 보편 구성(universal construction)을 일반화한다. 위상 공간, 집합 또는 군의 곱처럼 다른 종류의 객체의 수학적으로 유사한 구성(construction)이, 카테고리 이론에서는 동일한 구성의 예시에 불과하다는 사실을 매우 정확하게 기술할 수 있다. 집합의 데카르트 곱을 고려해보라. $$X \times Y$$는 일반적으로 순서쌍 $$\{(x, y)\\|x ∈ X \text{  and  } y ∈ Y \}$$라는 집합을 내부적으로 구성하여 정의한다. 이는 보편적인 방식으로 $$X$$와 $$Y$$로 투영되는 집합으로 이해할 수 있다. $$X\times Y$$에 무언가를 한다는 것은, $$X$$와 $$Y$$에 따로 무언가를 한다는 것과 같다는 것이다.

**정의 3.1.** 카테고리 $$\mathscr C$$의 객체 $$A, B$$의 곱(product)이란, 다음의 보편 성질(universal property)[^3]을 만족하는 객체 $$C$$와 사영(projection)이라고 하는 화살표 $$p : C \rightarrow A$$ 와 $$ q : C \rightarrow B$$로 정의된다. 임의의 다른 객체 $$D \in \mathscr C$$와 화살표 $$ f : D → A$$ 와 $$g : D → B$$에 대해 $$p\circ u = f$$와 $$q\circ u = g$$가 되도록 하는 유일한 화살표 $$u : D → C$$가 존재한다. 즉, 모든 $$(D, f, g)$$는 $$(C, u)$$를 통해 고유하게 인수분해된다 ($$(D, f, g)$$ uniquely factors through $$(C, u)$$).

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/4.png)

**예 3.2.** $$\textbf{Set}$$에서 곱은 데카르트 곱이다. 사영 $$p : A\times B \rightarrow A$$ 와 $$q : A\times B \rightarrow B$$는 $$p(a, b)=a$$ 와 $$q(a, b)=b$$로 주어진다. 다른 집합 $$D$$와 화살표 $$f:D\rightarrow A$$, $$g:D\rightarrow B$$가 주어지면, 화살표 $$u:D\rightarrow A\times B$$는 $$u(d)=(f(d), g(d))$$로 주어진다. 이렇게 정의하면 diagram이 commute한다는 것은 자명하다. 예를 들어, $$(p\circ u)(d)=p(u(d))=p(f(d),g(d))=f(d)$$이다.

**예 3.3.** $$\textbf{Grp}$$에서 곱은 군의 직접곱이다. 구성은 집합에서와 비슷하다; 각 원소는 곱은 데카르트의 곱으로 정의하고, 군 연산은 각 성분의 군의 연산을 통해 성분별로 구성한다. 보편 화살표 $$u$$가 존재하고 유일하다는 것을 보이기 위해, 이렇게 구성된 함수 $$u$$가 준동형이고 $$f, g$$가 준동형이라는 것을 보이면 충분하다. (사영이 준동형임은 자명하다.) 증명은 단도직입적이다.

$$u(d_1d_2) = (f(d_1d_2), g(d_1d_2)) = (f(d_1)f(d_2), g(d_1)g(d_2))
= (f(d_1), g(d_1))(f(d_2), g(d_2)) = u(d_1)u(d_2)$$

**예 3.4.** $$\textbf{Top}$$에서 곱은 위상공간의 곱이다. 사실 위상의 곱은 "사영이 연속인 가장 엉성한(coarsest) 위상"이라고 정의하는데, 위의 diagram과 정확히 일치한다.

**예 3.5.** 부분순서집합에서 곱은 (존재하면) 가장 작은 상한(least upper bound)이다. 이는 집합과 매우 다른 예일 뿐만 아니라, 곱이 존재하지 않을 수도 있다는 사실을 보여준다. $$c=lub(a, b)$$라고 하자. 이 때 사영을 정의하는 방법은 하나뿐이다[^101]. $$d$$가 $$a, b$$로의 화살표가 있다는 것은 $$a\le d$$, $$b\le d$$라는 것이고, 따라서 $$d$$는 상한이다. 그러나 $$c$$는 가장 작은 상한이므로, $$c\le d$$이다.
이 카테고리에서는 화살표가 희소하므로 보편 화살표가 쉽게 commute하며, 유일하다.

**명제 3.6.** *카테고리에서 두 객체의 곱은 (존재하면) 동형인 객체를 제외하고 (up to isomorphism[^102]) 유일하다.*

증명.  $$A$$와 $$B$$가 카테고리의 객체라고 하고, $$(C, p_C, q_C)$$와 $$(D, pD, qD)$$가 $$A$$와 $$B$$의 곱이라고 하자. 보편 성질에 의해, 화살표 $$f: C\rightarrow D$$와 $$g: D\rightarrow$$가 유일하게 존재한다. $$p_C \circ g=p_D$$와 $$p_D\circ f=p_C$$이므로 $$p_C\circ g\circ f=p_C$$이다. 비슷하게, $$q_C\circ g \circ f=q_C$$이다. 따라서 $$g\circ f$$는 $$C$$에서 자기 자신으로의 사상이고 사영과 commute한다. 그러나 보편 성질에 의해 사영과 commute하면서 $$C$$에서 자기 자신으로의 화살표는 유일하므로, $$g\circ f=1_C$$이다. $$f\circ g=1_D$$도 마찬가지이다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/5.png)
◻

**Remark 3.7.** 곱은 두 개 이상의 성분으로 자명하게 일반화할 수 있다. 후에 "모든 작은 곱"을 가지는 카테고리를 다룬다. 이는 단지 어떤 집합의 곱이 존재한다는 것에 불과하다. $$\textbf{Set}$$에서는 모든 작은 곱이 존재한다는 것이 분명하다.

두 번째로 중요한 극한의 예는 동등자(equalizer)이다. 집합과 그 비슷한 카테고리에서는 단지 두 평행한 화살표의 치역이 같도록 하는 정의역의 부분집합이다.

**정의 3.8.** 카테고리 $$\mathscr C$$의 두 화살표 $$f, g:X\rightarrow Y$$의 동등자란 객체 $$E$$와 화살표 $$e: E\rightarrow X$$로, 다음의 보편 성질을 만족한다:
임의의 $$O\in\mathscr C$$와 화살표 $$O\rightarrow X$$가 $$f\circ m=g\circ m$$을 만족할 때, $$u: O\rightarrow E$$가 유일하게 존재해서 $$m=e\circ u$$이다. 이 동등자를 $$\text{eq}(X, Y)$$라고 쓴다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/6.png)

**Remark 3.9.** $$\textbf{Grp}$$와 $$\textbf{Top}$$에서는 동등자는 위와 같은 식으로 구성한다. $$\textbf{Grp}$$에서는 차핵(difference kernel)으로 볼 수 있다. 사실 핵(kernel) 자체를 극한으로 볼 수 있다.

이제 우리는 극한의 일반적인 개념을 접할 준비가 되었다. 하지만 먼저 뿔(cone)을 정의하자. 곱에서 사영의 역할은 항등자에서 $$e$$와 같았다는 것을 의식하자. 다음에서 $$\mathscr J$$는 작은 카테고리로 생각해야 한다. 곱의 경우에는 두 독립된 객체가 있고 화살표는 항등 화살표만 있는 카테고리이다. 항등자의 경우에는 두 독립된 객체 사이의 화살표가 두 개 있는 카테고리이다.

**정의 3.10.** 함자 $$F: J\rightarrow C$$가 주어졌을 때, $$F$$의 뿔은 객체 $$N\in \mathscr C$$과 각 $$X\in\mathscr J$$마다 정의된 화살표 $$\psi_X: N\rightarrow F(X)$$이고, $$\mathscr J$$의 모든 화살표 $$X\rightarrow Y$$에 대해 다음의 삼각형이 commute한다. 즉, $$Ff\circ \psi_X = \psi_Y$$이다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/7.png)


**정의 3.11.** 함자 $$F:\mathscr J\rightarrow \mathscr C$$의 극한은 보편 뿔[^4] $$(L,\phi_X)$$이다. 즉, $$F$$의 모든 뿔 $$(N, \psi_X)$$에 대해, 유일한 화살표 $$u: N\rightarrow L$$이 존재해서 모든 객체 $$X\in\mathscr J$$ 에 대해 $$\phi_X=u\circ \psi_X$$이다. 극한 객체는 $$\lim_{i\in\mathscr J} F(i)$$라고 쓴다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/8.png)

**명제 3.12.** *어느 카테고리에서 어떤 diagram의 극한이 존재하면, 동형인 객체를 제외하고 유일하다.*

## 4. 당김

명시적으로 정의할 마지막 극한의 예로 당김(pullback 혹은 fiber product)을 소개한다. 많은 중요한 극한들이 있지만, 모든 다른 극한을 곱과 동등자에서 유도하는 방법에 대한 예로 당김을 사용할 것이다.

**정의 4.1.** 당김이란, 다음 형태의 diagram의 극한이다: $$A\rightarrow C \leftarrow B$$. 즉, 당김은 객체 $$D$$와 화살표 $$p_1:D\rightarrow A$$와 $$p_2: D\rightarrow B$$여서, 사각형을 commute하게 하고 보편적이다. 즉 다른 모든 객체 $$Q$$와 화살표 $$q_1:Q\rightarrow A$$ 와 $$q_12: Q\rightarrow B$$에 대해, 화살표 $$u: Q\rightarrow D$$가 유일하게 존재해서 아래 diagramm이 commute한다. 당김의 객체 $$D$$는 $$A \times_C B$$로 쓴다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/9.png)


**명제 4.2.** *집합에서는, 당김은 함수 $$f:X\rightarrow Z, g:Y\rightarrow Z$$가 주어졌을 때 집합 $$X \times_Z Y = \{(x, y)\\|f(x)=g(y)\}$$과 $$X, Y$$로의 사영 $$p_1, p_2$$로 정의된다.*

증명. $$D, q_1, q_2$$가 위의 diagram의 뿔이라고 하자. 각 $$d\in D$$에 대해 $$f(q_1(d)) = g(q_2(d))$$이다. 따라서 $$(q_1(d), q_2(d))$$는 $$X \times_Z Y$$의 원소이다. $$u(d) = (q_1(d), q_2(d))$$로 정의한다. ◻

**명제 4.3.** *임의의 카테고리에서 당김은 곱과 동등자를 사용해 정의할 수 있다.*

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/10.png)

곱 $$A\times B$$의 정의를 통해 대각선 상의 두 평행한 화살표를 유도할 수 있는데, 이에 동등자를 적용한다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/11.png)

이제 당김 diagram와 commute하는 뿔을 고려한다. 곱의 보편 성질에 의해 정의되는 곱의 유일한 화살표가 있다. diagram을 따라가며 설명해보면, 이 화살표는 대각선 상의 화살표를 같게 하는 것으로 볼 수 있으며, 이는 diagram을 commute하게 하는 동등자에 고유한 화살표가 된다. 따라서, 이 동등자는 당김이 된다.

## 5. 완전 카테고리

**정의 5.1.** 모든 작은[^5] diagram이 극한을 가질 때, 카테고리를 완전하다고 한다.

**정리 5.2.** *$$F : J → \textbf{Set}$$가 $$\textbf{Set}$$의 임의의 작은 diagram이라고 하자. 그러면 $$F$$의 극한은 다음의 집합이다.*

$$L = \lim_{i\in \mathscr J} F(i) = {(x_i) ∈ \prod_{i\in \mathscr J} F(i)\\|(Ff)(x_i) = x_{\text{cod} f}\forall f ∈ Ar(\mathscr J)}$$

**Remark 5.3.** 위와 동치인 조건으로, $$f, g \in Ar(\mathscr J )$$ 이고 $$\text{cod} f = \text{cod} g$$ 일 때 $$(Ff)(x_i) = (Fg)(x_j)$$라고 할 수 있다. $$g$$가 항등사상일 때 위의 정리가 되고, 반대 방향으로 가려면 $$\text{cod} f = \text{cod} g = k$$이면 $$(Ff)(x_i) = x_k = (Fg)(x_j)$$라는 사실을 관찰하면 된다. 이를 통해 극한을 만들기 위해 동등자를 취하고 있는 것이 명확해진다.

증명. 극한 뿔이 $$(L, p_i)$$라고 하고, 다른 뿔이 $$(N, (\psi_i)_{i\in \mathscr J})$$라고 하자.
그러면 $$\text{cod} f = \text{cod} g$$일 때 모든 $$n\in N$$에 대해 $$(Ff)(\psi_i(n))=(Fg)(\psi_j(n))$$이다. 따라서 순서쌍 $$(\psi_i(n))_{i\in \mathscr J}$$ 은 $$L$$의 원소이다. ◻

**정리 5.4.** *모든 동등자와 작은 곱이 존재하는 카테고리는 완전하다.*

증명. 위의 증명의 아이디어를 조심스럽게, 조금 참신하게 일반화한 것이 이 증명이다.
직접적인 같음이 더 이상 존재하지 않으므로, 동등자를 이용해야 한다. 우리는 두 곱을 가져 와서 그 사이에 두 개의 화살표를 찾아, 그 화살표를 통해 동등자가 극한이 되도록 할 것이다. 먼저 다이어그램의 모든 객체에 대해 곱을 취한 뒤, 화살표로 인덱싱된 diagram의 모든 화살표의 끝점에 대해서 곱을 취한다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/12.png)

첫 번째 그림 상단의 삼각형과 하단의 사각형에서 보는 것처럼, 첫 번째 곱에서 두 번째 곱의 뿔을 만드는 방법은 두 가지이다.
이를 통해 모든 삼각형과 사각형이 commute하도록 하는 두 개의 화살표 $$u, v$$를 얻는다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/13.png)

동등자는 위와 같이 취하고, 화살표 $$\phi_i = p_i e$$로 뿔 $$(E, \phi_i)$$을 정의한다. 뿔이라는 것은 diagram을 살펴보면 알 수 있다. $$f:j\rightarrow k$$에 대해 $$ue=ve$$, $$p_f ue = p_f ve$$, $$p_k e=(Ff)\circ p_j e$$, $$\phi_k = (Ff)\circ \phi_j$$이다. 그러면 보편 성질을 통해 모든 다른 뿔 $$(Q, \psi_i)$$에서 곱으로의 유일한 사상 $$t$$를 얻을 수 있다. 하지만 이는 뿔이기 때문에 $$ut=vt$$이고, 따라서 동등자의 보편 성질에 의해 유일한 화살표 $$s: Q\rightarrow E$$가 존재한다. ◻

## 6. 또 다른 극한 정리

아름답고 매력적인 정리를 소개한다. 많은 분야의 연구에서 많은 것을 해냈다. 다른 정리를 증명한다는 목적 이외에도, 카테고리의 극한의 개념에 숨어있는 많은 직관을 기술한다.

**정리 6.1.** *$$F: \mathscr J \rightarrow \mathscr C$$가 $$\mathscr C$$의 diagram이라고 하자. 그러면 객체 $$X\in \mathscr C$$가 $$F$$의 극한이라는 것은 자연 동형 $$\text{Hom}_{\mathscr C}(C,X) \simeq \lim_{i\in\mathscr J} \text{Hom}_{\mathscr C}(C,F(i))$$가 존재한다는 것과 동치이다. 우변의 극한은 $$\textbf{Set}$$에서 정의되므로 항상 존재한다.*

곱에 대한 증명. 먼저 $$C$$가 곱 $$A\times B$$라고 하자. $$\text{Hom}(D, C) \simeq \text{Hom}(D, A)\times \text{Hom}(D, B)$$인 전단사함수를 찾으면 된다. $$D$$에서 $$A, B$$로의 화살표가 주어지면 $$F$$의 뿔을 얻을 수 있고, $$C$$가 곱이기 때문에 보편 성질에 의해 유일한 화살표 $$u$$를 얻는다. 반대 방향은 화살표 $$h:D\rightarrow C$$가 주어졌을 때 단순히 $$p\circ h, q\circ h$$를 취하면 된다. 따라서 전단사 함수를 얻었다.

자연 변환임을 보이기 위해, $$\alpha: M\rightarrow N$$이 $$\mathscr C$$의 화살표라고 하자. 그러면 다음의 diagram이 commute한다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/14.png)

여기서 세로 방향 화살표는 단순히 $$\alpha$$로 왼쪽 합성을 한 것이고, 가로 방향 화살표는 각 성분에 $$p, q$$로 오른쪽 합성을 한 것이다. 결합법칙에 의해 diagram은 commute한다.

반대로 어떤 자연 동형이 객체 $$C$$에 주어졌다고 하자. 그러면 곱을 만들기 위해 사영을 찾아야 한다. 이 때 다음의 자연 동형에서 영감을 얻을 수 있다.

$$\text{Hom}(C, C)\simeq \text{Hom}(C, A) \times \text{Hom}(C, B)$$

임의의 카테고리라고 해도, $$\text{Hom}(C, C)$$는 항등사상이 있다. 항등사상을 위의 동형에 넣어보면 $$p: C\rightarrow A, q:C\rightarrow B$$를 얻는다. 이제 $$D, f, g$$가 다른 뿔이라고 해보자. 그럼 다음 diagram을 통해 보편 성질을 증명할 수 있다.

![](/images/2022-11-08-translation-limits-in-category-theory-scott-messick/15.png)

위의 전단사 함수로 $$(f, g)$$에서 $$u: D\rightarrow C$$를 얻을 수 있으므로, 우리는 세로 방향 화살표를 구성할 수 있다는 것을 알고있다. 세로 방향 화살표는 $$u$$의 왼쪽 합성이다. 그러면 diagram이 commute한다는 것은 $$p\circ u=f$$이고 $$q\circ u=g$$라는 것이다. ◻

이 정리는 곱의 아이디어를 기술하고 있다는 점에 주목하자: 각 성분에 함수를 정의하는 것과 자기 자신에 함수를 정의하는 것이 같은 객체이다.

일반적인 증명. 일반적인 경우에도 비슷하게 진행된다. $$L$$이 $$F:\mathscr J\rightarrow C$$의 극한이라고 하자. 우리는 $$\text{Hom}(X,L) \simeq \lim \text{Hom}(X,F(i))$$의 전단사 함수를 찾아야 한다. 우변의 극한의 원소는 무엇일까? 우리는 $$\textbf{Set}$$에서 극한의 명시적인 기술을 알고 있다. 하지만 조심해야 하는데, 왜냐하면 여기서의 함자는 $$F$$ 자신이 아니라, 사상집합 $$\text{Hom}(X, -)$$을 $$H$$라고 하고 $$HF$$이기 때문이다. 그럼 극한의 각 원소 $$\psi_i$$에 대해 다음이 성립한다: $$f:i\rightarrow j$$가 $$\mathscr J$$의 화살표이면 $$(HFf)\circ (\psi_i)=\psi_j$$이다. 하지만 우리는 $$H$$가 화살표에 어떤 일을 하는지 아니까, $$Ff \circ \psi_i=\psi_j$$이다. 따라서 화살표들의 순서쌍 $$(\psi_i)$$가 사상집합의 극한이라는 것은, $$(X, \psi_i)$$가 $$F$$의 뿔이라는 것과 같은 말이다. 이를 통해 $$u: X\rightarrow L$$를 얻고, 이후는 앞의 증명과 똑같다.

반대 방향을 증명하기 위해, 전단사함수 $$\text{Hom}(L, L) ∼= \lim \text{Hom}(L, F (i))$$를 가져와서 항등사상을 넣으면 아까와 같이 뿔 $$(L, \phi_i)$$를 얻고, 이 뿔이 보편 뿔이라는 것을 증명해야 한다. 다른 뿔이 $$(X, \psi_i)$$라고 하자. 아까와 같이, $$u$$와 전단사함수를 찾아 diagram을 구성하면, 증명이 완성된다. ◻

## References
1. Mac Lane, Saunders. Categories for the Working Mathematician. Second Edition, 1998.
2. Gillou, Bert and Haris Skiadas. WOMP 2004: Category Theory.
3. Anders, Alan. DRP Notes, Winter 2007.

## 역주

- 원 논문의 오탈자를 수정했다.
- 원 논문의 proclamation 3.4가 수식에 붙어있는데, 오타로 보인다. 제외했다.****

---

[^1]: 이 논문의 범위에서는, "모임"이라는 단어를 명확히 하지 않을 것이다. 그러나 많은 경우에 집합이기에는 너무 크다는 것을 인지하기 바란다.
[^2]: 첨자가 중첩되는 것을 피하기 위해 여기서는 표기를 살짝 바꾼다.
[^3]: 보편 성질의 수학적인 정의가 존재하지만, 이 논문의 목적상 불필요하다.
[^4]: 극한이라는 단어는 뿔 전체(즉, 객체와 화살표)가 아니라 뿔의 꼭지점만을 표현하기 위해 쓰기도 한다.
[^5]: diagram이 작다는 것은 객체의 모임이 집합이라는 뜻이다.
[^101]: (역주) poset의 정의 상 객체 사이의 화살표는 하나뿐이니까
[^102]: (역주) [equal up to](https://en.m.wikipedia.org/wiki/Up_to)는 수학적인 용어이다.
