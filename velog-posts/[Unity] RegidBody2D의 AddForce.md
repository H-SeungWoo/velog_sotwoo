<h3 id="공식문서">공식문서:</h3>
<p><a href="https://docs.unity3d.com/kr/2022.3/ScriptReference/Rigidbody2D.AddForce.html">https://docs.unity3d.com/kr/2022.3/ScriptReference/Rigidbody2D.AddForce.html</a></p>
<h2 id="regidbody2daddforce">RegidBody2D.AddForce</h2>
<p>RegidBody2D에서 AddForce의 선언은 다음과 같이 되어있다.</p>
<pre><code class="language-C#">public void AddForce (Vector2 force, ForceMode2D mode= ForceMode2D.Force);</code></pre>
<p>첫번째 인자인 force에는 얼마나 세게 힘을 줄 것인지, 그 값을 넣어주면 된다.
두번째 인자인 mode에는 어떤 Mode로 힘을 줄 것인지 적어주면된다.
<strong>(참고, RegidBody의 mode와 RegidBody2D에 mode는 차이가 있음)</strong></p>
<hr />
<p>2D이기 때문에, X축 또는 Y축에만 힘을 줄 수 있다. (Z축에는 힘을 줄 수 없음)</p>
<blockquote>
<p>힘 = 질량 X 가속도</p>
</blockquote>
<p>위 법칙에 따라, 힘이 가해진다.
질량이 높을수록 더 많은 힘을 주어야 빠른 속도를 내게할 수 있다.</p>
<hr />
<h2 id="forcemode2d">ForceMode2D</h2>
<p>mode의 자료형인 ForceMode2D는 다음처럼 선언된 enum이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/tmddn131/post/4bbd3128-40ae-4ca6-b7b9-b12ee1871d4d/image.png" /></p>
<p>즉, Force혹은 Impulse 둘 중에 하나를 넣으면 되는 것이다.</p>
<hr />
<h3 id="forcemode2dforce">ForceMode2D.Force</h3>
<p>해당 RegidBody의 질량을 이용해서,
매 FixedUpdate에서 일정 시간동안 힘을 가한다.</p>
<p>현실세계와 더 가깝게 보이기 위해서 연속적인 힘을 줄 때 사용한다.</p>
<hr />
<h3 id="forcemode2dimpulse">ForceMode2D.Impulse</h3>
<p>해당 RegidBody의 질량을 이용해서,
임펄스 힘을 즉시 준다.</p>
<p>폭발, 충돌 등과 같이 짧은 순간에 힘을 가할때 사용한다.</p>
<hr />
<h3 id="비교">비교</h3>
<p>공통점: 둘다 물체의 질량을 이용해서 힘을 가한다는 특징이 있다.
차이점: 순간적으로 힘을 가하느냐 아니냐의 차이.</p>