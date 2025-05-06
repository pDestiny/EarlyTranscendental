# 1.4 극한 셈

## 극한 법칙
1. 합의 극한 법칙 : $\lim_{x\rightarrow a}\{f(x) + g(x)\} = \lim_{x \rightarrow a}f(x) + \lim_{x \rightarrow a}g(x)$
2. 차의 극한 법칙 : $\lim_{x\rightarrow a}\{f(x) - g(x)\} = \lim_{x \rightarrow a}f(x) - \lim_{x \rightarrow a}g(x)$
3. 상수 배의 극한 법칙 : $\lim_{x\rightarrow a}\{cf(x)\} = c\lim_{x \rightarrow a}f(x)$
4. 곱의 극한 법칙 : $\lim_{x\rightarrow a}\{f(x)\cdot g(x)\} = \lim_{x \rightarrow a}f(x) \cdot \lim_{x \rightarrow a}g(x)$
5. 몫의 극한 법칙 : $\lim_{x\rightarrow a}\frac{f(x)}{g(x)} = \frac{\lim_{x \rightarrow a}f(x)}{\lim_{x \rightarrow a}g(x)}$ (단, $\lim_{x\rightarrow a}g(x) \neq 0$)
* 보기 1 - (a)

```julia
using Symbolics

# f = 2x^2 - 3x + 4
# 극한 법칙에 따르면 합의 극한법칙과, 차의 극한 법칙, 상수배의 극한법칙, 곱의 극한법칙을 이용하여 잘게 쪼갤 수 있다.
# lim f = 2(limx)^2 - 3limx + 4

@syms x

f = 2x^2 - 3x + 4

a = 2x^2
b = 3x
c = 4

Symbolics.limit(f, x, 5) # 39
limit(a, x, 5) - limit(b, x, 5) + limit(c, x, 5) # 39
```

* 보기 1 - (b)

```julia
@syms x
f = (x^3 + 2x^2 - 1) / (5 - 3x)

limit(f, x, -2) # 1/11 이 나옴

a = x^3 + 2x^2 -1
b = 5-3x

limit(a, x, -2) / limit(b, x, -2) # -1 / 11 이 나옴

# 단 lim b(x) 가 0 이 아니어야 함.
```

> **직접 대입 성질** : f가 다항 함수 또는 유리함수이고 a 가 f의 정의역에 속한다면, 다음의 성질이 성립한다.
$$\lim_{x\rightarrow a}f(x) = f(a) $$

**유리 함수란?**

유리 함수(rational function)란, 두 다항식(polynomial) P(x)와 Q(x)의 몫으로 정의되는 함수입니다. 즉
$f(x) = \frac{P(x)}{Q(x)},\quad Q(x)\neq 0$
꼴을 이루며, 그 정의역은 분모 Q(x)가 0이 되지 않는 모든 실수(또는 복소수) x 입니다.
* 형태
* 분자 P(x)와 분모 Q(x)는 각각
$P(x) = a_n x^n + \cdots + a_1 x + a_0,\qquad$
$Q(x) = b_m x^m + \cdots + b_1 x + b_0$
의 다항식입니다.
	•	예:
$f(x) = \frac{2x^3 - x + 5}{x^2 - 4},\quad$
$g(x) = \frac{x+1}{3},\quad$
$h(x) = \frac{1}{x}$
– g(x)는 분모가 상수(3)이므로 사실상 다항식이기도 하고,
– h(x)는 가장 단순한 유리함수입니다.
	•	정의역(domain)
유리함수는 분모가 0이 되는 점에서는 정의되지 않습니다.

$\mathrm{Dom}(f) = \{\,x\mid Q(x)\neq 0\}$.
•	성질
1. 다항식은 분모가 상수인 유리함수의 특별한 경우입니다.
2. 두 유리함수의 덧셈·뺄셈·곱셈·나눗셈 또한 유리함수입니다.
3. 분모가 0에 가까워질 때 함수값이 무한대로 발산하는 ‘극점(pole)’이 존재할 수 있습니다.

예시
```julia
using Symbolics

@syms x

P = 2x^3 - x + 5
Q = x^2 - 4
f = P/Q

# x → 2 근처에서의 극한
Symbolics.limit(f, x, 2)  # +∞ 또는 −∞ 로 발산

```

이렇게, 유리함수는 “다항식들의 나눗셈”으로 이루어진 함수군을 말합니다.

**유리 함수가 아닌 경우**

유리함수가 아닌 주요 예시를 몇 가지 유형으로 정리하면 다음과 같습니다.

