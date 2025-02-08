<p>문자열 -&gt; 정수 변환에는 크게 두가지가 있다.</p>
<ul>
<li>stoi</li>
<li>atoi</li>
</ul>
<h2 id="stoi-string-to-int">stoi (string to int)</h2>
<p><code>std::stoi(const std::string&amp; str, std::size_t* pos = 0, int base = 10)</code></p>
<p>문자열을 정수로 변환해주는 함수이다.</p>
<blockquote>
</blockquote>
<p>첫번째 인자 : 변환시킬 문자열을 넣는다.
두번째 인자 : 변환이 성공한 부분 이후의 인덱스(pos)를 저장할 수 있다. 
세번째 인자 : 2,8,10,16 등의 수를 넣어 진법을 지정해줄 수 있다.</p>
<p><strong>사용 예시</strong></p>
<pre><code>#include &lt;iostream&gt;
#include &lt;string&gt;

using namespace std
int main() {
    string str = &quot;12345&quot;;
    int num = std::stoi(str);
    cout &lt;&lt; &quot;변환된 숫자: &quot; &lt;&lt; num &lt;&lt; std::endl;
    return 0;
}</code></pre><blockquote>
<p><strong>출력</strong>
변환된 숫자: 12345</p>
</blockquote>
<p>⚠️<strong>숫자가 포함되지 않은 문자열은 변환이 되지 않는데 이때 예외가 발생한다.</strong></p>
<h3 id="자매품-stol-stoll-string-to-long-string-to-long-long">자매품 stol, stoll (string to long, string to long long)</h3>
<p><code>stoi</code>와 동일하지만, <code>long</code> 또는<code>long long</code> 타입으로 변환한다.</p>
<h3 id="pos-활용하기">pos 활용하기</h3>
<p>pos는 변환이 완료된 문자열의 끝 위치를 저장하는 포인터(<code>std::size_t*</code>)이다.</p>
<p>stoi는 변환할 수 있는 숫자까지만 변환하고, 변환이 끝난 위치를 pos에 저장한다.</p>
<pre><code>#include &lt;iostream&gt;
#include &lt;string&gt;

using namespace std;

int main() {
    string str = &quot;123abc&quot;;  // 숫자 + 문자
    size_t pos;  // 변환이 끝난 위치를 저장할 변수

    int num = stoi(str, &amp;pos);  // &quot;123&quot;은 변환 가능, &quot;abc&quot;는 변환 불가능

    cout &lt;&lt; &quot;변환된 숫자: &quot; &lt;&lt; num &lt;&lt; '\n';
    cout &lt;&lt; &quot;변환된 끝 위치: &quot; &lt;&lt; pos &lt;&lt; '\n';  // &quot;123&quot;의 다음 위치인 3이 출력됨

    return 0;
}</code></pre><blockquote>
<p><strong>출력</strong>
123
3</p>
</blockquote>
<p>이를 활용해서 문자열 처리를 해줄 수 있다.</p>
<pre><code>#include &lt;iostream&gt;
#include &lt;string&gt;

using namespace std;

int main() {
    string str = &quot;42 is the answer&quot;;
    size_t pos;

    int number = stoi(str, &amp;pos);  // &quot;42&quot; 변환 후, pos = 2 (공백 전까지 변환)

    string remaining = str.substr(pos);  // 남은 문자열 추출

    cout &lt;&lt; &quot;숫자: &quot; &lt;&lt; number &lt;&lt; '\n';
    cout &lt;&lt; &quot;남은 문자열: \&quot;&quot; &lt;&lt; remaining &lt;&lt; &quot;\&quot;&quot; &lt;&lt; '\n';

    return 0;
}</code></pre><blockquote>
<p><strong>출력</strong>
숫자: 42
남은 문자열: &quot; is the answer&quot;</p>
</blockquote>
<p>다만, 문자열이 숫자로 시작하지 않는다면, 바로 예외를 발생시킨다.</p>
<p>만약 첫번째 숫자 부분을 찾아서 변환을 시작하고 싶다면, stoi를 바로 사용하는 것이 아닌 전처리 과정을 거치는 것이 좋다.</p>
<pre><code>#include &lt;iostream&gt;
#include &lt;string&gt;
#include &lt;cctype&gt;  // isdigit() 사용

using  namespace std;

