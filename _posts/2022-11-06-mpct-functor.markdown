---
layout: mathpost
title:  "메타프로그래밍: 함자"
date:   2022-11-06 00:30:00 +0900
published: true
tags: category-theory functor
---

## 직관

카테고리 사이의 준동형사상을 함자(functor)라고 한다.
이 준동형 사상은 카테고리의 각 구성요소를 각 구성요소로 옮겨야 하므로, 카테고리 $$ C $$에서 $$ D $$로의 함자 $$F:C\rightarrow D$$ 는 점을 점으로, 화살표를 화살표로 옮겨야 할 것이다. 즉, $$ F_0: C_0 \rightarrow D_0 $$ 와 $$ F_1: C_1 \rightarrow D_1 $$ 의 두 개의 사상을 정의해야 한다.
또한, 이 준동형 사상은 카테고리의 구조를 보존해야 하므로, 항등원은 항등원으로, 합성 가능한 화살표들은 함자를 적용한 뒤에도 합성 가능해야 한다.

## 정의

### 구성요소
카테고리 에서 로의 함자 $$ F $$ 는:
1. $$ C $$ 의 각 점 $$ x\in C_0$$ 를 $$ F_0(x) \in C $$ 로 보낸다.
2. $$ C $$ 의 각 화살표 $$ f \in C_1(x, y) $$ 를 $$ F_1(f) \in D_1(F(x), F(y)) $$ 로 보낸다.

### 만족해야 하는 조건
1. 함자 F는 합성을 보존한다. 즉, $$ F_1(g\circ f) = F_1(g) \circ F_1(f) $$ 이다. (단, 존재하면)
2. F는 항등원을 보존한다. 즉, $$ F_1(1_x) = 1_{F_0(x)} $$ 이다.
3. (1), (2)와 동치로, 다음의 diagram이 commute한다.

$$
\begin{CD}
    x     @>F>>  F(x)   \\
    @VV{f}V  @VV{Ff}V\\
    y     @>F>> F(y)
\end{CD}
$$

### Syntactic Sugar

점과 화살표가 맥락상 명확히 구분될 때, $$ F_0(x) $$ 나 $$ F_1(f) $$ 대신 $$F(x)$$ 혹은 $$F(f)$$와 같이 첨자를 생략하여 표시한다.

## 성질

함자는 합성 가능하다. 즉, 카테고리 $$ C $$에서 $$ D $$로의 함자 $$ F $$와 카테고리 $$ D $$에서 $$ E $$로의 함자 $$ G $$가 주어졌을 때, $$G\circ F: C \rightarrow E $$ 또한 함자이다.

## 예시

C++ Template, Rust나 Python의 Generic 등이 바로 함자이다.
예를 들어 임의의 자료형 `T`에 대해 정의되는 `LinkedList[T]` 등이다.

## 카테고리의 카테고리

카테고리의 카테고리 Cat을 다음과 같이 정의한다.
1. 점은 카테고리이다.
2. 화살표는 함자이다.
3. 합성은 함자의 합성으로 정의된다.
4. 항등화살표는 함자 $$(x \mapsto x)$$로 정의된다.

## 포함

함자의 직관 중 하나로, "카테고리 $$C$$가 $$D$$에서 어떻게 표현되는가"라는 일종의 포함관계를 함자 $$F$$를 통해 살펴볼 수 있다. 이를 조금 더 자세히 정의하려면, 집합에서의 단사와 전사의 정의를 살펴볼 필요가 있다.

### 단사 (monomorphism)

집합에서 단사(injection)라는 것은, 집합 $$A, B$$ 사이의 함수 $$ f:A\rightarrow B $$가 주어졌을 때, 모든 $$x, y \in A$$에 대해 $$f(x) = f(y)$$이면 $$x=y$$라는 뜻이다. 즉, 출력 값이 같으면 입력이 같았다는 뜻이다.

카테고리의 언어로 집합의 카테고리 Set에 대해 위의 정의를 다시 써보려고 하면 바로 문제가 생긴다. 왜냐하면 우리는 $$A$$가 "원소"를 가지고 있다는 사실을 모르기 때문이다. 대신 우리는 집합의 카테고리 Set에 $$\{\phi\}$$, 즉 원소가 하나인 집합이 있다는 것을 알고 있다. 이 집합을 $$T$$라고 하면, $$T$$에서 집합 $$A$$로의 화살표 $$Set(T, A)$$와 $$A$$가 같다는 것을 알 수 있다. 형식적으로는 요네다 보조정리를 이용해 증명할 수 있다.

