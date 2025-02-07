<h1 id="💡-누적합">💡 누적합</h1>
<p>누적합이란, 누적된 합이 담긴 배열을 활용하는 것을 말한다.</p>
<p>앞에서부터 더하는 <strong>prefix sum</strong>과 뒤에서부터 더하는 <strong>suffix sum</strong>
두가지 방법이 있는데, 여기서는 prefix sum만을 다룬다.
prefix sum을 줄여 psum이라고 많이 사용하는 것 같다.</p>
<blockquote>
</blockquote>
<p>한가지 예를 들어보자면, 홀수를 누적합한 배열을 구하고 싶다.
그렇다면 
psum[1] = 1 
psum[2] = 1+3
psum[3] = 1+3+5
이런식으로 구성될 것이다.
<img alt="" src="https://velog.velcdn.com/images/tmddn131/post/0a36714a-f564-4b62-83e3-73daef2ade5a/image.jpg" />
위와 같이, 앞에서부터 차근차근 더해 배열에 저장해두는 기법이다. 
(기본적으로 배열의 0번째 인덱스는 비워둔다.)</p>
<h1 id="🔢-구간합-쿼리">🔢 구간합 쿼리</h1>
<p>구간합 쿼리는 특정 구간에 대한 합을 구하는 알고리즘 개념이다.
단순하게 배열을 순차적으로 탐색하며 구간의 합을 구할수도 있지만, 더 빠르게 구하기 위해선</p>
<ul>
<li>누적합</li>
<li>트리 (세그먼트, 펜윅트리)</li>
</ul>
<p>를 사용한다.</p>
<p>그 구간안에 있는 요소들이 <strong>변하지 않는 정적 요소</strong>라면 누적합을 쓴다.
(요소들이 동적이면 누적합을 쓸 수가 없다. 이럴땐 트리 사용)</p>
<h2 id="구간쿼리에서-누적합-활용">구간쿼리에서 누적합 활용</h2>
<p>만약, 세번째 홀수에서 다섯번째 홀수까지의 합을 구하고 싶다면, 다음 처럼 하면 된다.
<img alt="" src="https://velog.velcdn.com/images/tmddn131/post/64b0c069-f194-4fbc-b2f7-910531825322/image.jpg" /></p>
<p>psum[5]는 처음부터 다섯번째까지, psum[2]는 처음부터 두번째까지 누적해서 더했으므로,
psum[5] - psum[2]를 해주면, 세번째에서 다섯번째까지 더한 값을 구할 수 있다.</p>
<h1 id="✍🏻-누적합과-구간쿼리-구현">✍🏻 누적합과 구간쿼리 구현</h1>
<p>이제 누적합을 코드로 구현해보겠다.</p>
<ol>
<li>누적합을 psum 배열에 구현한 한다.</li>
<li>psum의 차를 활용해 구간합 쿼리를 구한다.
이 순서로 구현해보겠다.</li>
</ol>
<pre><code>#include &lt;bits/stdc++.h&gt;

using namespace std;

int psum[7]
int main()
{    
    // 1.누적합을 psum 배열에 구현한다.
    for(int i=1; i&lt;=psum.length(); i++)
    {
        psum[i] = psum[i-1] + (i*2-1);
    // 현재 인덱스 값 = 전 인덱스 값 + 추가할 값(여기서는 홀수)
    }

    // 2. psum의 차를 활용해 구간합 쿼리를 구한다.
    cout &lt;&lt; psum[5]-psum[2] &lt;&lt; '\n';
}</code></pre><p>여기서 psum을 구현할때, <strong>인덱스를 1부터 시작하는 것이 좋다.</strong>
0부터 시작하게 되면, psum[i-1]이 애매해진다.
<strong>1부터 시작했으므로, 종결조건에는 등호를 붙여준다.</strong></p>
<hr />
<p>이번에는 입력을 받는 형태의 코드를 작성해보겠다.</p>
<p>n개의 수를 입력받아 구간쿼리를 m번동안 구해보겠다.
이때 구간은 b~c의 구간의 합을 구해보겠다.</p>
<pre><code>#include&lt;bits/stdc++.h&gt;

using namespace std;

int a[1000004], b, c, psum[1000004], n, m;
int main(){
    // n: 입력받을 숫자의 개수, m: 구간합쿼리 반복횟수
    cin &gt;&gt; n &gt;&gt; m;
    for(int i=1; i&lt;=n; i++)
    {
        cin &gt;&gt; a[i];
        psum[i] = psum[i-1] + a[i];
    }

    for(int i=0; i&lt;m; i++)
    {
        cin &gt;&gt; b &gt;&gt; c;
        cout &lt;&lt; psum[c] - psum[b-1] &lt;&lt; '\n';
    }

    return 0;

    /* 입력예시
    6 3
    1 3 5 7 8 11
    3 5
    1 5
    3 6 */

    /* 출력
    21
    25
    32 */    

}</code></pre><p><img alt="" src="https://velog.velcdn.com/images/tmddn131/post/9d086729-c1b9-4131-902d-d6d6441ad1b1/image.png" /></p>
<p>여기서 놓치기 쉬운 부분은
<strong>구간합을 구할때 psum[b-1]을 빼줘야한다는 것이다.</strong>
3<del>5의 구간을 구할때, psum[5] - psum[3]을 해버리면 4</del>5구간을 구하게 된다.
psum[5]-psum[3-1]를 해야 3~5구간을 구할 수 있다.</p>