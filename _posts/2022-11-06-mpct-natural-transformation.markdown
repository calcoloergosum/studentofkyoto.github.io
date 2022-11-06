---
layout: mathpost
title:  "메타프로그래밍: 자연변환"
date:   2022-11-06 21:30:00 +0900
published: true
tags: category-theory natural-transformation
---

## 직관

두 함자 $$ F, G: C\rightarrow D$$ 가 주어졌을 때, 함자 사이를 "건너뛰는" 사상 $$\alpha(x)=(F(x) \mapsto G(x))$$ 를 정의하고 싶다. 이는 "거의 $$G\circ F^{-1}$$"라고 볼 수 있겠다. 그러나 $$F^{-1}$$은 아직 정의하지 않았을 뿐더러, 정의했다고 해도 반드시 존재해야 하는 것은 아니다. 존재하지 않는 경우가 많다.

## 정의

아래의 diagram이 commute하는 사상 $$\alpha_{(-)}:C_0\rightarrow D_1(F(-), G(-))$$를 $$F$$에서 $$G$$로의 자연 변환이라고 부른다.

$$
\begin{CD}
   F(x)   @>\alpha_x>>   G(x)     \\
        @VV{F(f)}V       @VV{G(f)}V \\
   F(y)   @>\alpha_y>>   G(y)
\end{CD}
$$

즉, $$\alpha_y \circ F(f) = G(f) \circ \alpha_x$$이다. 이를 Naturality condition이라고 부른다.

정의의 동기에 관해서는, John D. Cook의 "[자연변환(번역)]({% post_url 2022-11-05-translation-natural-transformation %})"이라는 포스트를 읽어보길 추천한다.

### Syntactic Sugar
$$F$$에서 $$G$$로의 자연 변환을 $$\alpha: F\Rightarrow G$$로 표기한다.

## 성질

### 합성

자연 변환은 합성 가능하다. 즉, 세 함자 $$F, G, H: C\rightarrow D$$와 두 자연변환 $$\alpha: F\Rightarrow G$$와 $$\beta: G\Rightarrow H$$이 주어지면, $$\beta \circ \alpha: F \Rightarrow H$$를 $$(\beta \circ \alpha)_x=(F(x)\mapsto \beta_x(\alpha_x(F(x))))$$로 정의하고, 자연변환이다. Naturality condition을 확인해 보자.

카테고리 $$C$$의 화살표 $$f:x\rightarrow y$$가 주어졌을 때,

$$
\begin{CD}
   F(x)   @>{\beta_x \circ \alpha_x}>> H(x)      \\
   @VV{F(f)}V                          @VV{H(f)}V\\
   F(y)   @>{\beta_y \circ \alpha_y}>>  H(y)
\end{CD}
$$

한 번 풀어 헤쳐보면 다음과 같다.

$$
\begin{CD}
   F(x)   @>\alpha_x>>   G(x)   @>\beta_x>>   H(x)      \\
   @VV{F(f)}V            @VV{G(f)}V           @VV{H(f)}V\\
   F(y)   @>\alpha_y>>   G(y)   @>\beta_y>>   H(y)
\end{CD}
$$

수식으로 쓰면 다음과 같다.

$$(H(f)\circ (\beta\circ \alpha)_x)(F(x))$$

$$=H(f)(\beta_x(\alpha_x(F(x))))$$

$$=H(f)(\beta_x(G(x)))$$

$$=H(f)H(x)$$

$$=H(y)$$

$$=\beta_y (G(y))$$

$$=\beta_y (\alpha_y(F(y)))$$

$$=((\beta_y \circ \alpha_y) \circ F(f))(F(x))$$

$$=((\beta \circ \alpha)_y \circ F(f))(F(x))$$

따라서, $$\beta\circ\alpha$$도 자연변환이다.

자연변환의 합성을 vertical composition이라고 한다.

## 함자의 카테고리

자연변환이 합성 가능하다는 점에서 이미 눈치 챘을 수도 있겠다. 이는 곧 함자가 카테고리라는 것을 의미한다.

### 정의

카테고리 $$C, D$$가 주어졌을 때, 두 카테고리 사이의 함자 카테고리 $$[C, D]$$는 다음과 같이 정의된다.
1. 점은 함자 $$F:C\rightarrow D$$ 이다.
2. 화살표는 자연변환 $$\alpha:F\Rightarrow G$$이다.
3. 항등 화살표는 $$\alpha_x=(F(x)\mapsto F(x))$$이다.
4. 화살표의 합성은 자명하게 정의된다.

### Syntax의 주의점