1.	초월 함수(transcendental functions)
* 지수 함수: $f(x)=e^x, 2^x$
* 로그 함수: $f(x)=\ln x, \log_{10}x$
* 삼각 함수: $f(x)=\sin x, \cos x, \tan x$ 등

→ 이들 함수는 다항식의 비(比) 꼴로 표현될 수 없습니다.
1. 유리수가 아닌 지수(분수·무리 지수)
    * $f(x)=x^{1/2}=\sqrt{x}, x^{\pi}$ 등
→ 분수가 지수에 들어가면 다항식이 아니므로, 분수 다항식의 몫으로도 나타낼 수 없습니다.
2.	루트(근호) 표현이 포함된 대수 함수(algebraic but non-rational)
    * $f(x)=\sqrt{x^2+1}, f(x)=\sqrt[3]{x+2}$

→ 대수적(algebraic) 함수이지만, 다항식 몫의 형태로 간단히 표현할 수 없는 경우입니다.

3.	절댓값·계단 함수 등 특수 함수
    * $f(x)=|x|$
    * $f(x)=\lfloor x\rfloor (바닥 함수), \lceil x\rceil$ (천장 함수)
→ 분리된 정의(domains)나 불연속성을 가지므로 유리함수가 아닙니다.
4. 조합 함수 중 분모·분자에 위 함수를 포함한 경우
    * 예: $\displaystyle f(x)=\frac{\sin x}{x+1}, \frac{x}{\sqrt{x}+1}$
→ 전체가 유리함수 꼴이 될 수 없습니다.

⸻

요약하자면, “다항식(polynomial) 간의 나눗셈”으로 표현되지 않는 모든 함수—즉 초월함수, 분수·무리 지수가 들어간 함수, 근호를 포함한 대수 함수, 절댓값·계단 함수 등—은 유리함수가 아닙니다.

* 보기 2
다음 값을 찾아라
$$\lim_{x \rightarrow 1} \frac{x^2 - 1}{x - 1}$$

$$\begin{align}
f(x) &= \frac{x^2 -1}{x-1} \\
&= \frac{(x + 1)(x - 1)}{x - 1} \\
&= x + 1
\end{align}$$

$$ \lim_{x \rightarrow 1}(x + 1) = 2 $$

> $x \neq a$ 일 때 $f(x) = g(x)$ 이고 $x\rightarrow 0$ 일 때 $f(x)$ 와 $g(x)$
의 극한이 존재하면, $\lim_{x\rightarrow a}f(x) = \lim_{x \rightarrow a}g(x)$ 가 성립한다.

- 보기 2 설명
이 성질은 한 점 a 근처에서 두 함수가 똑같이 정의되어 있다면(단, x = a 에서는 다를 수 있지만), 그 점으로 다가갈 때의 극한값도 같다는 뜻입니다. 좀 더 풀어서 보겠습니다.
1.	전제
    * 어떤 열린 구간에서 $x \neq a$ 일 때 항상 $f(x) = g(x)$ 이다.
    * 그리고 $\displaystyle\lim_{x\to a}f(x)$ 와 $\displaystyle\lim_{x\to a}g(x)$ 가 둘 다 존재한다.
2.	극한의 정의(아이디어)
$\displaystyle\lim_{x\to a}f(x)=L$ 이라는 것은, $x$ 가 $a$ 에 “충분히 가까워지면” $f(x)$ 도 “충분히” $L$ 에 가까워진다는 얘기입니다.
즉, 아무리 작은 거리 $\varepsilon>0$ 를 정해도, 어떤 $\delta>0$ 가 있어서 $|x-a|<\delta$ 이면 $|f(x)-L|<\varepsilon$ 이 성립합니다.
3.	함수 일치의 의미
$x\neq a$ 인 상태에서는 언제나 $f(x)=g(x)$ 이므로, $x$ 가 $a$ 에 가까워질 때 살펴볼 값들은 사실상 $f(x)$ 나 $g(x)$ 나 똑같습니다.
    * 즉, $|x-a|<\delta$ 이고 $x\neq a$ 이면
$|f(x) - L| < \varepsilon
\quad\Longrightarrow\quad
|g(x) - L| = |f(x) - L| < \varepsilon$.
4. 결론
위 관찰로부터, g(x) 에 대해서도 “$x\to a$ 이면 $g(x)\to L$” 이 성립함을 알 수 있으므로
$lim_{x\to a}g(x) = L = \lim_{x\to a}f(x)$.

⸻

예시