하지만 $$T$$에서 출발하는 화살표 뿐만 아니라 임의의 $$C$$에서 출발하는 화살표를 생각해도 상황은 같다. 즉, $$g_1, g_2: C\rightarrow X$$에 대해, $$f \circ g_1 =f\circ g_2$$이면 $$g_1 = g_2$$이다. 이렇게 단사를 정의하면, $$T$$를 도입하지 않아도 된다.

#### 정의

카테고리 $$C$$에서 화살표 $$f: y\rightarrow z$$가 단사(monomorphism)라는 것은, 임의의 $$g_1, g_2: x\rightarrow y$$ 가 주어졌을 때 $$f \circ g_1 =f\circ g_2$$이면 $$g_1=g_2$$가 성립한다는 것이다.

조금 더 멋을 부려 다르게 표현해 보면, $$C(-, f)$$가 집합의 단사이면 $$f$$를 카테고리의 단사라고 한다.

### 전사

카테고리 $$C$$에서 화살표 $$f: x\rightarrow y$$가 전사(epimorphism)라는 것은, 임의의 $$g_1, g_2: y\rightarrow z$$ 가 주어졌을 때 $$g_1\circ f=g_2\circ f$$이면 $$g_1=g_2$$가 성립한다는 것이다.

조금 더 멋을 부려 다르게 표현해 보면, $$C(f, -)$$가 집합의 전사이면 $$f$$를 카테고리의 전사라고 한다.

### Full/Faithful functor

함자 $$ F: C\rightarrow D$$가 full이라는 것은, 모든 $$x, y\in C$$에 대해 $$F_1: C(x, y) \rightarrow D(F(x), F(y))$$가 집합에서 전사라는 뜻이다. $$F_1: C(x, y) \rightarrow D(F(x), F(y))$$가 단사인 경우에는 Faithful 이라고 부른다.

### 부분카테고리

카테고리 $$D$$가 카테고리 $$C$$의 부분카테고리(subcategory)라는 것은, $$C_0$$의 부분모임이 $$D_0$$이고 $$C_1$$의 부분모임이 $$D_1$$이어서, 다음의 조건들을 만족한다는 뜻이다.

1. $$C$$의 화살표 $$f:x\rightarrow y$$가 $$D_1$$에 포함되면, $$x,y$$는 $$D_0$$에 포함된다.
2. $$C$$의 점 $$x$$가 $$D_0$$에 포함되면, $$1_x$$는 $$D_1$$에 포함된다.
3. $$C$$의 화살표 $$f:x\rightarrow y$$, $$g: y\rightarrow z$$가 $$D_1$$에 포함되면, $$C$$의 화살표 $$g\circ f$$ 도 $$D_1$$에 포함된다.

부분 카테고리의 정의에 의해 자연스럽게 정의되는 포함 관계는 함자이다. 이를 포함 함자(inclusion functor)라고 부른다.

포함 함자는 정의 상 faithful하다.

특히, 포함 함자가 full이면, 그 부분 카테고리를 full하다고 한다.

### $$ x $$에서 출발하는 화살표들의 집합

국소적으로 작은 카테고리 $$ C $$ 와 점 $$ x\in C $$를 고정했을 때, 이 점에서 출발하는 화살표들의 집합, 즉 Homset으로의 사상 $$ y\mapsto C(x, y) $$ 을 생각해볼 수 있다. 대개 $$ C(x, -):C\rightarrow \text{Set} $$ 로 표기한다. 이 사상을 함자로 정의하기 위해서는, 함자의 정의의 각 항목을 확인하면 된다.
1. 점을 점으로 보내는가?
   국소적으로 작은 카테고리의 정의 상, 임의의 $$ y \in C$$에 대해 $$C(x, -)(y) = C(x, y)$$는 집합이다. 즉, Set 카테고리의 점이다.
2. 화살표를 화살표로 보내는가?
   임의의 화살표 $$ f: y\rightarrow z $$ 에 대해, $$ C(x, -)(g) = (f\mapsto g\circ f)$$로 정의하면, 분명 집합을 집합으로 보내므로, Set 카테고리의 화살표이다.
3. 항등원을 보존하는가?
   $$ C(x, -)(1_x) $$
   $$ = (f\mapsto f) $$
4. 합성을 보존하는가?
   즉 임의의 $$ g, h \in C_1 $$에 대해 $$ C(x, -)(h\circ g) = C(x, -)(h) \circ C(x, -)(g) $$ 인가?

   $$ C(x, -)(h\circ g) $$

   $$ = C(x, h \circ g) $$

   $$ = (f\mapsto (h\circ g) \circ f) $$

   $$ = (f\mapsto h\circ (g \circ f)) $$

   $$ = h \circ (f\mapsto g \circ f) $$

   $$ = (f \mapsto h\circ f) \circ (f \mapsto g \circ f) $$

   $$ = C(x, -)(h) \circ C(x, -)(g) $$

   이므로, 합성을 보존한다.

