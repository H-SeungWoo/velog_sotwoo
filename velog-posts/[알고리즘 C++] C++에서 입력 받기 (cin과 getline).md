<h2 id="입력받기">입력받기</h2>
<p>C++에서는 입력받는 방법이 다음과 같다.</p>
<ul>
<li>scanf</li>
<li>cin</li>
<li>getline</li>
</ul>
<p>이 중에서 scanf를 제외하고, <strong>cin과 getline</strong>에 대해 알아보겠다.</p>
<h3 id="💡cin">💡cin</h3>
<p>cin은 </p>
<ul>
<li>iosteam 헤더 파일을 불러와야 사용할 수 있다.</li>
<li><code>&gt;&gt;</code>피연산자와 같이 사용한다.</li>
</ul>
<p>사용 예시를 바로 알아보겠다.</p>
<pre><code class="language-C++">#include &lt;iostream&gt;

using namespace std;
string name;
int main(){
    cin &gt;&gt; name;
    return 0;
}</code></pre>
<p>위 처럼 사용하게 되면, 콘솔창에 사용자가 입력한 값이 name에 저장된다.</p>
<hr />
<p>하지만, 띄어쓰기가 포함되어 있다면 cin을 사용하기 애매해진다.</p>
<pre><code>string s;

cin &gt;&gt; s;
cout &lt;&lt; s &lt;&lt; endl;

/*입력
가나다라 마바사

출력
가나다라
*/</code></pre><p>위 처럼 s에 <code>가나다라 마바사</code>를 저장하고 싶었지만, 띄어쓰기 전까지만 입력되어서 <code>가나다라</code>만 저장이 된다.
아래처럼 하면 모든 입력을 받을 수 있긴하다.</p>
<pre><code>string s, r;

cin &gt;&gt; s &gt;&gt; r;
cout &lt;&lt; s &lt;&lt; &quot; &quot; &lt;&lt; r &lt;&lt; '\n';

/*입력
가나다라 마바사

출력
가나다라 마바사
*/</code></pre><p>하지만, 이렇게 되면 변수를 띄어쓰기마다 선언해줘야하는 문제점이 있다.
그래서 getline을 사용하면, 이 문제가 해결이 된다.</p>
<h3 id="💡getline">💡getline</h3>
<p>getline의 사용예시를 바로 살펴보겠다.</p>
<pre><code>#include &lt;iostream&gt; 
#include &lt;string&gt; //getline함수를 사용하기 위해 string 클래스를 가져옴. 

using namespace std; 
string s; 
int main()
{ 
    getline(cin, s); 
    cout &lt;&lt; s &lt;&lt; endl; 
    return 0; 
}</code></pre><p>getline의 첫번째 인자로 cin을 넣어주고, 두번째 인자로 저장시킬 변수를 넣어준다.
s에는 띄어쓰기를 포함한 문자열이 저장된다.
(위의 예시로 따지자면, <code>가나다라 마바사</code>가 통째로 저장된다.)</p>
<hr />
<h3 id="⚠️-getline을-n번-사용할-때-주의점">⚠️ getline을 n번 사용할 때 주의점</h3>
<p>문자열을 n번 입력받아야하는 상황이 있을 수 있다.
이럴때 보통 n을 먼저 입력받는데, n은 cin을 통해 입력을 받을 것이다.</p>
<p>그런데 cin으로 입력을 받으면, 개행문자 직전까지 처리하기 때문에 입력 버퍼에 '\n'(개행문자)가 남게된다.
그래서 cin 사용 후 getline을 사용하려면 입력버퍼에 남아있는 개행문자를 처리하도록 코드를 구성해야한다.</p>
<pre><code>#include &lt;iostream&gt; 
#include &lt;string&gt; 
int n; 
string s; 
int main()
{ 
    cin &gt;&gt; n; 
    string bufferflush; 
    getline(cin, bufferflush); 
    for(int i = 0; i &lt; n; i++)
    { 
        getline(cin, s); 
        cout &lt;&lt; s &lt;&lt; endl; 
    } 
    return 0; 
}</code></pre><p>위 코드를 보면 <code>string형 변수인 bufferflush</code>를 통해 getline을 한번 받아준다.
이는 개행문자를 처리하기 위한 작업이다.</p>
<p>위 코드의 메인함수의 흐름은 다음과 같다:</p>
<ol>
<li><p>cin으로 입력이 반복되는 횟수를 받는다.</p>
</li>
<li><p>bufferflush를 통해 버퍼에 남아있는 '\n'을 제거해준다.</p>
</li>
<li><p>for문을 통해 n번 반복해서 입력을 받는다.</p>
</li>
</ol>