$f(x) = \frac{x^2 - 1}{x - 1},\quad$
$g(x) = x + 1,\quad$
$a = 1$.
	•	$x\neq 1$ 일 때 $\displaystyle\frac{x^2-1}{x-1} = x+1$, 즉 $f(x)=g(x)$.
	•	f(1) 은 정의되지 않지만,
$\displaystyle\lim_{x\to1}f(x) = \lim_{x\to1}(x+1) = 2$.
	•	따라서 $\displaystyle\lim_{x\to1}g(x)$ 도 똑같이 2 가 됩니다.

이처럼 함수 자체가 a 에서 정의된 값과는 무관하게, a 에 아주 가까워질 때의 “주변 값들”만 같으면 극한도 같아진다는 것이 이 성질의 핵심입니다.

* 보기 3

다음과 같은 함수 $g$ 에 대해 $\lim_{x\to1}g(x)$를 찾아라

$$g(x) = \begin{cases}
    x + 1\quad (x \neq 1) \\
    \pi \quad(x = 1)
\end{cases}$$

$$\lim_{x\to1}g(x) = \lim_{x\to1}(x + 1) = 2 \therefore \lim_{x\to1}g(x) = 2$$

* 보기 4

$$\lim_{h \to 0}\frac{(3 + h)^2 - 9}{h}$$

의 값을 찾아라.

$$\begin{align}
\frac{(3 + h)^2 -9}{h} &= \frac{\{(3 + h) + 3\}\{(3 + h) - 3\}}{h} \\
&= \frac{h(h + 6)}{h} \\
&= (h + 6)
\end{align}$$

$$\begin{align} 
\lim_{h\to0}\frac{(3 + h)^2 -9}{h} &= \lim_{x \to 0}(h + 6)\\
&= 6
\end{align}$$

$$\therefore \lim_{h\to0}\frac{(3 + h)^2 -9}{h} = 6$$


* 보기 5
다음 값을 찾아라

$$\lim_{t \to 0}\frac{\sqrt{t^2 + 9} - 3}{t^2}$$

**풀이**

$$\begin{align}
\lim_{t \to 0}\frac{\sqrt{t^2 + 9} - 3}{t^2} &= \lim_{t \to 0}\frac{\sqrt{t^2 + 9} - 3}{t^2}\cdot\frac{\sqrt{t^2 + 9} + 3}{\sqrt{t^2 + 9} + 3} \\
&= \lim_{t \to 0}\frac{(t^2 + 9) - 9}{t^2(\sqrt{t^2 + 9} + 3)} = \lim_{t\to0}\frac{1}{\sqrt{t^2 + 9} + 3} \\
&= \frac{1}{\sqrt{\lim_{t\to0}(t^2 + 9)} + 3} = \frac{1}{6} 
\end{align}$$

어떤 극한을 셈하는 최선의 방법은 먼저 왼쪽 극한과 오른쪽 극한을 찾는 것이다.

> 정리 $\lim_{x\to a}f(x) = L$이기 위한 필요 충분 조건은 아래와 같다.
> $$\lim_{x \to a}f(x) = L = \lim_{x \to a}g(x)$$

# 1.5 연속

> 다음이 성립할 때 함수 $f$ 는 <span style="color:blue">수 a 에서 연속</span>이라고 한다.
> $$\lim_{x \to a}f(x) = f(a)$$

$f$ 가 $a$ 근방에서 정의되어 있을 때\[바꿔말하면, $f$ 가 $a$를 포함하는 열린 구간에서 (기껏해야 $a$를 제외하고)정의되어 있을때\], $f$가 $a$에서 연속이 아니면 $f$는 $a$에서 연속이 아니다.

* 보기 2 - (a)
다음 함수는 어디서 불연속인가?
$$f(x) = \frac{x^2 - x - 2}{x -2}$$

풀이
$f(x)$ 는 $x = 2$ 에서 연속이 이다.

* 보기 2 - (b)
다음 함수는 어디서 불연속인가?
$$f(x) = \begin{cases}
\frac{1}{x^2} \quad (x \neq 0) \\
1 \quad (x = 0)
\end{cases}$$

풀이
연속인 조건은 $x\to a$ 일 때, $\lim_{x\to a}f(x) = f(a)$ 와 같을 경우이다. 만일 x = 0에 한 없이 가까워 질 경우 $\lim_{x\to 0}f(x) = f(0) \neq 1$ 이다. 왜냐하면 $\lim_{x\to 0}\frac{1}{x^2}$의 경우 $\infin$으로 발산하기 때문이다. 따라서 $x$ 는 0에서 연속이 아니다.

* 보기 2 - (c)
