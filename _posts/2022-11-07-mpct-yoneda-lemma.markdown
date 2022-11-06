---
layout: mathpost
title:  "메타프로그래밍: 요네다 보조정리"
date:   2022-11-07 00:30:00 +0900
published: false
tags: category-theory natural-transformation yoneda-lemma
---


> 수학에서 가장 어려운 자명한 것 (the hardest trivial thing in mathematics)
> 
> &mdash; <cite>Dan Piponi</cite>


> 기초적이지만 심오하고 중심적인 것 (elementary but deep and central)
> 
> &mdash; <cite>nLab</cite>


> 카테고리 이론에서 명백하게 가장 중요한 결과 (arguably the most important result in category theory)
> 
> &mdash; <cite>Emily Riehl</cite>


> 많은 이들을 매우 당혹시킨다 (many people find it quite bewildering)
> 
> &mdash; <cite>Tom Leinster</cite>

요네다 보조정리는 다음과 같다.
함자 $$F:C\rightarrow D$$와 자연변환 $$\eta: C(x, -)\Rightarrow F$$가 주어졌을 때, $$[C, D](C(x, -), F)=Fx$$이다

이 관찰은 대단히 놀라운데, 왜냐하면 좌변은 함자 카테고리의 화살표들의 모임이고, 우변은 함자가 정의된 codomain 카테고리의 점이기 때문이다. 한 카테고리의 점과 다른 카테고리의 화살표의 모임이 "같다"고 얘기하고 있는 것이다.

이 화살표의 모임은 바로, 그 점에서 출발하는 모든 화살표의 모임이다. 즉, 점을 정의하는 것은 곧 그 점과 다른 점의 관계를 정의하는 것과 동치이다.

To be written