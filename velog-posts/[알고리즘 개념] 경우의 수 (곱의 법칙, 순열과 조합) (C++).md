<h1 id="경우의-수">경우의 수</h1>
<p>어떤 일이나 사건이 일어날 수 있는 경우의 가짓 수를 표현한다.
이 경우의 수를 구하는 방법은 크게 세가지가 있다.</p>
<ul>
<li>곱의 법칙</li>
<li>조합 (n개중 r개를 순서 <strong>상관없이</strong> 뽑는 경우)</li>
<li>순열 (n개중 r개를 순서 <strong>상관있이</strong> 뽑는 경우)</li>
</ul>
<h2 id="곱의-법칙">곱의 법칙</h2>
<p>어떤 상황이 발생할 수 있는 가능한 경우를 구할때 곱하기를 하면 된다.</p>
<h3 id="예시">예시</h3>
<p><a href="https://www.acmicpc.net/problem/9375">https://www.acmicpc.net/problem/9375</a>
위 문제는 패션왕 신해빈이란 문제이다.
모자, 안경, 상의 등 카테고리가 나눠져 있고,
아무것도 안입고 나가는 경우를 제외하고 가능한 경우를 전부 구해야한다.</p>
<p>예를 들어, 모자가 3개, 안경이 2개 주어졌다면,
모자 1만 쓰는 경우도 있고,
모자 2와 안경 1을 쓰는 경우도 있을 것이다.
그래서 모든 경우의 수를 구하자면 (4*3)-1이 되는 것이다.</p>
<p>왜냐하면, 모자가 3개가 있지만, 모자를 안쓰는 경우도 있기 때문에 4개의 경우가 있는 것이다.
안경도 마찬가지로 안쓴는 경우가 있기 때문에 3개의 경우가 있다.
그래서 3*4를 하면, 모든 경우의 수가 나오고, 그 중에서 아무것도 안입는 경우의 수 1을 뺴면 된다.</p>
<hr />
<h2 id="조합">조합</h2>
<p>조합은 순서가 없는 뽑기이다.
예를들어, 1,2,3 세개의 숫자 중 두개를 순서 고려 없이 뽑아야한다면,
1,2 / 2,3/ 1,3 이 세가지의 경우가 있다.
만약, 뽑히는 순서가 고려된다면 1,2/ 2,1이 다른 경우가 되기 때문에, 1,2/ 2,1/ 2,3/ 3,2/ 1,3/ 3,1 이렇게 6가지의 경우가 된다.</p>
<p>조합은 두가지 방법으로 구현이 가능하다.</p>
<ul>
<li>반복문</li>
<li>재귀함수</li>
</ul>
<p>뽑아야하는 개수가 적을때는 반복문으로 구현해도 된다.
하지만, 중첩반복문을 사용하기때문에 4개, 5개.. 점점 많아질수록 시간복잡도가 높아지기 때문에 뽑아야하는 개수가 많아지면 재귀함수를 써야한다.</p>
<h3 id="예시코드---반복문">예시코드 - 반복문</h3>
<pre><code class="language-C++">#include &lt;iostream&gt; 
#include &lt;vector&gt; 

using namespace std; 
vector&lt;int&gt; v{ 1,2,3,4,5 }; 
int n = v.size(); 

int main() // 5개 중에 3개는 경우 전부 출력
{ 
    for (int i = 0; i &lt; n; i++) 
    { 
        for (int j = 0; j &lt; i; j++) // for(int j = i+1; j&lt;n; j++) 도 가능
        {  
            for (int k = 0; k &lt; j; k++) // for(int k = j+1; k&lt;n; k ++) 
            { 
               cout &lt;&lt; i &lt;&lt; &quot; &quot; &lt;&lt; j &lt;&lt; &quot; &quot; &lt;&lt; k &lt;&lt; '\n'; 
            } 
        } 
    } 
    return 0; 
}</code></pre>
<p>이런 식으로 3개를 뽑는다면 for문을 3개를 써야한다.
그런데, 그 이상으로 더 많은 개수를 뽑는다면 for문을 더 많이 중첩해야한다.
그래서 재귀함수로 작성하는 방법을 익히는 것을 권장한다.
한 두개 뽑는 경우라면 괜찮다.</p>
<h3 id="예시코드---재귀함수">예시코드 - 재귀함수</h3>
<pre><code>#include &lt;iostream&gt; 
#include &lt;vector&gt; 
#include &lt;algorithm&gt; 

using namespace std; 
int n = 5; 
int r = 3; 
vector&lt;int&gt; v; 

void print(vector&lt;int&gt; a) 
{ 
    for (int i = 0; i &lt; a.size(); i++) 
    { 
        cout &lt;&lt; a[i] &lt;&lt; &quot; &quot;; 
    } 
    cout &lt;&lt; '\n'; 
} 

void combi(int index, vector&lt;int&gt; a) 
{ 
    if (a.size() == r) 
    { 
        print(a); // logic 
        return; 
    } 
    for (int i = index + 1; i &lt; n; i++) 
    { 
        a.push_back(i); 
        combi(i, a); 
        a.pop_back(); 
    } 
} 

int main() 
{ 
    combi(-1, v); 
    return 0; 
}</code></pre><p>재귀함수를 작성할때 항상 고려해야하는 것은 <strong>기저사례</strong>이다.
combi 함수에서 기저사례는 <strong>a 벡터의 크기가 r일때</strong>이다.
즉, n개 중에 r개를 뽑는 상황에서, r개를 다 뽑았을 때 logic을 실행시키는 것이다.</p>
<p>a 벡터를 채우는 것은 for문에서 확인할 수 있다.</p>
<ol>
<li>i를 push_back하고, (원하는 값을 채우고)</li>
<li>재귀함수 호출하고</li>
<li>원상복구 시킨다.</li>
</ol>
<p>⚠️ <strong>주의 사항</strong></p>
<ul>
<li>main에서 combi함수를 처음 부를때 <strong>첫번째 인자에 -1을</strong> 넣는 것이 특징이다.</li>
<li>combi함수에서 for문에서 사용할 i를 선언할때, <strong>int i = index +1</strong> 로 선언해야한다.</li>
</ul>
<hr />
<h2 id="순열">순열</h2>
<p>순열은 순서를 고려한 뽑기이다.
어떤 것을 먼저 뽑느냐 또한 경우를 나누는 기준이 되는 것이다.</p>
<p>순열 또한 두가지 방법으로 구현이 가능하다.</p>
<ul>
<li>next_permutation 함수 사용하기</li>
<li>재귀함수</li>
</ul>