int main() {
    string str = &quot;abc123def&quot;;
    size_t pos = str.find_first_of(&quot;0123456789&quot;);  // 숫자가 처음 나오는 위치 찾기

    if (pos != string::npos) {  // 숫자가 있는 경우만 변환
        int num = stoi(str.substr(pos));  // 숫자가 시작하는 부분부터 변환
        cout &lt;&lt; &quot;변환된 숫자: &quot; &lt;&lt; num &lt;&lt; '\n';
    } else {
        cout &lt;&lt; &quot;변환할 숫자가 없음&quot; &lt;&lt; '\n';
    }

    return 0;
}</code></pre><blockquote>
<p><strong>출력</strong>
변환된 숫자: 123</p>
</blockquote>
<hr />
<h2 id="atoiascii-to-int">atoi(ASCII to int)</h2>
<p><code>int atoi(const char* str)</code>
C 스타일의 문자열 (char <em>)을 int로 변환한다.
⚠️ stoi와 다르게 예외처리가 없으며, *</em>변환 실패시 0을 반환한다.**</p>
<p><strong>사용 예시</strong></p>
<pre><code>#include &lt;iostream&gt;
#include &lt;cstdlib&gt;  // atoi 포함

using namespace std
int main() {
    const char* str = &quot;123&quot;;
    int num = atoi(str);
    cout &lt;&lt; &quot;변환된 숫자: &quot; &lt;&lt; num &lt;&lt; '\n';
    return 0;
}</code></pre><blockquote>
<p><strong>출력</strong>
변환된 숫자: 123</p>
</blockquote>
<h3 id="string-형을-char-형으로-변환하기">string 형을 char* 형으로 변환하기</h3>
<p>C++에서는 문자열을 string 형으로 주로 사용한다.
하지만, <strong>atoi를 쓰기 위해서는 인자가 char* 이어야하기 때문에</strong> 변환해야한 필요가 있다.</p>
<p>이럴땐 string 클래스의 <code>c_str()</code> 메소드를 사용하면 된다. (C++17부터는 data()도 동일한 동작을 함.)</p>
<p><strong>사용 예시</strong></p>
<pre><code>#include &lt;iostream&gt;
#include &lt;string&gt;

int main() {
    std::string str = &quot;Hello, World!&quot;;
    const char* cstr = str.c_str();  // 변환

    std::cout &lt;&lt; &quot;변환된 문자열: &quot; &lt;&lt; cstr &lt;&lt; std::endl;
    return 0;
}</code></pre><blockquote>
<p><strong>출력</strong>
변환된 문자열: Hello, World!</p>
</blockquote>
<p>c_str()을 사용하면 메모리를 직접 할당할 필요가 없지만, 객체가 살아있는 동안에만 사용이 가능하다.
이 객체가 변경되거나 소멸되면 포인터는 더 이상 유효하지 않게 된다.</p>
<h3 id="✍️-atoi-활용하기">✍️ atoi 활용하기</h3>
<p>알고리즘 문제를 풀다보면 입력을 int와 string으로 두가지를 구별해야할 때가 있다.</p>
<p>그럴때, atoi를 활용하면 쉽게 구별할 수 있다.</p>
<p><strong>사용 예시</strong></p>
<pre><code>#include&lt;bits/stdc++.h&gt;

using namespace std;

string str_or_int;

int main()
{        
    for(int i=0; i&lt;2; i++)
    {
        cin&gt;&gt; str_or_int;
        if(atoi(str_or_int.c_str()) == 0) 
        cout &lt;&lt; &quot;str: &quot; &lt;&lt; str_or_int &lt;&lt; '\n';
        else 
        cout &lt;&lt; &quot;int: &quot;&lt;&lt; atoi(str_or_int.c_str()) &lt;&lt; '\n';
    }

    return 0;
}</code></pre><blockquote>
<p><strong>입력</strong>
abc
123</p>
</blockquote>
<p><strong>출력</strong>
str: abc
int: 123</p>
<p>여기서 if(atoi(str_or_int.c_str())==0) 조건문을 살펴보면,
str_or_int가 &quot;abc&quot;인 경우에 atoi가 0을 반환해서 조건에 걸린 것을 볼 수 있다.
stoi는 예외를 발생시키기 때문에 프로그램이 종료되는 반면, atoi는 이렇게 활용할 수 있다는 장점이 있다.</p>
<hr />
<h3 id="관련문제">관련문제</h3>
<p><a href="https://www.acmicpc.net/problem/1620">https://www.acmicpc.net/problem/1620</a></p>