카테고리의 종류가 점점 많아지면서, 합성의 종류의 수도 함께 늘어난다. 예를 들어 함자 $$F: C\rightarrow D$$와 $$G: D\rightarrow E$$, 그리고 $$H, K: C\rightarrow E $$, 자연변환 $$\alpha: GF\Rightarrow H$$와 $$\beta: H\Rightarrow K $$가 주어졌을 때,

(\beta \circ \alpha)_x\circ(G\circ F)(g\circ f)$$라는 식을 생각해보자. 똑같은 기호 $$\circ$$가 네 번 등장하고 있지만, 네 번 다 정의가 다르다. 각 합성이 정의되는 카테고리를 첨자로 써 보면 다음과 같다.

$$ (\beta \circ_{[C, E]} \alpha)_x\circ_E(G\circ_{\text{Cat}} F)(g\circ_C f)$$

그러나 문맥 상 어느 카테고리에서 합성하는지 혼동의 여지가 없으므로, 함자에 대해서는 오히려 생략할 수 있다. 즉, 앞으로는 $$G\circ F$$와 $$GF$$를 혼용한다.
또한, $$ G(F(f)) = (GF)(f)$$이므로, $$GFf$$로 써도 혼동의 여지가 없다.
따라서 괄호도 생략한다.

### 함자와 자연변환의 연산

카테고리 $$B, C, D, E$$와 함자 $$F, G: C\rightarrow D$$이고 $$H: B\rightarrow C$$, $$K: D\rightarrow E$$ 이고 $$\alpha: F\Rightarrow G$$일때,

1. $$\alpha_{H(-)}= (FH(-)\mapsto GH(-))$$는 자연변환이다.
2. $$K\circ \alpha_{(-)}= (KF(-)\mapsto KG(-))$$는 자연변환이다.

### Syntactic Sugar
(1)의 자연변환을 $$\alpha H$$, (2)의 자연변환을 $$K \alpha$$로 간략히 표기한다.

정리하면, 함자 사이의 연산(합성)이 잘 정의되고, 자연변환 사이의 연산(합성)이 잘 정의되며, 함자와 자연변환 사이의 연산이 잘 정의된다. 함자는 알파벳, 자연변환은 그리스 문자로 써서, "$$ F\alpha \beta G \gamma HK$$"와 같은 식도 자연 변환이다.

다만, $$\alpha Ff$$와 같이 썼을 때 $$(\alpha F)(f)$$로 해석할 여지가 있다. 물론 화살표는 자연변환의 인자가 될 수 없으나, 표기법을 유연하게 하기 위해 자연 변환의 정의를 확장하자.

### 자연 변환의 정의의 확장

아래의 diagram이 commute하는 사상 $$\alpha(-):C\rightarrow D_1(F(-), G(-))$$를 $$F$$에서 $$G$$로의 자연 변환이라고 부른다.

점에 대해서는:

$$
\begin{CD}
   F(x)   @>\alpha(x)>>   G(x)     \\
        @VV{F(f)}V       @VV{G(f)}V \\
   F(y)   @>\alpha(y)>>   G(y)
\end{CD}
$$

화살표에 대해서는:

$$
\begin{CD}
  x @. @. 1_{Fx}   @>\alpha(1_x)>>   1_{Gx} \\
  @VfVV @. @V{Ff}VV                 @VV{Gf}V \\
  y @. @. Ff       @>\alpha(f)>>   Gf
\end{CD}
$$

가 commute한다.

### Whiskering theorem

함자 $$F, G: C\rightarrow D$$ 와 $$H, K:D\rightarrow E$$, 자연변환 $$\alpha: F\Rightarrow G$$와 $$\beta: H\Rightarrow K$$가 주어졌을 때, 자연 변환 $$HF \Rightarrow KG$$ 은 $$(K\alpha) (\beta F)$$ 혹은 $$(\beta G) (H\alpha)$$로 쓸 수 있다.

이 자연변환 $$HF \Rightarrow KG$$을 $$\beta * \alpha$$ 로 표기하며, horizontal composition이라고 부른다.

#### Remark

$$\alpha(f) = Gf\circ \alpha(1_x)$$이다. 각 $$\alpha(x) = Gx \in D$$가 정의되어 있다면, $$\alpha(f)$$를 정의하기 위해 추가적으로 제약조건을 더할 필요는 없다는 뜻이다. $$\alpha(x)$$ 하나를 정의하면 임의의 $$f\in C(x, -)$$ 에 대해 $$\alpha(f)$$가 모두 정의된다.

이 말을 그대로 수식으로 바꿔 보면, 함자 $$F:C\rightarrow D$$와 자연변환 $$\eta: C(x, -)\Rightarrow F$$가 주어졌을 때, $$[C, D](C(x, -), F)=Fx$$이다. 이를 요네다의 보조정리(Yoneda Lemma)라고 부른다.

요네다 보조정리는 따로 다룬다.