따라서, $$ C(x, -) $$는 함자이다.

### $$ x $$로 끝나는 화살표들의 집합

마찬가지로 $$ C(-, x) $$ 도 함자인데, 조금 다르다. 왜냐하면 위와 같이 정의하면 화살표 $$ g\in C_1 $$에 대해, 화살표의 변환은 $$ C(-, x)(g)=(f\mapsto f\circ g) $$ 로 정의되는데, "합성을 보존하는가?" 부분을 똑같이 전개해 보면

$$ C(x, -)(h\circ g) $$

$$ = C(x, h \circ g) $$

$$ = (f\mapsto f\circ (h\circ g)) $$

$$ = (f\mapsto (f\circ h) \circ g) $$

$$ = (f\mapsto f \circ h) \circ g$$

$$ = (f \mapsto f\circ g) \circ (f \mapsto f \circ h) $$

$$ = C(x, -)(g) \circ C(x, -)(h) $$

즉, $$ F(h\circ g) = F(g) \circ F(h) $$ 로 합성의 순서가 보존되지 않고, 반대가 됨을 알 수 있다.
반대 카테고리를 사용해 합성의 순서가 반대가 되는 문제를 해결할 수 있다. 바로 $$ F:C\rightarrow Set $$ 대신 $$ F':C^{op}\rightarrow Set$$ 를 도입해, $$ F'(f)=F(f^{op})$$ 라고 정의하면 된다. 그러면:

$$ F'(g^{op}\circ h^{op})$$

$$=F'((h\circ g)^{op})$$

$$=F(h\circ g)$$

$$=F(g)\circ F(h)$$

$$=F'(g^{op})\circ F'(h^{op}) $$

로, 합성의 순서를 보존한다!

이렇게 합성의 순서가 반대로 뒤집혀, 반대 카테고리를 사용해 함자로 만들 수 있는 경우를 contra-functor라고 부른다. $$ F: C^{op} \rightarrow D $$로 쓰되, 인자 부분의 $$(-)^{op} $$ 는 생략해서 쓴다. 즉, $$ C(-, x)(g^{op}) $$ 대신 $$ C(-, x)(g) $$ 라고 쓴다.

contra-functor의 반대말은 co-functor이다. 함자가 co-인지 contra-인지를 variance라고 부른다. functor가 covariant라는 것은 co-functor를 칭하는 것이고, functor가 contravariant라는 것은 contrafunctor라는 뜻이다.

### Hom-functor의 정의

위에서 보았듯, Homset $$ C(x, y) $$는 두 인자 모두에 대해 함자로써 정의되므로, 곱 카테고리에서 집합으로의 함자로 생각할 수 있다. 즉, $$ C(-, -): C^{op}\times C \rightarrow Set $$이다. 이 함자는 단연 카테고리 이론에서 가장 중요한 함자라고 할 수 있다. 이 함자를 **Hom-functor**라고 한다.

1. Hom-functor $$C(-, -)$$의 점의 사상은 $$ C(-, -)((x, y)) = C(x, y)$$ 로 정의된다.
2. Hom-functor $$C(-, -)$$의 화살표의 사상은 $$ C(-, -)(g, h) = (f\mapsto h\circ f \circ g)$$로 정의된다.

### Profunctor로의 확장
hom-functor는 "$$ x \in C $$에서 $$ y \in C $$로 가는 화살표들의 집합"으로 정의된다. 이를 더 일반화해, "$$ x \in C $$ 에서 $$ y \in D $$ 로의 합성 가능한 관계의 집합"을 정의할 수 있는데, 이러한 함자는 $$ C^{op} \times D \rightarrow \text{Set} $$로 표현할 수 있다. 이러한 함자를 Profunctor라고 부른다. 나중에 자세히 소개한다.

### Hom-object로의 확장
당분간은 $$ x, y\in C$$ 사이의 화살표들 $$ C(x, y) $$ 가 집합인 경우만 생각하지만, 구체적인 예에 있어서는, $$ C(x, y) $$가 집합 이상의 정보를 가지는 경우가 많다. 예를 들어 반순서 집합의 경우는 boolean의 구조를 가지고 있다. 이러한 경우, hom-set 대신 hom-object라고 부르고, 이러한 카테고리를 enriched category라고 부른다. 특히 $$ C(x, y) \in C $$ 인 경우, 즉 $$ C(-, -): C^{op} \times C \rightarrow C $$인 경우, 이를 internal hom이라고 부른다.
