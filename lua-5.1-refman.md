> **Original post: http://www.codingnow.com/2000/download/lua_manual.html**

<!-- saved from url=(0054)http://www.codingnow.com/2000/download/lua_manual.html -->

<!--
<html><div class="oneNoteWebClipperIsInstalledOnThisBrowser" style="display: none;"></div><head><meta http-equiv="Content-Type" content="text/html; charset=GBK">
<title>Lua 5.1 �ο��ֲ�</title>
 
<style id="style-1-cropbar-clipper">/* Copyright 2014 Evernote Corporation. All rights reserved. */
.en-markup-crop-options {
    top: 18px !important;
    left: 50% !important;
    margin-left: -100px !important;
    width: 200px !important;
    border: 2px rgba(255,255,255,.38) solid !important;
    border-radius: 4px !important;
}

.en-markup-crop-options div div:first-of-type {
    margin-left: 0px !important;
}
</style></head>

<body data-feedly-mini="yes">
-->

<hr>
<h1>
Lua 5.1 �ο��ֲ�
</h1>

by Roberto Ierusalimschy, Luiz Henrique de Figueiredo, Waldemar Celes
<p>
�Ʒ� �� <a href="http://www.codingnow.com/">www.codingnow.com</a>

</p><p>
<small>
<a href="http://www.lua.org/copyright.html">Copyright</a>
&#169; 2006 Lua.org, PUC-Rio.  All rights reserved.
</small>
</p><hr>

<!-- ====================================================================== -->
<p>





</p><h1>1 - <a name="1">����</a></h1>

<p>
Lua ��һ����չʽ����������ԣ�������Ƴ�֧��ͨ�õĹ���ʽ��̣��������������������ʩ��
Lua Ҳ�ܶ���������̣�����ʽ��̣���������ʽ����ṩ�ܺõ�֧�֡�
��������Ϊһ��ǿ�������Ľű����ԣ����κ���Ҫ�ĳ���ʹ�á�
Lua ��һ���� <em>clean</em> C д�ɵĿ���ʽ�ṩ������ν Clean C ��ָ�� ANSI C �� C++ �й�ͨ��һ���Ӽ���

</p><p>
��Ϊһ����չʽ���ԣ�Lua û�� "main" ����ĸ����ֻ�� <em>Ƕ��</em> һ�����������й���������������򱻳���
<em>embedding program</em> ����Ϊ <em>host</em> ��
�����������ͨ�����ú���ִ��һС�� Lua ���룬���Զ�д Lua ����������ע�� C ������ Lua ������á�
��Щ��չ�� C ���������Դ�����չ�� Lua ���Դ�����������������Ϳ��Զ��Ƴ��������ԣ�
�����ǹ���һ��ͳһ�ľ䷨��ʽ�Ŀ�ܡ�
Lua �Ĺٷ�������Ͱ�����һ������ <code>lua</code> �ļ򵥵������������� Lua ���ṩ��һ����֤������ Lua ��������


</p><p>
Lua ��һ����������������ʹ�����ɾ����˶�����ʹ�ù���һ��û���κα�֤��
����ֲ��������Ķ�����ʵ�֣������� Lua �Ĺٷ���վ <code>www.lua.org</code> �ҵ���


</p><p>
������������ο��ֲ�һ��������ĵ���Щ�ط��ȽϿ��
���� Lua ������뷨��̽�֣����Կ��� Lua ��վ���ṩ�ļ������ġ�
�й��� Lua ��̵�ϸ�ڽ��ܣ����Զ�һ�� Roberto ���飬<em>Programming in Lua (Second Edition)</em> ��


</p><h1>2 - <a name="2">����</a></h1>

<p>
��һ�ڴӴʷ����﷨���䷨������ Lua ��
���仰˵����һ����������Щ token �����ǣ�����Ч�ģ�������α������������Щ��Ϸ�ʽ��ʲô���塣

</p><p>
�������ԵĹ��ɸ���ó�������չ BNF ����ʽд����Ҳ����������ӣ�
{<em>a</em>} ��˼�� 0 ���� <em>a</em> ��
[<em>a</em>] ��˼��һ����ѡ�� <em>a</em> ��
�����յķ��Żᱣ��ԭ�������ӣ��ؼ��������������� <b>kword</b> ��
�������յķ�����д�� `<b>=</b>�� ��
������ Lua �﷨�����ڱ��ֲ�����ҵ���

</p><h2>2.1 - <a name="2.1">�ʷ�Լ��</a></h2>

<p>
Lua ���õ��� <em>����</em>��Ҳ���� <em>��ʶ��</em>���������κη����ֿ�ͷ����ĸ�����֡��»�����ɵ��ַ�����
����ϼ������б�������й������ֵĶ��塣
����ĸ�Ķ��������ڵ�ǰ������ϵͳ�����ж������ĸ���е���ĸ�����Ա����ڱ�ʶ������
��ʶ��������������������Ϊ����������

</p><p>
����Ĺؼ����Ǳ����ģ������������֣�

</p><pre>     and       break     do        else      elseif
     end       false     for       function  if
     in        local     nil       not       or
     repeat    return    then      true      until     while
</pre>

<p>
Lua ��һ����Сд���е����ԣ�
<code>and</code> ��һ�������֣����� <code>And</code> �� <code>AND</code> ����������ͬ�ĺϷ������֡�
һ��Լ�������»��߿�ͷ����һ����д��ĸ�����֣����� <code>_VERSION</code>������������ Lua �ڲ�ȫ�ֱ�����

</p><p>
������Щ�������� token ��

</p><pre>     +     -     *     /     %     ^     #
     ==    ~=    &lt;=    &gt;=    &lt;     &gt;     =
     (     )     {     }     [     ]
     ;     :     ,     .     ..    ...
</pre>

<p>
�ַ����ȿ�����һ�Ե���������Ҳ������˫���ţ����滹���԰������� C ��ת�����
'<code>\a</code>' �����壩��
'<code>\b</code>' ���˸񣩣�
'<code>\f</code>' ����������
'<code>\n</code>' �����У���
'<code>\r</code>' ���س�����
'<code>\t</code>' �������Ʊ�����
'<code>\v</code>' �������Ʊ�����
'<code>\\</code>' ����б�ܣ���
'<code>\"</code>' ��˫���ţ���
�Լ� '<code>\'</code>' ��������)��
���ң������һ����б�ܺ����һ�������Ļ��з��������������ַ����в���һ�����з���
���ǻ������÷�б�ܼ����ֵ���ʽ <code>\<em>ddd</em></code> ������һ���ַ������
<em>ddd</em> ��һ�������λ��ʮ�������֡���ע�⣬�����Ҫ�����������������һ�������ֵ��ַ���
��ô��б�ܺ����д���������֡���Lua �е��ַ������԰����κ� 8 λ��ֵ�������� '<code>\0</code>' ��ʾ���㡣

</p><p>
ֻ��������Ҫ�Ѳ�ͬ�����š����С���б�ܡ��������������Щ�ַ������ַ���ʱ��
��ű���ʹ��ת���������κ��ַ�������ֱ��д���ı����һЩ���Ʒ����Ի�Ӱ���ļ�ϵͳ���ĳЩ���⣬
���ǲ������� Lua ���κ����⡣��

</p><p>
�ַ�����������һ�ֳ������������ķ�ʽ���塣
���ǰ��������ķ����ż���� n ���ȺŶ���Ϊ�� n ���������š�
����˵��0 �����ĳ�����д�� <code>[[</code> ��
һ�����ĳ�����д�� <code>[=[</code> ����˵ȵȡ�
���ĳ���չҲ�����ƶ��壻
�ٸ����ӣ�4 �����ĳ�����д�� <code>]====]</code> ��
һ�����ַ����������κ�һ�������ĳ����ſ�ʼ�����ɵ�һ��������ͬ�����ĳ����Ž�����
�����ʷ��������̽����ܷ������ƣ��������κ�ת��������Һ��Ե��κβ�ͬ����ĳ����š�
���ַ�ʽ�������ַ������԰����κζ�������Ȼ�ض�����ķ������ų��⡣

</p><p>
��һ��Լ���ǣ������ĳ����ź�����������һ�����з���
������з��Ͳ�����������ַ����ڡ�
�ٸ����ӣ�����һ��ϵͳʹ�� ASCII ��
����ʱ��'<code>a</code>' ����Ϊ 97 �����з�����Ϊ 10 ��'<code>1</code>' ����Ϊ 49 ����
�������ַ�ʽ��������ȫ��ͬ���ַ�����

</p><pre>     a = 'alo\n123"'
     a = "alo\n123\""
     a = '\97lo\10\04923"'
     a = [[alo
     123"]]
     a = [==[
     alo
     123"]==]
</pre>

<p>
���ֳ������Է�������д��ʮ���Ƶ������ֺ�ʮ���Ƶ�ָ�����֡�ָ�������ǿ�ѡ�ġ�
Lua Ҳ֧��ʮ����������������ֻ��Ҫ��ǰ�����ǰ׺ <code>0x</code> ��
������һЩ�Ϸ������ֳ��������ӣ�

</p><pre>     3   3.0   3.1416   314.16e-2   0.31416E1   0xff   0x56
</pre>

<p>
ע�Ϳ����ڳ��ַ����ڵ��κεط��������� (<code>--</code>) ��ʼ��
��������������Ĳ���һ�������ţ������һ����ע�ͣ��������÷�Χֱ����ĩ��
�������һ����ע�ͣ������÷�Χֱ���������ĳ����š�
��ע��ͨ����������ʱ���δ���顣

</p><h2>2.2 - <a name="2.2">ֵ������</a></h2>

<p>
Lua ��һ�� <em>��̬��������</em>��
����ζ�ű���û�����ͣ�ֻ��ֵ�������͡�
�����в��������Ͷ��塣�����е�ֵ����Я�������Լ���������Ϣ��

</p><p>
Lua �е�����ֵ����һ�� (first-class) �ġ�
����ζ�����е�ֵ�����Ա����ڱ���������������ݵ���һ�������У�����������Ϊ������ء�

</p><p>
Lua ���а��ֻ������ͣ�
<em>nil</em>, <em>boolean</em>, <em>number</em>,
<em>string</em>, <em>function</em>, <em>userdata</em>,
<em>thread</em>, and <em>table</em>.
<em>Nil</em> ����ֻ��һ��ֵ <b>nil</b> ��������Ҫ��;���ڱ��ʶ�ͱ���κ�ֵ�Ĳ��죻
ͨ��������Ҫ����һ���������ֵʱ���õ�����
<em>Boolean</em> ����ֻ������ֵ��<b>false</b> �� <b>true</b>��
<b>nil</b> �� <b>false</b> ���ܵ�������Ϊ�٣����������е�ֵ���������档
<em>Number</em> ��ʾʵ����˫���ȸ���������
������һ�������ڲ��������͵� Lua �������Ǽ������׵��£�������ڲ��������͸���
�����ȸ����������͡��μ��ļ� <code>luaconf.h</code> ����
<em>String</em> ��ʾһ���ַ������顣

Lua �� 8-bit clean �ģ�
�ַ������԰����κ� 8 λ�ַ���
����������� ('<code>\0</code>') ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.1">��2.1</a>����


</p><p>
Lua ���Ե��ã��ʹ������� Lua д�ĺ����Լ��� C д�ĺ������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.8">��2.5.8</a>��.


</p><p>
<em>userdata</em> �������������� C ���ݱ����� Lua �����С�
��������൱��һ��ԭ�����ڴ棬���˸�ֵ����ͬ���жϣ�Lua û��Ϊ֮Ԥ�����κβ�����
Ȼ����ͨ��ʹ�� <em>metatable ��Ԫ����</em> ������Ա����Ϊ userdata �Զ���һ�����
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����
userdata ������ Lua �д���������Ҳ������ Lua ���޸ġ������Ĳ���ֻ��ͨ�� C API��
��һ�㱣֤������������ȫ�ƹ����е����ݡ�

</p><p>
<em>thread</em> �����������������ִ���̣߳���������ʵ�� coroutine ��Эͬ���̣����μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.11">��2.11</a>����
��Ҫ�� Lua �̸߳�����ϵͳ���̸߳�졣
Lua ���������е�ϵͳ���ṩ�� coroutine ��֧�֣���ʹϵͳ����֧���̡߳�

</p><p>
<em>table</em> ����ʵ����һ���������顣Ҳ����˵��
����������κζ���������<b>nil</b>���������������������֡�
table �����Բ�ͬ���͵�ֵ���ɣ������԰������е����͵�ֵ���� <b>nil</b> �⣩��
table �� lua ��Ψһ��һ�����ݽṹ����������������ԭʼ�����顢���ű������ϡ�
��¼��ͼ�������ȵȡ�
���ڱ�����¼ʱ��lua ʹ��������Ϊ������
���Ա�������һ���﷨�ǣ�֧���� <code>a.name</code> ����ʽ��ʾ <code>a["name"]</code>��
�кܶ���ʽ������ lua �д���һ�� table ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.7">��2.5.7</a>����

</p><p>
������һ���� table ÿ�����е�ֵҲ�������κ����ͣ��� <b>nil</b>�⣩��
�ر�ģ���Ϊ��������Ҳ��ֵ������ table ������Ҳ���Էź�����
���� table �оͿ�����һЩ <em>methods</em> �� ���μ�see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.9">��2.5.9</a>����

</p><p>
table�� function ��thread ���� (full) userdata ��Щ���͵�ֵ����ν�Ķ���
�������������������Ĵ�����ǵ�ֵ����ֻ�Ƿ���һ���Զ�������á�
��ֵ���������ݣ��������أ����Ƕ���Щ��������ý��в�����
��Щ�������������������κ����ʵĿ�����

</p><p>
�⺯�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-type"><code>type</code></a> ���Է���һ����������ֵ�����͵��ַ�����

</p><h3>2.2.1 - <a name="2.2.1">ǿ��ת��</a></h3>

<p>
Lua �ṩ����ʱ�ַ��������ֵ��Զ�ת����
�κζ��ַ�������ѧ����������᳢����һ���ת�����������ַ���ת����һ�����֡�
�෴�����ۺ�ʱ��һ��������Ҫ��Ϊ�ַ�����ʹ��ʱ�����ֶ����Ժ����ĸ�ʽת��Ϊ�ַ�����
��Ҫ��ȫ������������ת��Ϊ�ַ���������ʹ���ַ������е� <code>format</code> ����
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.format"><code>string.format</code></a>����


</p><h2>2.3 - <a name="2.3">����</a></h2>

<p>
д�ϱ����ĵط���ζ�ŵ����䱣���ֵ�����֮��

Lua �������������ȫ�ֱ������ֲ����������� table ����

</p><p>
һ����һ�����ֿ��Ա�ʾһ��ȫ�ֱ�����Ҳ���Ա�ʾһ���ֲ����� ��������һ�������Ĳ���������һ��������ʽ�ľֲ���������

</p><pre>	var ::= Name
</pre><p>
Name ���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.1">��2.1</a> ��������ı�ʶ����

</p><p>
�κα��������ٶ�Ϊȫ�ֱ�����������ʽ���� local ���ζ��� 
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.7">��2.4.7</a>����
�ֲ������������÷�Χ��
�ֲ��������Ա������������÷�Χ�еĺ�������ʹ��
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.6">��2.6</a>����


</p><p>
�ڱ������״θ�ֵ֮ǰ��������ֵ��Ϊ <b>nil</b>��


</p><p>
�����ű������� table ��������

</p><pre>	var ::= prefixexp `<b>[</b>�� exp `<b>]</b>��
</pre><p>
��ȫ�ֱ����Լ� table ��֮���ʵĺ������ͨ�� metatable ���ı䡣
��ȡһ�������±�ָ����� <code>t[i]</code> �ȼ��ڵ��� <code>gettable_event(t,i)</code>��
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a> ����һ�������Ĺ���
<code>gettable_event</code> ������˵����
���������û���� lua �ж��������Ҳ������ lua �е��á�
�������ǰ����г���ֻ�Ƿ���˵������

</p><p>
<code>var.Name</code> �����﷨ֻ��һ���﷨�ǣ�������ʾ
<code>var["Name"]</code>��

</p><pre>	var ::= prefixexp `<b>.</b>�� Name
</pre>

<p>
���е�ȫ�ֱ������Ƿ���һ���ض� lua table ��������У�����ض��� table
���� <em>environment ��������table</em> ���߼��Ϊ
<em>����</em> ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.9">��2.9</a>����
ÿ���������ж�һ�����������ã�
����һ�������пɼ�������ȫ�ֱ���������������������õĻ�������environment table���С�
��һ����������������������Ӵ������ĺ����м̳��价��������Ե���
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-getfenv"><code>getfenv</code></a> ȡ���价����
�����ı价�������Ե��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-setfenv"><code>setfenv</code></a>��
������ C ��������ֻ��ͨ�� debug �����ı��价����
�μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#5.9">��5.9</a>����

</p><p>
��һ��ȫ�ֱ��� <code>x</code> �ķ���
�ȼ��� <code>_env.x</code>�������ֿ��Եȼ���

</p><pre>     gettable_event(_env, "x")
</pre>

<p>
���<code>_env</code> �ǵ�ǰ���еĺ����Ļ�����
������ <code>gettable_event</code> ������˵���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>��
���������û���� lua �ж��������Ҳ���ܵ��á�
��Ȼ��<code>_env</code> �������Ҳͬ��û���� Lua �ж��������
����������ʹ�����ǣ�����ֻ�Ƿ�����Ͷ��ѡ���


</p><h2>2.4 - <a name="2.4">���Σ�Statement��</a></h2>

<p>
Lua ֧�ֹ�����ʽ�����Σ����� Pascal ���� C ������
������ϰ�����ֵ�����ƽṹ���������ã����б���������

</p><h3>2.4.1 - <a name="2.4.1">Chunk������飩</a></h3>

<p>
Lua ��һ��ִ�е�Ԫ������ <em>chunk</em>��
һ�� chunk ����һ�����Σ����ǻᱻѭ���ִ�С�
ÿ�����ο�����һ���ֺŽ�����

</p><pre>	chunk ::= {stat [`<b>;</b>��]}
</pre><p>
����������пյ����Σ����� '<code>;;</code>' �ǷǷ��ġ�

</p><p>
lua ��һ�� chunk ����һ��ӵ�в�����������������
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.9">��2.5.9</a>��������
����������chunk �ڿ��Զ���ֲ����������ղ��������ҷ���ֵ��

</p><p>
chunk ���Ա�������һ���ļ��У�Ҳ���Ա��������������һ���ַ����С�
��һ�� chunk ��ִ�У��������ᱻԤ�����������е�ָ�����У�
Ȼ�����������������Щָ�


</p><p>
chunk Ҳ���Ա�Ԥ����ɶ�������ʽ��ϸ�ڲο����� <code>luac</code>��
��Դ����ʽ�ṩ�ĳ���ͱ�������Ķ�������ʽ�ĳ����ǿ����໥�滻�ģ�
Lua ���Զ�ʶ���ļ����Ͳ�����ȷ�Ĵ�����


</p><h3>2.4.2 - <a name="2.4.2">����</a></h3><p>
������һ�����Σ����﷨����˵��һ�������һ�� chunk ��ͬ��

</p><pre>	block ::= chunk
</pre>

<p>
һ��������Ա���ʽ��д��һ�����������Σ�

</p><pre>	stat ::= <b>do</b> block <b>end</b>
</pre><p>
��ʽ��������ڿ��Ʊ��������÷�Χ�����á�
��ʱ����ʽ�����鱻��������һ�������в���
<b>return</b> ���� <b>break</b> ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.4">��2.4.4</a>����


</p><h3>2.4.3 - <a name="2.4.3">��ֵ</a></h3>

<p>
Lua �������ظ�ֵ��
��ˣ���ֵ���﷨�����ǵȺ���߷�һϵ�б�����
���Ⱥ��ұ߷�һϵ�еı���ʽ��
���ߵ�Ԫ�ض��ö��ż俪��

</p><pre>	stat ::= varlist1 `<b>=</b>�� explist1
	varlist1 ::= var {`<b>,</b>�� var}
	explist1 ::= exp {`<b>,</b>�� exp}
</pre><p>
����ʽ���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5">��2.5</a> �����ۡ�


</p><p>
������ֵ����֮ǰ��
��һϵ�е���ֵ�ᱻ���뵽��߱�����Ҫ�ĸ�����
�����ֵ����Ҫ�ĸ���Ļ��������ֵ�ͱ��ӵ���
�����ֵ��������������
���ᰴ������չ���ɸ� <b>nil</b>��
�������ʽ�б���һ���������ý�����
������������ص�����ֵ�����ڶ������֮ǰ��������ֵ�����С�
����������������ñ������������������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5">��2.5</a>����

</p><p>
��ֵ�����Ȼ������������еı���ʽ��Ȼ���������ֵ������
��ˣ�������δ���

</p><pre>     i = 3
     i, a[i] = i+1, 20
</pre><p>
��� <code>a[3]</code> ����Ϊ 20��������Ӱ�쵽 <code>a[4]</code> ��
������Ϊ <code>a[i]</code> �е� <code>i</code> �ڱ���ֵΪ 4 ֮ǰ�ͱ��ó����ˣ���ʱ�� 3 ����
��˵ ������һ��

</p><pre>     x, y = y, x
</pre>
<p>
������������ <code>x</code> �� <code>y</code> �е�ֵ��


</p><p>
��ȫ�ֱ����Լ� table �е���ĸ�ֵ�����ĺ������ͨ�� metatable ���ı䡣
�Ա����±�ָ��ĸ�ֵ���� <code>t[i] = val</code> �ȼ���
<code>settable_event(t,i,val)</code>��
�����ں��� <code>settable_event</code> ����ϸ˵�����μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>��
���������û���� Lua �ж��������Ҳ�����Ա����á�
���������г������������ڷ�����͵�Ŀ�ģ�


</p><p>
����ȫ�ֱ����ĸ�ֵ <code>x = val</code>
�ȼ���
<code>_env.x = val</code>������ֿ��Եȼ���

</p><pre>     settable_event(_env, "x", val)
</pre><p>
���<code>_env</code> ָ�������������еĺ����Ļ�����
������ <code>_env</code> ��û���� Lua �ж��������
���ǽ������ڽ��͵�Ŀ��������д��������

</p><h3>2.4.4 - <a name="2.4.4">���ƽṹ</a></h3><p>
<b>if</b>�� <b>while</b>���Լ� <b>repeat</b> ��Щ���ƽṹ����ͨ�������壬����Ҳ�����Ƶ��﷨��

</p><pre>	stat ::= <b>while</b> exp <b>do</b> block <b>end</b>
	stat ::= <b>repeat</b> block <b>until</b> exp
	stat ::= <b>if</b> exp <b>then</b> block {<b>elseif</b> exp <b>then</b> block} [<b>else</b> block] <b>end</b>
</pre><p>

Lua Ҳ��һ�� <b>for</b> ��䣬����������ʽ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.5">��2.4.5</a>����


</p><p>
���ƽṹ�е���������ʽ���Է����κ�ֵ��
<b>false</b> �� <b>nil</b> ���߶�����Ϊ�Ǽ�������
���в�ͬ�� <b>nil</b> �� <b>false</b> ������ֵ������Ϊ����
���ر���Ҫע����ǣ����� 0 �Ϳ��ַ���Ҳ����Ϊ���棩��


</p><p>
�� <b>repeat</b>�C<b>until</b> ѭ���У�
�ڲ�����Ľ����㲻���� <b>until</b> ����ؼ��ִ���
����������������������ʽ��
��ˣ���������ʽ�п���ʹ��ѭ���ڲ������еĶ���ľֲ�������

</p><p>
<b>return</b> �����ڴӺ������� chunk����ʵ������һ����������
����ֵ��

������ chunk ���Է��ز�ֻһ��ֵ��
���� <b>return</b> ���﷨Ϊ

</p><pre>	stat ::= <b>return</b> [explist1]
</pre>

<p>
<b>break</b> ����������
<b>while</b>�� <b>repeat</b>���� <b>for</b> ѭ����
�������Ե�ѭ������������ε����У�

</p><pre>	stat ::= <b>break</b>
</pre><p>

<b>break</b> �������ڲ��ѭ����


</p><p>
<b>return</b> �� <b>break</b> ֻ�ܱ�д��һ����������һ�䡣
����������Ҫ��������м� <b>return</b> ���� <b>break</b> ��
�����ʹ����ʽ������һ���ڲ����顣
һ��д�� <code>do return end</code> ���� <code>do break end</code>��
��������д����Ϊ���� <b>return</b> �� <b>break</b> ������һ����������һ���ˡ�


</p><h3>2.4.5 - <a name="2.4.5">For ���</a></h3>

<p>

<b>for</b> ��������ʽ��һ����������ʽ����һ����һ����ʽ��

</p><p>
������ʽ�� <b>for</b> ѭ����ͨ��һ����ѧ���㲻�ϵ������ڲ��Ĵ���顣
�����������﷨��

</p><pre>	stat ::= <b>for</b> Name `<b>=</b>�� exp `<b>,</b>�� exp [`<b>,</b>�� exp] <b>do</b> block <b>end</b>
</pre><p>
<em>block</em> ���� <em>name</em> ��ѭ���������ӵ�һ�� <em>exp</em> ��ʼ��ֱ���ڶ��� <em>exp</em> ��ֵΪֹ���䲽��Ϊ
������ <em>exp</em> ��
��ȷ�е�˵��һ�� <b>for</b> ѭ�����������������

</p><pre>     for v = <em>e1</em>, <em>e2</em>, <em>e3</em> do <em>block</em> end
</pre><p>
��ȼ��ڴ��룺

</p><pre>     do
       local <em>var</em>, <em>limit</em>, <em>step</em> = tonumber(<em>e1</em>), tonumber(<em>e2</em>), tonumber(<em>e3</em>)
       if not (<em>var</em> and <em>limit</em> and <em>step</em>) then error() end
       while (<em>step</em> &gt; 0 and <em>var</em> &lt;= <em>limit</em>) or (<em>step</em> &lt;= 0 and <em>var</em> &gt;= <em>limit</em>) do
         local v = <em>var</em>
         <em>block</em>
         <em>var</em> = <em>var</em> + <em>step</em>
       end
     end
</pre><p>

ע�������⼸�㣺

</p><ul>

<li>
�����������Ʊ���ʽ��ֻ������һ�Σ�����ʽ�ļ�����ѭ����ʼ֮ǰ��
��Щ����ʽ�Ľ�����������֡�
</li>

<li>
<code><em>var</em></code> ��<code><em>limit</em></code> ���Լ� <code><em>step</em></code> ����һЩ���ɼ��ı�����
���������������ֶ��������ڽ��ͷ��㡣
</li>

<li>
�������������ʽ��������û�и�������Ѳ�����Ϊ 1 ��
</li>

<li>
������� <b>break</b> ���˳� <b>for</b> ѭ����
</li>

<li>
ѭ������ <code>v</code> ��һ��ѭ���ڲ��ľֲ�������
�� <b>for</b> ѭ����������Ͳ�����ʹ������
�������Ҫ���ֵ�����˳�ѭ��ǰ����������һ��������
</li>

</ul>

<p>
һ����ʽ�� <b>for</b> ͨ��һ��������������<em>iterators</em>���ĺ���������
ÿ�ε������������������ᱻ�����Բ���һ���µ�ֵ��
�����ֵΪ <b>nil</b> ʱ��ѭ��ֹͣ��
һ����ʽ�� <b>for</b> ѭ�����﷨���£�

</p><pre>	stat ::= <b>for</b> namelist <b>in</b> explist1 <b>do</b> block <b>end</b>
	namelist ::= Name {`<b>,</b>�� Name}
</pre><p>
<b>for</b> ����������

</p><pre>     for <em>var_1</em>, ������, <em>var_n</em> in <em>explist</em> do <em>block</em> end
</pre><p>
���ȼ�������һ�δ��룺

</p><pre>     do
       local <em>f</em>, <em>s</em>, <em>var</em> = <em>explist</em>
       while true do
         local <em>var_1</em>, ������, <em>var_n</em> = <em>f</em>(<em>s</em>, <em>var</em>)
         <em>var</em> = <em>var_1</em>
         if <em>var</em> == nil then break end
         <em>block</em>
       end
     end
</pre><p>
ע�����¼��㣺

</p><ul>

<li>
<code><em>explist</em></code> ֻ�ᱻ����һ�Ρ�
����������ֵ�� һ��������������һ��״̬��һ���������ĳ�ʼֵ��
</li>

<li>
<code><em>f</em></code>�� <code><em>s</em></code>�� �Լ� <code><em>var</em></code> ���ǲ��ɼ��ı�����
���������������ֶ�ֻ��Ϊ�˽�˵���㡣
</li>

<li>
�����ʹ�� <b>break</b> ������ <b>for</b> ѭ����
</li>

<li>
ѭ������ <code><em>var_i</em></code> ����ѭ����˵��һ���ֲ�������
�㲻������ <b>for</b> ѭ�����������ʹ�á�
�������Ҫ������Щֵ����ô����ѭ������ǰ��ֵ����ı�����ȥ��
</li>

</ul>




<h3>2.4.6 - <a name="2.4.6">�Ѻ���������Ϊ����</a></h3><p>
Ϊ������ʹ�ÿ��ܵĸ����ã�
�������ÿ��Ա���Ϊһ������ִ�У�

</p><pre>	stat ::= functioncall
</pre><p>
����������£����еķ���ֵ����������
���������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.8">��2.5.8</a> �н��͡�


</p><h3>2.4.7 - <a name="2.4.7">�ֲ���������</a></h3><p>
�ֲ������������������κεط�������
�������԰���һ����ʼ����ֵ������

</p><pre>	stat ::= <b>local</b> namelist [`<b>=</b>�� explist1]
</pre><p>
����еĻ�����ʼ����ֵ��������Ϊ��ͬ�ڸ�ֵ�������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.3">��2.4.3</a>����
�������еı���������ʼ��Ϊ <b>nil</b>��


</p><p>
һ�� chunk ͬʱҲ��һ�����飨�μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.1">��2.4.1</a>����
���Ծֲ��������Է��� chunk ����Щ��ʽע��������֮�⡣
��Щ�ֲ����������÷�Χ��������һֱ���쵽 chunk ĩβ��

</p><p>
�ֲ������Ŀɼ������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.6">��2.6</a> �н��͡�


</p><h2>2.5 - <a name="2.5">����ʽ</a></h2>

<p>
Lua ������Щ��������ʽ��

</p><pre>	exp ::= prefixexp
	exp ::= <b>nil</b> | <b>false</b> | <b>true</b>
	exp ::= Number
	exp ::= String
	exp ::= function
	exp ::= tableconstructor
	exp ::= `<b>...</b>��
	exp ::= exp binop exp
	exp ::= unop exp
	prefixexp ::= var | functioncall | `<b>(</b>�� exp `<b>)</b>��
</pre>

<p>
���ֺ��ַ����� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.1">��2.1</a> �н��ͣ�
������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.3">��2.3</a> �н��ͣ�
���������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.9">��2.5.9</a> �н��ͣ�
���������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.8">��2.5.8</a> �н��ͣ�
table �Ĺ����� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.7">��2.5.7</a> �н��ͣ�
�ɱ�����ı���ʽд�������� ('<code>...</code>') ����ֻ�ܱ������пɱ�����ĺ����У�
��Щ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.9">��2.5.9</a> �н��͡�


</p><p>
��Ԫ��������������ѧ������������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.1">��2.5.1</a>����
�Ƚϲ��������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.2">��2.5.2</a>�����߼����������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.3">��2.5.3</a>����
�Լ����Ӳ��������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.4">��2.5.4</a>����
һԪ�������������ţ��μ�see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.1">��2.5.1</a>����
ȡ�� <b>not</b>���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.3">��2.5.3</a>����
��ȡ���Ȳ��������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.5">��2.5.5</a>����


</p><p>
�������úͿɱ��������ʽ�����Է��ڶ��ط���ֵ�С�
�������ʽ��Ϊһ���������γ��֣��μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.6">��2.4.6</a>��
����ֻ����һ���������ã���
���ǵķ����б��������뵽���Ԫ�أ�Ҳ���Ǻ������з���ֵ��
�������ʽ���ڱ���ʽ�б�����󣨻�����Ψһ����Ԫ�أ�
�Ͳ������κεĶ�����������Ǻ�����������������������
���κ�����������£�Lua ���ѱ���ʽ������ɵ�һԪ�أ�
���Գ���һ��֮����κ�ֵ��

</p><p>
������һЩ���ӣ�

</p><pre>     f()                -- ������ 0 �����
     g(f(), x)          -- f() ��������һ�����
     g(x, f())          -- g ������ x �������� f() �ķ���ֵ
     a,b,c = f(), x     -- f() ��������һ����� �� c �����ﱻ��Ϊ nil ��
     a,b = ...          -- a ����ֵΪ�ɱ�����еĵ�һ����
                        -- b ����ֵΪ�ڶ��� ������ɱ�����в�û�ж�Ӧ��ֵ��
						-- ���� a �� b ���п��ܱ���Ϊ nil��
     
     a,b,c = x, f()     -- f() ������Ϊ�������
     a,b,c = f()        -- f() ������Ϊ�������
     return f()         -- ���� f() ���ص����н��
     return ...         -- �������дӿɱ�����н�������ֵ
     return x,y,f()     -- ���� x, y, �Լ����� f() �ķ���ֵ
     {f()}              -- �� f() �����з���ֵ����һ���б�
     {...}              -- �ÿɱ�����е�����ֵ����һ���б�
     {f(), nil}         -- f() ������Ϊһ�����
</pre>

<p>
�������������ı���ʽ��Զ������һ��ֵ�����ԣ�
<code>(f(x,y,z))</code> ��ʹ <code>f</code> ���ض��ֵ���������ʽ��Զ��һ����һֵ��
��<code>(f(x,y,z))</code> ��ֵ�� <code>f</code> ���صĵ�һ��ֵ����� <code>f</code>
������ֵ�Ļ�����ô����ֵ���� <b>nil</b> ����


</p><h3>2.5.1 - <a name="2.5.1">��ѧ���������</a></h3><p>
Lua ֧�ֳ�������ѧ�����������
��Ԫ���� <code>+</code> ���ӷ�����
<code>-</code> ����������<code>*</code> ���˷�����
<code>/</code> ���������� <code>%</code> ��ȡģ�����Լ� <code>^</code> ���ݣ���
��һԪ���� <code>-</code> ��ȡ������
��������ֲ��������ǿ���ת��Ϊ���ֵ��ַ������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">��2.2.1</a>����
������Щ������������ͨ���ĺ��塣
�ݲ������Զ��κ���ֵ���������������磬
<code>x^(-0.5)</code> ������� <code>x</code> ƽ�����ĵ�����
ȡģ����������Ϊ

</p><pre>     a % b == a - math.floor(a/b)*b
</pre><p>
�����˵������������Ը�����Բ���������������ע������������ȡģ�Ľ��Ϊ������


</p><h3>2.5.2 - <a name="2.5.2">�Ƚϲ�����</a></h3><p>
Lua �еıȽϲ�������

</p><pre>     ==    ~=    &lt;     &gt;     &lt;=    &gt;=
</pre><p>
��Щ�����Ľ������ <b>false</b> ���� <b>true</b>��


</p><p>
���ڲ��� (<code>==</code>) ���ȱȽϲ����������͡�
������Ͳ�ͬ��������� <b>false</b>��
���򣬼����Ƚ�ֵ��
���ֺ��ַ������ó���ķ�ʽ�Ƚϡ�
���� ��table ��userdata ��thread ���Լ������������õ���ʽ�Ƚϣ�
��������ֻ��������ָ��ͬһ������ʱ����Ϊ��ȡ�
ÿ���㴴��һ���¶���һ�� table ���� userdata ��thread ��������
���Ƕ�������ͬ������ͬ���ϴδ����Ķ�����


</p><p>
����Ըı� Lua �Ƚ� table �� userdata �ķ�ʽ������Ҫʹ�� "eq" ���ԭ����
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">��2.2.1</a> ���ἰ��ת�����򲢲������ڱȽϲ�����
���ԣ� <code>"0"==0</code> ���� <b>false</b>��
���� <code>t[0]</code> �� <code>t["0"]</code> �������� table �в�ͬ����

</p><p>
������ <code>~=</code> ��ȫ�ȼ��� (<code>==</code>) �����ķ�ֵ��


</p><p>
��С�Ƚϲ��������·�ʽ���С�
��������������֣���ô��ֱ�������ֱȽϡ�
����������������ַ����������ַ����Ƚϵķ�ʽ���С�
����Lua �����ŵ��� "lt" ���� "le" Ԫ����
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����

</p><h3>2.5.3 - <a name="2.5.3">�߼�������</a></h3><p>
Lua �е��߼���������
<b>and</b>, <b>or</b>, �Լ� <b>not</b>��
�Ϳ��ƽṹ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.4">��2.4.4</a>��һ����
���е��߼��������� <b>false</b> �� <b>nil</b> ����Ϊ�٣�
��������һ�ж������档


</p><p>
ȡ������ <b>not</b> ���Ƿ��� <b>false</b> �� <b>true</b> �е�һ����
������� <b>and</b> �ڵ�һ������Ϊ <b>false</b> �� <b>nil</b> ʱ
�������һ��������
����<b>and</b> ���صڶ���������
������� <b>or</b> �ڵ�һ��������Ϊ <b>nil</b> Ҳ��Ϊ <b>false</b> ʱ��
�������һ�����������򷵻صڶ���������
<b>and</b> �� <b>or</b> ����ѭ��·����
Ҳ����˵���ڶ���������ֻ����Ҫ��ʱ��ȥ��ֵ��
������һЩ���ӣ�

</p><pre>     10 or 20            --&gt; 10
     10 or error()       --&gt; 10
     nil or "a"          --&gt; "a"
     nil and 10          --&gt; nil
     false and error()   --&gt; false
     false and nil       --&gt; false
     false or nil        --&gt; nil
     10 and 20           --&gt; 20
</pre><p>
�����Ȿ�ֲ��У�
--&gt; ָǰ�����ʽ�Ľ������



</p><h3>2.5.4 - <a name="2.5.4">���ӷ�</a></h3><p>
Lua ���ַ��������Ӳ�����д�������� ('<code>..</code>')��
������������������ַ����������֣����Ӳ������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">��2.2.1</a> ���ᵽ�Ĺ������ת��Ϊ�ַ�����
���򣬻�ȡ����Ԫ���� "concat" ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����


</p><h3>2.5.5 - <a name="2.5.5">ȡ���Ȳ�����</a></h3>

<p>
ȡ���Ȳ�����д��һԪ���� <code>#</code>��
�ַ����ĳ����������ֽ�����������һ���ַ�һ���ֽڼ�����ַ������ȣ���


</p><p>
table <code>t</code> �ĳ��ȱ������һ�������±� <code>n</code> ��
������ <code>t[n]</code> ���� <b>nil</b> �� <code>t[n+1]</code> Ϊ <b>nil</b>��
���⣬��� <code>t[1]</code> Ϊ <b>nil</b> ��<code>n</code> �Ϳ������㡣
���ڳ�������飬����� 1 �� <code>n</code> ����һЩ�ǿյ�ֵ��ʱ��
���ĳ��Ⱦ;�ȷ��Ϊ <code>n</code>�������һ��ֵ���±ꡣ
���������һ�����ն��� ������˵��<b>nil</b> ֵ�����ڷǿ�ֵ֮�䣩��
��ô <code>#t</code> ������ָ���κ�һ���� <b>nil</b> ֵ��ǰһ��λ�õ��±�
������˵���κ�һ�� <b>nil</b> ֵ���п��ܱ���������Ľ�������





</p><h3>2.5.6 - <a name="2.5.6">���ȼ�</a></h3><p>
Lua �в����������ȼ�д���±��У��ӵ͵������ȼ�����

</p><pre>     or
     and
     &lt;     &gt;     &lt;=    &gt;=    ~=    ==
     ..
     +     -
     *     /     %
     not   #     - (unary)
     ^
</pre><p>
ͨ������������������ı��������
���Ӳ����� ('<code>..</code>') ���ݲ��� ('<code>^</code>') �Ǵ�������ġ�
�������еĲ������Ǵ������ҡ�


</p><h3>2.5.7 - <a name="2.5.7">Table ����</a></h3><p>
table ��������һ������ table �ı���ʽ��
ÿ�ι����ӱ�ִ�У����ṹ���һ���µ� table ��
�����ӿ��Ա���������һ���յ� table��
Ҳ������������һ�� table ����ʼ�����е�һЩ��
һ��Ĺ����ӵ��﷨����

</p><pre>	tableconstructor ::= `<b>{</b>�� [fieldlist] `<b>}</b>��
	fieldlist ::= field {fieldsep field} [fieldsep]
	field ::= `<b>[</b>�� exp `<b>]</b>�� `<b>=</b>�� exp | Name `<b>=</b>�� exp | exp
	fieldsep ::= `<b>,</b>�� | `<b>;</b>��
</pre>

<p>
ÿ������ <code>[exp1] = exp2</code> ������ table �������µ�һ�
���ֵΪ <code>exp1</code> ��ֵΪ <code>exp2</code>��
���� <code>name = exp</code> ����ȼ���
<code>["name"] = exp</code>��
������� <code>exp</code> ����ȼ���
<code>[i] = exp</code> �� ����� <code>i</code> ��һ���� 1 ��ʼ�������������֡�
�������ʽ�е������򲻻��ƻ��������
�ٸ����ӣ�

</p><pre>     a = { [f(1)] = g; "x", "y"; x = 1, f(x), [30] = 23; 45 }
</pre><p>
�ȼ���

</p><pre>     do
       local t = {}
       t[f(1)] = g
       t[1] = "x"         -- 1st exp
       t[2] = "y"         -- 2nd exp
       t.x = 1            -- t["x"] = 1
       t[3] = f(x)        -- 3rd exp
       t[30] = 23
       t[4] = 45          -- 4th exp
       a = t
     end
</pre>

<p>
������������һ�������ʽ�� <code>exp</code> ��
���������ʽ��һ���������û�����һ���ɱ������
��ô�������ʽ���еķ���ֵ�������Ľ����б�
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.8">��2.5.8</a>����
Ϊ�˱�����һ�㣬����������ŰѺ������ã����ǿɱ������������
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5">��2.5</a>����


</p><p>
��ʼ���������������һ���ָ����
������ƿ��Է����ɻ������ɴ��롣



</p><h3>2.5.8 - <a name="2.5.8">��������</a></h3><p>
Lua �еĺ������õ��﷨���£�

</p><pre>	functioncall ::= prefixexp args
</pre><p>
��������ʱ����һ����prefixexp �� args �ȱ���ֵ��
��� prefixexp ��ֵ�������� <em>function</em>��
��ô��������ͱ��ø����Ĳ������á�
���� prefixexp ��Ԫ���� "call" �ͱ����ã�
��һ���������� prefixexp ��ֵ������������ԭ���ĵ��ò���
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����


</p><p>
��������ʽ

</p><pre>	functioncall ::= prefixexp `<b>:</b>�� Name args
</pre><p>
������������ "����"��
���� Lua ֧�ֵ�һ���﷨�ǡ��� <code>v:name(<em>args</em>)</code>
������ӣ������ͳ� <code>v.name(v,<em>args</em>)</code>��
���� <code>v</code> ֻ�ᱻ��ֵһ�Ρ�


</p><p>
�������﷨���£�

</p><pre>	args ::= `<b>(</b>�� [explist1] `<b>)</b>��
	args ::= tableconstructor
	args ::= String
</pre><p>
���в����ı���ʽ��ֵ���ں�������֮ǰ��
�����ĵ�����ʽ <code>f{<em>fields</em>}</code> ��һ���﷨�����ڱ�ʾ
 <code>f({<em>fields</em>})</code>��
����ָ�����б���һ����һ���´����������б���
����������ʽ <code>f'<em>string</em>'</code> 
������ <code>f"<em>string</em>"</code> ����� <code>f[[<em>string</em>]]</code>��
Ҳ��һ���﷨�ǣ����ڱ�ʾ <code>f('<em>string</em>')</code>��
����ָ�����б���һ���������ַ�����


</p><p>
��Ϊ����ʽ�﷨�� Lua �бȽ����ɣ�
�����㲻���ں������õ� '<code>(</code>' ǰ���С�
������ƿ��Ա��������е�һЩ���塣
����������д

</p><pre>     a = f
     (g).x(a)
</pre><p>
Lua ����������һ����һ���Σ� <code>a = f(g).x(a)</code> ��
��ˣ�������������Ϊ���������Σ������������֮��д��һ���ֺš�
������������� <code>f</code>��
������ <code>(g)</code> ǰ��ȥ���С�


</p><p>
����һ�ֵ�����ʽ��<code>return</code> <em>functioncall</em> ������һ��β���á�
Lua ʵ�����ʵ���β�����ã������ʵ���β�ݹ飩��
��β�����У�
�����õĺ������õ������ĺ����Ķ�ջ�
��ˣ����ڳ���ִ�е�Ƕ��β���õĲ�����û�����Ƶġ�
Ȼ����β���ý�ɾ���������ĺ������κε�����Ϣ��
ע�⣬β����ֻ�������ض����﷨�£�
��ʱ�� <b>return</b> ֻ�е�һ����������Ϊ������
�����﷨ʹ�õ��ú����Ľ�����Ծ�ȷ���ء�
��ˣ�������Щ���Ӷ�����β���ã�

</p><pre>     return (f(x))        -- ����ֵ������Ϊһ��
     return 2 * f(x)
     return x, f(x)       -- ������ɷ���ֵ
     f(x); return         -- �޷���ֵ
     return x or f(x)     -- ����ֵ������Ϊһ��
</pre>




<h3>2.5.9 - <a name="2.5.9">��������</a></h3>

<p>
����������﷨���£�

</p><pre>	function ::= <b>function</b> funcbody
	funcbody ::= `<b>(</b>�� [parlist1] `<b>)</b>�� block <b>end</b>
</pre>

<p>
���ⶨ����һЩ�﷨�Ǽ򻯺��������д����

</p><pre>	stat ::= <b>function</b> funcname funcbody
	stat ::= <b>local</b> <b>function</b> Name funcbody
	funcname ::= Name {`<b>.</b>�� Name} [`<b>:</b>�� Name]
</pre><p>
������д����
</p><pre>     function f () <em>body</em> end
</pre><p>
��ת����
</p><pre>     f = function () <em>body</em> end
</pre><p>
������д����
</p><pre>     function t.a.b.c.f () <em>body</em> end
</pre><p>
��ת����
</p><pre>     t.a.b.c.f = function () <em>body</em> end
</pre><p>
������д����
</p><pre>     local function f () <em>body</em> end
</pre><p>
��ת����
</p><pre>     local f; f = function () <em>body</em> end
</pre><p>
ע�⣬������ת����
</p><pre>     local f = function () <em>body</em> end
</pre><p>
��������ֻ�ں���������Ҫ���� <code>f</code> ʱ���С���


</p><p>
һ������������һ����ִ�еı���ʽ��
ִ�н����һ������Ϊ <em>function</em> ��ֵ��
�� Lua Ԥ����һ�� chunk ��ʱ��
chunk ��Ϊһ������������������Ҳ�ͱ�Ԥ�����ˡ�
��ô�����ۺ�ʱ Lua ִ���˺������壬
������������ͱ�ʵ�����ˣ�����˵�ǹر��ˣ���
���������ʵ��������˵�� <em>closure</em>���հ�����
�Ǳ���ʽ������ֵ��
��ͬ�����Ĳ�ͬʵ���п������ò�ͬ���ⲿ�ֲ�������
Ҳ����ӵ�в�ͬ�Ļ�������

</p><p>
�βΣ�����������Ҫ�Ĳ�������һЩ��ʵ�Σ�ʵ�ʴ����������ֵ��ʼ���ľֲ�������

</p><pre>	parlist1 ::= namelist [`<b>,</b>�� `<b>...</b>��] | `<b>...</b>��
</pre><p>
��һ�����������ã�
�������û�б�����Ϊ���ղ����������������β��б���ĩβע�������� ('<code>...</code>')��
��ôʵ���б��ͻᱻ�������β��б��ĳ��ȣ�
�䳤���������������ʵ���б���
ȡ����֮���ǣ����������ж���Ĳ�������һ��ͨ���䳤��������ʽ���ݸ�������
��д�������������㡣
�������ʽ��ֵ��һ��ʵ��ֵ���б����������͸�һ�����Է��ض������ĺ���һ����
���һ���䳤��������ʽ������һ������ʽ��ʹ�ã����Ƿ�����һ������ʽ���м䣬
��ô���ķ���ֵ�ͻᱻ����Ϊ����ֵ��
���������ʽ������һϵ�б���ʽ�����һ�����Ͳ����������ˣ����������Ÿ�������������


</p><p>
�����������¶��壬Ȼ��������һ�����ӣ�

</p><pre>     function f(a, b) end
     function g(a, b, ...) end
     function r() return 1,2,3 end
</pre><p>
���濴��ʵ�ε��β����Լ��ɱ䳤������ӳ���ϵ��

</p><pre>     CALL            PARAMETERS
     
     f(3)             a=3, b=nil
     f(3, 4)          a=3, b=4
     f(3, 4, 5)       a=3, b=4
     f(r(), 10)       a=1, b=10
     f(r())           a=1, b=2
     
     g(3)             a=3, b=nil, ... --&gt;  (nothing)
     g(3, 4)          a=3, b=4,   ... --&gt;  (nothing)
     g(3, 4, 5, 8)    a=3, b=4,   ... --&gt;  5  8
     g(5, r())        a=5, b=1,   ... --&gt;  2  3
</pre>

<p>
����� <b>return</b> �����أ��μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.4.4">��2.4.4</a>����
���ִ�е�����ĩβ����û�������κ� <b>return</b> ��䣬
�����Ͳ��᷵���κν����


</p><p>
ð���﷨�����������巽����
����˵������������һ����ʽ���β� <code>self</code>��
��ˣ�����д����

</p><pre>     function t.a.b.c:f (<em>params</em>) <em>body</em> end
</pre><p>
������һ��д�����﷨�ǣ�

</p><pre>     t.a.b.c.f = function (self, <em>params</em>) <em>body</em> end
</pre>






<h2>2.6 - <a name="2.6">���ӹ���</a></h2>

<p>
Lua ��һ���дʷ����÷�Χ�����ԡ�
���������÷�Χ��ʼ����������֮��ĵ�һ�����Σ�
�����ڰ���������������ڲ�����Ľ����㡣
��������Щ���ӣ�

</p><pre>     x = 10                -- ȫ�ֱ���
     do                    -- �µ�����
       local x = x         -- �µ�һ�� 'x', ����ֵ������ 10
       print(x)            --&gt; 10
       x = x+1
       do                  -- ��һ������
         local x = x+1     -- ��һ�� 'x'
         print(x)          --&gt; 12
       end
       print(x)            --&gt; 11
     end
     print(x)              --&gt; 10  ��ȡ������ȫ�ֵ���һ����
</pre>

<p>
ע��������� <code>local x = x</code> ������������
�µ� <code>x</code> ���ڱ����������ǻ�û�н����������÷�Χ��
���Եڶ��� <code>x</code> ָ���������һ��ı�����


</p><p>
��Ϊ������һ���ʷ����÷�Χ�Ĺ���
���Կ����ں����ڲ����ɵĶ���ֲ�������ʹ�����ǡ�
��һ���ֲ����������ڲ�ĺ�����ʹ�õ�ʱ��
�����ڲ㺯������
<em>upvalue</em>����ֵ�������� <em>�ⲿ�ֲ�����</em>��

</p><p>
ע�⣬ÿ��ִ�е�һ�� local ��䶼�ᶨ���һ���µľֲ�������
��������һ�����ӣ�

</p><pre>     a = {}
     local x = 20
     for i=1,10 do
       local y = 0
       a[i] = function () y=y+1; return x+y end
     end
</pre><p>
���ѭ��������ʮ�� closure����ָʮ������������ʵ������
��Щ closure �е�ÿһ����ʹ���˲�ͬ�� <code>y</code> ������
�������ֹ�����ͬһ�� <code>x</code>��


</p><h2>2.7 - <a name="2.7">������</a></h2>

<p>
��Ϊ Lua ��һ��Ƕ��ʽ����չ���ԣ�
���е� Lua �������Ǵ���������� C ������� Lua ��
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a>���е�һ��������ʼ�ġ�
�� Lua ��������е��κ�ʱ�����˴��󣬿���Ȩ���ύ���� C ��
�� C ��������һЩǡ���Ĵ�ʩ�������ӡ��һ��������Ϣ����

</p><p>
Lua ���������ʽ�ĵ��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-error"><code>error</code></a> ����������һ������
�������Ҫ�� Lua �в������Ĵ���
�����ʹ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-pcall"><code>pcall</code></a> ������

</p><h2>2.8 - <a name="2.8">Metatable��Ԫ����</a></h2>

<p>
Lua �е�ÿ��ֵ��������һ�� <em>metatable</em>��
��� <em>metatable</em> ����һ��ԭʼ�� Lua table ��
����������ԭʼֵ���ض������µ���Ϊ��
�����ͨ���� metatable �е��ض�����һЩֵ���ı�ӵ����� metatable ��ֵ
��ָ������֮��Ϊ��
������˵����һ�������ֵ�ֵ���ӷ�������ʱ��
Lua �������� metatable �� <code>"__add"</code> ���е��Ƿ���һ��������
�������ôһ�������Ļ���Lua �������������ִ��һ�μӷ���


</p><p>
���ǽ� metatable �еļ���Ϊ <em>�¼� (event)</em> �������е�ֵ���� <em>Ԫ���� (metamethod)</em>��
���ϸ������У��¼��� <code>"add"</code> ��Ԫ���������Ǹ�ִ�мӷ������ĺ�����


</p><p>
�����ͨ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-getmetatable"><code>getmetatable</code></a> ��������ѯ���κ�һ��ֵ�� metatable��


</p><p>
�����ͨ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-setmetatable"><code>setmetatable</code></a> �������滻�� table �� metatable ��
�㲻�ܴ� Lua �иı������κ����͵�ֵ�� metatable ��ʹ�� debug �����⣩��
Ҫ�������Ļ�����ʹ�� C API ��


</p><p>
ÿ�� table �� userdata ӵ�ж����� metatable ����Ȼ��� table �� userdata
���Թ���һ����ͬ�ı������ǵ� metatable����
�����������͵�ֵ��ÿ�����Ͷ��ֱ���Ψһ��һ�� metatable��
��ˣ����е�����һ��ֻ��һ�� metatable �����е��ַ���Ҳ�ǣ��ȵȡ�


</p><p>
һ�� metatable ���Կ���һ����������ѧ����������Ƚϲ��������Ӳ�����ȡ���Ȳ�����ȡ�±����ʱ����Ϊ��
metatable �л����Զ���һ���������� userdata �������ռ�ʱ��������
������Щ������Lua �����������һ���������¼���ָ������
�� Lua ��Ҫ��һ��ֵ������Щ�����е�һ��ʱ��
����ȥ���ֵ�� metatable ���Ƿ��ж�Ӧ�¼���
����еĻ���������Ӧ��ֵ��Ԫ������������ Lua ���������������


</p><p>
metatable ���Կ��ƵĲ������������г�����
ÿ������������Ӧ���������֡�
ÿ�������ļ��������ò������ּ��������»��� '<code>__</code>' ǰ׺���ַ�����
������˵��"add" �����ļ��������ַ��� <code>"__add"</code>��
��Щ������������һ�� Lua �������������������ִ�и�Ϊǡ����

</p><p>
����չʾ���� Lua д�Ĵ��������˵�ã�
ʵ�ʵ���Ϊ�Ѿ�Ӳ�����ڽ������У���ִ��Ч��ҪԶ������Щģ����롣
��Щ���������ĵĴ������õ��ĺ���
�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-rawget"><code>rawget</code></a> �� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-tonumber"><code>tonumber</code></a> ���ȵȡ���
�������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#5.1">��5.1</a> ���ҵ���
�ر�ע�⣬����ʹ������һ������ʽ���Ӹ�����������ȡԪ����

</p><pre>     metatable(obj)[event]
</pre><p>

���Ӧ�ñ������

</p><pre>     rawget(getmetatable(obj) or {}, event)
</pre><p>

�����˵������һ��Ԫ�������ٻᴥ���κε�Ԫ������
���ҷ���һ��û�� metatable �Ķ���Ҳ����ʧ�ܣ���ֻ�Ǽ򵥷��� <b>nil</b>����


</p><ul>

<li><b>"add":</b>
<code>+</code> ������



<p>
������� <code>getbinhandler</code> ���������� Lua ����ѡ��һ��������������Ԫ������
���ȣ�Lua ���Ե�һ����������
����������������û�ж�����������Ĵ�������Ȼ�� Lua �᳢�Եڶ�����������

</p><pre>     function getbinhandler (op1, op2, event)
       return metatable(op1)[event] or metatable(op2)[event]
     end
</pre><p>
ͨ����������� <code>op1 + op2</code> ����Ϊ����

</p><pre>     function add_event (op1, op2)
       local o1, o2 = tonumber(op1), tonumber(op2)
       if o1 and o2 then  -- �����������������֣�
         return o1 + o2   -- ����� '+' ��ԭ���� 'add'
       else  -- ����һ����������������ʱ
         local h = getbinhandler(op1, op2, "__add")
         if h then
           -- �����������������ô�����
           return h(op1, op2)
         else  -- û�д�������ȱʡ��Ϊ
           error(������)
         end
       end
     end
</pre><p>
</p></li>

<li><b>"sub":</b>
<code>-</code> ������

����Ϊ������ "add" ������
</li>

<li><b>"mul":</b>
<code>*</code> ������

����Ϊ������ "add" ������
</li>

<li><b>"div":</b>
<code>/</code> ������

����Ϊ������ "add" ������
</li>

<li><b>"mod":</b>
<code>%</code> ������

����Ϊ������ "add" ������
����ԭ��������������
<code>o1 - floor(o1/o2)*o2</code>
</li>

<li><b>"pow":</b>
<code>^</code> ���ݣ�������

����Ϊ������ "add" ������
����ԭ�������ǵ��� <code>pow</code> ������ͨ�� C math �⣩��
</li>

<li><b>"unm":</b>
һԪ <code>-</code> ������


<pre>     function unm_event (op)
       local o = tonumber(op)
       if o then  -- �����������֣�
         return -o  -- ����� '-' ��һ��ԭ���� 'unm'
       else  -- �������������֡�
         -- ���ԴӲ������еõ�������
         local h = metatable(op).__unm
         if h then
           -- �Բ�����Ϊ�������ô�����
           return h(op)
         else  -- û�д�������ȱʡ��Ϊ
           error(������)
         end
       end
     end
</pre><p>
</p></li>

<li><b>"concat":</b>
<code>..</code> �����ӣ�������


<pre>     function concat_event (op1, op2)
       if (type(op1) == "string" or type(op1) == "number") and
          (type(op2) == "string" or type(op2) == "number") then
         return op1 .. op2  -- ԭ���ַ�������
       else
         local h = getbinhandler(op1, op2, "__concat")
         if h then
           return h(op1, op2)
         else
           error(������)
         end
       end
     end
</pre><p>
</p></li>

<li><b>"len":</b>
<code>#</code> ������


<pre>     function len_event (op)
       if type(op) == "string" then
         return strlen(op)         -- ԭ����ȡ�ַ�������
       elseif type(op) == "table" then
         return #op                -- ԭ����ȡ table ����
       else
         local h = metatable(op).__len
         if h then
           -- ���ò������Ĵ�����
           return h(op)
         else  -- û�д�������ȱʡ��Ϊ
           error(������)
         end
       end
     end
</pre><p>
���� table �ĳ��Ȳμ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.5">��2.5.5</a> ��
</p></li>

<li><b>"eq":</b>
<code>==</code> ������

���� <code>getcomphandler</code> ������ Lua ����ѡ��һ�������������Ƚϲ�����
Ԫ���������ڲ��ڱȽϵ���������������ͬ���ж�Ӧ������ͬ��Ԫ����ʱ����Ч��

<pre>     function getcomphandler (op1, op2, event)
       if type(op1) ~= type(op2) then return nil end
       local mm1 = metatable(op1)[event]
       local mm2 = metatable(op2)[event]
       if mm1 == mm2 then return mm1 else return nil end
     end
</pre><p>
"eq" �¼������·�ʽ���壺

</p><pre>     function eq_event (op1, op2)
       if type(op1) ~= type(op2) then  -- ��ͬ�����ͣ�
         return false   -- ��ͬ�Ķ���
       end
       if op1 == op2 then   -- ԭ������ȱȽϽ����
         return true   -- �������
       end
       -- ����ʹ��Ԫ����
       local h = getcomphandler(op1, op2, "__eq")
       if h then
         return h(op1, op2)
       else
         return false
       end
     end
</pre><p>
<code>a ~= b</code> �ȼ��� <code>not (a == b)</code> ��
</p></li>

<li><b>"lt":</b>
<code>&lt;</code> ������


<pre>     function lt_event (op1, op2)
       if type(op1) == "number" and type(op2) == "number" then
         return op1 &lt; op2   -- ���ֱȽ�
       elseif type(op1) == "string" and type(op2) == "string" then
         return op1 &lt; op2   -- �ַ��������ַ��Ƚ�
       else
         local h = getcomphandler(op1, op2, "__lt")
         if h then
           return h(op1, op2)
         else
           error(������);
         end
       end
     end
</pre><p>
<code>a &gt; b</code> �ȼ��� <code>b &lt; a</code>.
</p></li>

<li><b>"le":</b>
<code>&lt;=</code> ������


<pre>     function le_event (op1, op2)
       if type(op1) == "number" and type(op2) == "number" then
         return op1 &lt;= op2   -- ���ֱȽ�
       elseif type(op1) == "string" and type(op2) == "string" then
         return op1 &lt;= op2   -- �ַ��������ַ��Ƚ�
       else
         local h = getcomphandler(op1, op2, "__le")
         if h then
           return h(op1, op2)
         else
           h = getcomphandler(op1, op2, "__lt")
           if h then
             return not h(op2, op1)
           else
             error(������);
           end
         end
       end
     end
</pre><p>
<code>a &gt;= b</code> �ȼ��� <code>b &lt;= a</code> ��
ע�⣬���Ԫ���� "le" û���ṩ��Lua �ͳ��� "lt" ��
���ٶ� <code>a &lt;= b</code> �ȼ��� <code>not (b &lt; a)</code> ��
</p></li>

<li><b>"index":</b>
ȡ�±�������ڷ��� <code>table[key]</code> ��


<pre>     function gettable_event (table, key)
       local h
       if type(table) == "table" then
         local v = rawget(table, key)
         if v ~= nil then return v end
         h = metatable(table).__index
         if h == nil then return nil end
       else
         h = metatable(table).__index
         if h == nil then
           error(������);
         end
       end
       if type(h) == "function" then
         return h(table, key)      -- ���ô�����
       else return h[key]          -- �����ظ���������
       end
     end
</pre><p>
</p></li>

<li><b>"newindex":</b>
��ֵ��ָ���±� <code>table[key] = value</code> ��


<pre>     function settable_event (table, key, value)
       local h
       if type(table) == "table" then
         local v = rawget(table, key)
         if v ~= nil then rawset(table, key, value); return end
         h = metatable(table).__newindex
         if h == nil then rawset(table, key, value); return end
       else
         h = metatable(table).__newindex
         if h == nil then
           error(������);
         end
       end
       if type(h) == "function" then
         return h(table, key,value)    -- ���ô�����
       else h[key] = value             -- �����ظ���������
       end
     end
</pre><p>
</p></li>

<li><b>"call":</b>
�� Lua ����һ��ֵʱ���á�


<pre>     function function_event (func, ...)
       if type(func) == "function" then
         return func(...)   -- ԭ���ĵ���
       else
         local h = metatable(func).__call
         if h then
           return h(func, ...)
         else
           error(������)
         end
       end
     end
</pre><p>
</p></li>

</ul>




<h2>2.9 - <a name="2.9">����</a></h2>

<p>
����Ϊ thread ��function ���Լ� userdata 
�Ķ��󣬳��� metatable �⻹����������һ����֮�����ı�����
���ǵĻ�����һ������
�� metatable һ��������Ҳ��һ������� table �����������Թ���
ͬһ��������

</p><p>
userdata �Ļ����� Lua ��û�����塣
�������ֻ��Ϊ���ڳ���Ա���һ����������һ�� userdata ��ʱ�ṩ������

</p><p>
�������߳��ϵĻ���������ȫ�ֻ�����
ȫ�ֻ��������������е��߳��Լ��̴߳����ķ�Ƕ�׺���
��ͨ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-loadfile"><code>loadfile</code></a> �� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-loadstring"><code>loadstring</code></a> ����
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-load"><code>load</code></a> ����ȱʡ������
���������Ա� C ����ֱ�ӷ��ʣ��μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.3">��3.3</a>����


</p><p>
������ C �����ϵĻ�������ֱ�ӱ� C ������ʣ��μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.3">��3.3</a>����
���ǻ���Ϊ��� C �����д���������������ȱʡ������


</p><p>
������ Lua �����ϵĻ��������ӹ��ں����ڶ�ȫ�ֱ������μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.3">��2.3</a>�������з��ʡ�
����Ҳ����Ϊ��������ڴ���������������ȱʡ������

</p><p>
�����ͨ������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-setfenv"><code>setfenv</code></a> ���ı�һ�� Lua ����
�������������е��̵߳Ļ�����
����ٿ���������userdata��C �����������̣߳��Ļ����Ļ����ͱ���ʹ�� C API ��



</p><h2>2.10 - <a name="2.10">�����ռ�</a></h2>

<p>
Lua �ṩ��һ���Զ����ڴ������
�����˵�㲻��Ҫ���Ĵ����¶���ķ����ڴ������Ҳ����Ҫ����Щ��������Ҫʱ�������ͷ��ڴ档
Lua ͨ������һ�������ռ������Զ������ڴ棬�Դ�һ����һ��Ļ��������Ķ���
������ָ Lua �в��ٷ��ʵĵ��Ķ���ռ�õ��ڴ档
Lua �����ж��󶼱��Զ�������������
table, userdata�� �������̡߳����ַ�����


</p><p>
Lua ʵ����һ���������������ռ�����
�����������������������ռ����ڣ�
<em>garbage-collector pause</em> �� <em>garbage-collector step multiplier</em> ��


</p><p>
garbage-collector pause �������ռ����ڿ�ʼһ���µ��ռ�����֮ǰҪ�ȴ���á�
�������ֵ�����͵����ռ������������Ĳ���ô������
С�� 1 ��ֵ��ζ���ռ������µ����ڿ�ʼʱ���ٵȴ���
��ֵΪ 2 ��ʱ����ζ������ʹ���ڴ������ﵽԭ��������ʱ�ٿ����µ����ڡ�

</p><p>
step multiplier �������ռ�������ڴ������ٶȡ�
��������ֽ������ռ��������ĸ�������ͬʱ��Ҳʹÿ���ռ��ĳߴ����ӡ�
С�� 1 ��ֵ��ʹ�ռ��������ķǳ��������ܵ����ռ�����Զ���������˵�ǰ���ڡ�
ȱʡֵΪ 2 ������ζ���ռ��������ڴ�����������������С�


</p><p>
�����ͨ���� C �е��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_gc"><code>lua_gc</code></a> ������ Lua �е��� 
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-collectgarbage"><code>collectgarbage</code></a> ���ı���Щ���֡�
���߶����ܰٷֱ���ֵ����˴������ 100 ��ζ��ʵ��ֵ 1 ����
ͨ����Щ��������Ҳ����ֱ�ӿ����ռ��������磬ֹͣ������������


</p><h3>2.10.1 - <a name="2.10.1">�����ռ���Ԫ����</a></h3>

<p>
ʹ�� C API����
����Ը� userdata ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>������һ�������ռ���Ԫ������
���Ԫ����Ҳ����Ϊ�����ӡ�
�������������ö������Դ�������� Lua ���ڴ������Эͬ����
������ر��ļ����������ӡ��������ݿ����ӣ�Ҳ����˵�ͷ����Լ����ڴ棩��

</p><p>
һ�� userdata �ɱ����գ������� metatable ���� <code>__gc</code> ����򡡣�
�����ռ����Ͳ������ջ�����
ȡ����֮���ǣ�Lua �����Ƿŵ�һ���б��С�
���ռ�������Lua ����б��е�ÿ�� userdata ִ����������������ĵȼ۲�����

</p><pre>     function gc_event (udata)
       local h = metatable(udata).__gc
       if h then
         h(udata)
       end
     end
</pre>

<p>
��ÿ�������ռ����ڵĽ�β��ÿ���ڵ�ǰ���ڱ��ռ������� userdata �Ľ����ӻ���
���ǹ���ʱ���������ε��á�
Ҳ����˵���ռ��б��У����һ���ڳ����б������� userdata ��
�����ӻᱻ��һ�����á�


</p><h3>2.10.2 - <a name="2.10.2">Weak Table��������</a></h3>

<p>
<em>weak table</em> ��һ�������� table�������е�Ԫ�ض��������á�
�����ý��������ռ������Ե���
���仰˵��
�����һ�����������ֻ�������ã�
�����ռ����������������

</p><p>
weak table �ļ���ֵ�������� weak �ġ�
���һ�� table ֻ�м��� weak �ģ���ô�������ռ����������ǵļ���
���ǻ���ֹ���������ն�Ӧ��ֵ��
��һ�� table �ļ���ֵ���� weak ʱ���ͼ������ռ������ռ��������ջ�ֵ��
�κ�����£��������ֵ����һ���������ˣ�������ֵ�Ծͻ�� table ���õ���
table �� weak ���Կ���ͨ�������� metatable ������ <code>__mode</code> �����ı䡣
��� <code>__mode</code> ������һ���������ַ� '<code>k</code>' ���ַ���ʱ��
table �ļ����� weak �ġ�
��� <code>__mode</code> ������һ���������ַ� '<code>v</code>' ���ַ���ʱ��
table ��ֵ���� weak �ġ�

</p><p>
�����һ�� table ����һ�� metatable ʹ��֮��
�Ͳ������޸� <code>__mode</code> ���ֵ��
��������� metatable ���Ƶ� table �� weak ��Ϊ�ͳ���δ����ġ�


</p><h2>2.11 - <a name="2.11">Coroutine ��Эͬ���̣�</a></h2>

<p>
Lua ֧�� coroutine ���������Ҳ����ΪЭͬʽ���߳� (<em>collaborative multithreading</em>)����
Lua Ϊÿ�� coroutine �ṩһ��������������·��
Ȼ���Ͷ��߳�ϵͳ�е��̲߳�ͬ��coroutine ֻ����ʽ�ĵ����� yield ����ʱ�Ż����

</p><p>
����һ�� coroutine ��Ҫ����һ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.create"><code>coroutine.create</code></a> ��
��ֻ���յ������������������ coroutine ����������
<code>create</code> ������������һ���µ� coroutine Ȼ�󷵻����Ŀ�����
��һ������Ϊ <em>thread</em> �Ķ��󣩣�
������������ coroutine �����С�


</p><p>
�����һ�ε��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> ʱ��
���贫��ĵ�һ���������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.create"><code>coroutine.create</code></a> �ķ���ֵ��
��ʱ��coroutine ���������ĵ�һ�п�ʼ���С�
���������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> �Ĳ����������� coroutine ����������
�� coroutine ��ʼ���к��������е�������ֹ��������һ�� <em>yields</em> ��


</p><p>
coroutine ����ͨ�����ַ�ʽ����ֹ���У�
һ���������˳���ָ�������������أ����һ��ָ����к�������û����ʽ�ķ���ָ�;
��һ���Ƿ������˳�����������δ�����Ĵ�������ʱ��
��һ������У� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> ���� <b>true</b> ��
����������� coroutine ��������һϵ�з���ֵ��
�ڶ��ַ������������£� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> ���� <b>false</b> ��
��������һ��������Ϣ��

</p><p>
coroutine ���л���ȥ�����Ե��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.yield"><code>coroutine.yield</code></a>��
�� coroutine �г�����֮��ϵ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> ���������أ�
������ yield �������ڲ�ĺ���������Ҳ���ԣ�����˵��
�ⲻ���ڷ������������У�Ҳ������������ֱ�ӻ��ӵ��õ�ĳ���������
�� yield ������£�<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> Ҳ�Ƿ��� <b>true</b>��
��������Щ������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.yield"><code>coroutine.yield</code></a> �Ĳ�����
�ȵ��´����ڼ���ͬ���� coroutine �����ӵ��� yield �Ķϵ㴦������ȥ��
�ϵ㴦 yield �ķ���ֵ���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> ����Ĳ�����


</p><p>
���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.create"><code>coroutine.create</code></a> ��
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.wrap"><code>coroutine.wrap</code></a> �������Ҳ������һ�� coroutine ��
�������������� coroutine ���������Ƿ���һ������ȡ����֮��һ�������������غ������ͻ����� coroutine ���С�
���д�����������Ĳ�����ͬ�ڴ��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> �Ĳ�����
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.wrap"><code>coroutine.wrap</code></a> �᷵������Ӧ���ɳ���һ�������������Ǹ���������
֮����� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> ���ص�ֵ��
�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.resume"><code>coroutine.resume</code></a> ��ͬ��
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-coroutine.wrap"><code>coroutine.wrap</code></a> �������κδ���
���еĴ���Ӧ���ɵ������Լ����ݡ�


</p><p>
��������δ���չʾ��һ�����ӣ�

</p><pre>     function foo (a)
       print("foo", a)
       return coroutine.yield(2*a)
     end
     
     co = coroutine.create(function (a,b)
           print("co-body", a, b)
           local r = foo(a+1)
           print("co-body", r)
           local r, s = coroutine.yield(a+b, a-b)
           print("co-body", r, s)
           return b, "end"
     end)
            
     print("main", coroutine.resume(co, 1, 10))
     print("main", coroutine.resume(co, "r"))
     print("main", coroutine.resume(co, "x", "y"))
     print("main", coroutine.resume(co, "x", "y"))
</pre><p>
���������������õ�������������

</p><pre>     co-body 1       10
     foo     2
     
     main    true    4
     co-body r
     main    true    11      -9
     co-body x       y
     main    true    10      end
     main    false   cannot resume dead coroutine
</pre>


<h1>3 - <a name="3">����ӿڣ�API��</a></h1>

<p>

������������� Lua �� C API ��
Ҳ������������� Lua ͨѶ�õ�һ�� C ������
���е� API ��������ص������Լ�������������ͷ�ļ�
<a name="pdf-lua.h"><code>lua.h</code></a> �С�


</p><p>
��Ȼ����˵���ǡ�����������һ���ּ򵥵� API ���Ժ����ʽ�ṩ�ġ�
���е���Щ�궼ֻʹ�����ǵĲ���һ��
�����˵�һ��������Ҳ���� lua ״̬������
����㲻�赣����Щ���չ��������һЩ�����á�


</p><p>
�����е� C ���У�Lua API ��������ȥ����������Ч�Ժͼ���ԡ�
Ȼ����������ڱ��� Lua ʱ���ϴ�һ���꿪����
���� <code>luaconf.h</code> �ļ��еĺ� <a name="pdf-luai_apicheck"><code>luai_apicheck</code></a>
�Ըı������Ϊ��

</p><h2>3.1 - <a name="3.1">��ջ</a></h2>

<p>
Lua ʹ��һ������ջ���� C ����ֵ��
ջ�ϵĵ�ÿ��Ԫ�ض���һ�� Lua ֵ
��<b>nil</b>�����֣��ַ������ȵȣ���


</p><p>
���ۺ�ʱ Lua ���� C�������õĺ������õ�һ���µ�ջ��
���ջ������ C ���������Ķ�ջ��Ҳ��������ǰ��ջ��
����ע���� C ������� Lua API ���ܷ��ʵ� Lua ״̬���б��ε���֮��Ķ�ջ�е����ݣ�
����������� Lua ���ݸ� C ���������в�����
�� C �������Ҫ���صĽ��Ҳ�����ջ�Է��ظ�������
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_CFunction"><code>lua_CFunction</code></a>����


</p><p>
����������������ջ�� API ��ѯ���������ϸ���ѭջ�Ĳ�������
���ǿ�����һ��������ָ��ջ�ϵ��κ�Ԫ�أ�
��������ָ����ջ�ϵľ���λ�ã���һ��ʼ����
����������ָ��ջ����ʼ��ƫ������
����ϸ��˵��һ�£������ջ�� n ��Ԫ�أ�
��ô���� 1 ��ʾ��һ��Ԫ�أ�Ҳ�������ȱ�ѹ���ջ��Ԫ�أ�
������ n ��ָ���һ��Ԫ�أ�
���� -1 Ҳ��ָ���һ��Ԫ�أ���ջ����Ԫ�أ���
���� -n ��ָ��һ��Ԫ�ء�
��������� 1 ��ջ��֮�䣨Ҳ���ǣ�<code>1 �� abs(index) �� top</code>��
���Ǿ�˵���Ǹ���Ч��������


</p><h2>3.2 - <a name="3.2">��ջ�ߴ�</a></h2>

<p>
����ʹ�� Lua API ʱ���������α�֤�����ԡ�
�ر���Ҫע����ǣ��������ο��Ʋ�Ҫ��ջ�����
�����ʹ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_checkstack"><code>lua_checkstack</code></a> ���������������ö�ջ�ĳߴ硣

</p><p>
���ۺ�ʱ Lua ���� C ��
����ֻ��֤ <a name="pdf-LUA_MINSTACK"><code>LUA_MINSTACK</code></a> ��ô��Ķ�ջ�ռ����ʹ�á�
<code>LUA_MINSTACK</code> һ�㱻����Ϊ 20����
��ˣ�ֻҪ�㲻�ǲ��ϵİ�����ѹջ��ͨ���㲻�ù��Ķ�ջ��С��


</p><p>
���еĲ�ѯ���������Խ���һ��������ֻҪ����������κ�ջ�ṩ�Ŀռ��е�ֵ��
ջ���ṩ�����ռ���ͨ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_checkstack"><code>lua_checkstack</code></a> �����õġ�
��Щ�����������ɽ��ܵ�������ͨ�����ǰ�������Ϊ��

</p><pre>     (index &lt; 0 &amp;&amp; abs(index) &lt;= top) ||
     (index &gt; 0 &amp;&amp; index &lt;= stackspace)
</pre><p>
ע�⣬0 ��Զ������һ���ɽ��ܵ�����������ע�������з��ᵽ��������û���ر�ע���Ļ�����ָ�ɽ��ܵ���������


</p><h2>3.3 - <a name="3.3">α����</a></h2>

<p>
�����ر������⣬�κ�һ�����������Խ�����һ����Ч�����������Ǳ�������α��������
������԰��� C �������һЩ������ջ�ϵ� Lua ֵ��
α���������������̵߳Ļ����������Ļ�����ע��������� C ������ upvalue
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.4">��3.4</a>����


</p><p>
�̵߳Ļ�����Ҳ����ȫ�ֱ����ŵĵط���ͨ����α���� <a name="pdf-LUA_GLOBALSINDEX"><code>LUA_GLOBALSINDEX</code></a> ����
�������е� C �����Ļ��������α���� <a name="pdf-LUA_ENVIRONINDEX"><code>LUA_ENVIRONINDEX</code></a> ֮����


</p><p>
������ó���� table ���������ʺ͸ı�ȫ�ֱ�����ֵ��ֻ��Ҫָ����������λ�á�
�������ԣ�Ҫ����ȫ�ֱ�����ֵ����������

</p><pre>     lua_getfield(L, LUA_GLOBALSINDEX, varname);
</pre>




<h2>3.4 - <a name="3.4">C Closure</a></h2>

<p>
�� C ���������������������п��ܻ��һЩֵ������һ��
Ҳ���Ǵ���һ�� C closure ��
��Щ������������ֵ������ upvalue ��
���ǿ����ں��������õ�ʱ����ʵĵ���
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushcclosure"><code>lua_pushcclosure</code></a>����


</p><p>
���ۺ�ʱȥ���� C ������������ upvalue ��������ָ����α��������
���ǿ����� <a name="lua_upvalueindex"><code>lua_upvalueindex</code></a> �������������Щα������
��һ��������������ֵ���� <code>lua_upvalueindex(1)</code> λ�ô����������ơ�
�κ�����¶������� <code>lua_upvalueindex(<em>n</em>)</code> ����һ�� upvalue ��������
��ʹ��n ����ʵ�ʵ� upvalue ����Ҳ���ԡ��������Բ���һ���ɽ��ܵ���һ����Ч��������


</p><h2>3.5 - <a name="3.5">ע���</a></h2>

<p>
Lua �ṩ��һ��ע���������һ��Ԥ��������ı����������������κ� C �����뱣��� Lua ֵ��
�����������α���� <a name="pdf-LUA_REGISTRYINDEX"><code>LUA_REGISTRYINDEX</code></a> ����λ��
�κ� C �ⶼ���������ű��ﱣ�����ݣ�Ϊ�˷�ֹ��ͻ������Ҫ�ر�С�ĵ�ѡ�������
һ����÷��ǣ��������һ��������Ŀ������ַ�����Ϊ���������߿���ȡ���Լ� C ����
�е�һ����ַ���� light userdata ����ʽ������

</p><p>
ע�����������������ڲ������ʵ�ֵ�����ϵͳ�Ĺ�����һ��˵����Ҫ���������ڱ����;��


</p><h2>3.6 - <a name="3.6">C �еĴ�����</a></h2>

<p>
���ڲ�ʵ���У�Lua ʹ���� C �� <code>longjmp</code> ��������������
�������ʹ�� C++ �Ļ���Ҳ����ѡ�����쳣���μ� <code>luaconf.h</code> �ļ�����
�� Lua �����κδ��󣨱����ڴ����������ʹ����﷨���󡢻���һЩ����ʱ����
���������һ�������ȥ��
Ҳ���ǵ���һ�� long jump ��
�ڱ��������£�Lua ʹ�� <code>setjmp</code> ������һ���ָ��㣻
�κη����Ĵ��󶼻ἤ�������һ���ָ��㡣

</p><p>
�������е� API ���������ܲ������������ڴ�������
�������һЩ���������ڱ��������У�Ҳ����˵���Ǵ�����һ���������������������У���
������ǲ���������������
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a>, <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_close"><code>lua_close</code></a>, <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a>, and <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_cpcall"><code>lua_cpcall</code></a>��


</p><p>
�� C �������Ҳ����ͨ������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_error"><code>lua_error</code></a> ����һ������


</p><h2>3.7 - <a name="3.7">����������</a></h2>

<p>
���������ǰ���ĸ�����г������� C API �еĺ��������͡�


</p><hr><h3><a name="lua_Alloc"><code>lua_Alloc</code></a></h3>
<pre>typedef void * (*lua_Alloc) (void *ud,
                             void *ptr,
                             size_t osize,
                             size_t nsize);</pre>

<p>
Lua ״̬����ʹ�õ��ڴ���������������͡�
�ڴ���亯�������ṩһ������������ <code>realloc</code> ���ֲ���ȫ��ͬ�ĺ�����
���Ĳ�����
<code>ud</code> ��һ���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> ��������ָ�룻
<code>ptr</code> ��һ��ָ���ѷ���������ǽ������·������Ҫ�ͷŵ��ڴ��ָ�룻
<code>osize</code> ���ڴ��ԭ���ĳߴ磻
<code>nsize</code> �����ڴ��ĳߴ硣
�����ֻ�� <code>osize</code> ����ʱ��<code>ptr</code> Ϊ <code>NULL</code> ��
�� <code>nsize</code> ���㣬���������뷵�� <code>NULL</code>��
��� <code>osize</code> �����㣬������Ӧ���ͷŵ� <code>ptr</code> ָ����ڴ�顣
�� <code>nsize</code> �����㣬��������������������ʱ������������ <code>NULL</code> ��
�� <code>nsize</code> ������� <code>osize</code> ����ʱ��������Ӧ�ú� <code>malloc</code>
����ͬ����Ϊ��
�� <code>nsize</code> �� <code>osize</code> ��������ʱ����������Ӧ�� <code>realloc</code>
����һ������Ϊ��
Lua ����������� <code>osize &gt;= nsize</code> ʱ��Զ����ʧ�ܡ�

</p><p>
������һ���򵥵ķ�����������ʵ�֡�
���ʵ�ֱ����ڲ�����У��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_newstate"><code>luaL_newstate</code></a> �ṩ��

</p><pre>     static void *l_alloc (void *ud, void *ptr, size_t osize,
                                                size_t nsize) {
       (void)ud;  (void)osize;  /* not used */
       if (nsize == 0) {
         free(ptr);
         return NULL;
       }
       else
         return realloc(ptr, nsize);
     }
</pre><p>
��δ������ <code>free(NULL)</code> ɶҲ��Ӱ�죬����
<code>realloc(NULL, size)</code> �ȼ��� <code>malloc(size)</code>��
�������� ANSI C ��֤����Ϊ��


</p><hr><h3><a name="lua_atpanic"><code>lua_atpanic</code></a></h3>
<pre>lua_CFunction lua_atpanic (lua_State *L, lua_CFunction panicf);</pre>

<p>
����һ���µ� panic ���ֻţ� ������������ǰһ����


</p><p>
����ڱ�������֮�ⷢ�����κδ���
Lua �ͻ����һ�� panic ���������ŵ��� <code>exit(EXIT_FAILURE)</code>��
�����Ϳ�ʼ�˳���������
��� panic ����������Զ�����أ�������һ�γ���ת������������˳���

</p><p>
panic �������Դ�ջ��ȡ��������Ϣ��


</p><hr><h3><a name="lua_call"><code>lua_call</code></a></h3>
<pre>void lua_call (lua_State *L, int nargs, int nresults);</pre>

<p>
����һ��������


</p><p>
Ҫ����һ����������ѭ����Э�飺
���ȣ�Ҫ���õĺ���Ӧ�ñ�ѹ���ջ��
���ţ�����Ҫ���ݸ���������Ĳ���������ѹջ��
����ָ��һ����������ѹջ��
������һ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a>��
<code>nargs</code> ����ѹ���ջ�Ĳ���������
������������Ϻ����еĲ����Լ��������������ջ��
�������ķ���ֵ��ʱ��ѹ���ջ��
����ֵ�ĸ�����������Ϊ <code>nresults</code> ����
���� <code>nresults</code> �����ó� <a name="pdf-LUA_MULTRET"><code>LUA_MULTRET</code></a>��
����������£����еķ���ֵ����ѹ���ջ�С�
Lua �ᱣ֤����ֵ������ջ�ռ��С�
��������ֵ��������ѹջ����һ������ֵ����ѹջ����
����ڵ��ý��������һ������ֵ��������ջ����


</p><p>
�����ú����ڷ����Ĵ��󽫣�ͨ�� <code>longjmp</code>��һֱ���ס�


</p><p>
����������У����� Lua ����ȼ��������������� C ������һЩ������

</p><pre>     a = f("how", t.x, 14)
</pre><p>
������ C ��Ĵ��룺

</p><pre>     lua_getfield(L, LUA_GLOBALSINDEX, "f");          /* �����õĺ��� */
     lua_pushstring(L, "how");                          /* ��һ������ */
     lua_getfield(L, LUA_GLOBALSINDEX, "t");          /* table ������ */
     lua_getfield(L, -1, "x");         /* ѹ�� t.x ��ֵ���� 2 ��������*/
     lua_remove(L, -2);                           /* �Ӷ�ջ����ȥ 't' */
     lua_pushinteger(L, 14);                           /* �� 3 ������ */
     lua_call(L, 3, 1); /* ���� 'f'������ 3 ������������ȡ 1 ������ֵ */
     lua_setfield(L, LUA_GLOBALSINDEX, "a");      /* ����ȫ�ֱ��� 'a' */
</pre><p>
ע��������δ����ǡ�ƽ�⡱�ģ�
������󣬶�ջ�ָ���ԭ�ɵ����á�
����һ�����õı��ϰ�ߡ�


</p><hr><h3><a name="lua_CFunction"><code>lua_CFunction</code></a></h3>
<pre>typedef int (*lua_CFunction) (lua_State *L);</pre>

<p>
C ���������͡�


</p><p>
Ϊ����ȷ�ĺ� Lua ͨѶ��C ��������ʹ������
�����˲����Լ�����ֵ���ݷ�����Э�飺
C ����ͨ�� Lua �еĶ�ջ�����ܲ�����������������ջ����һ������������ջ����
��ˣ���������ʼ��ʱ��
<code>lua_gettop(L)</code> ���Է��غ����յ��Ĳ���������
��һ������������еĻ��������� 1 �ĵط��������һ������������ <code>lua_gettop(L)</code> ����
����Ҫ�� Lua ����ֵ��ʱ��C ����ֻ��Ҫ������������ѹ����ջ�ϣ���һ������ֵ����ѹ�룩��
Ȼ�󷵻���Щ����ֵ�ĸ�����
����Щ����ֵ֮�µģ���ջ�ϵĶ������ᱻ Lua ������
�� Lua ����һ������ Lua �е��� C ����Ҳ�����кܶ෵��ֵ��

</p><p>
������������еĺ����������������ֲ��������������ǵ�ƽ������ͣ�

</p><pre>     static int foo (lua_State *L) {
       int n = lua_gettop(L);    /* �����ĸ��� */
       lua_Number sum = 0;
       int i;
       for (i = 1; i &lt;= n; i++) {
         if (!lua_isnumber(L, i)) {
           lua_pushstring(L, "incorrect argument");
           lua_error(L);
         }
         sum += lua_tonumber(L, i);
       }
       lua_pushnumber(L, sum/n);   /* ��һ������ֵ */
       lua_pushnumber(L, sum);     /* �ڶ�������ֵ */
       return 2;                   /* ����ֵ�ĸ��� */
     }
</pre>




<hr><h3><a name="lua_checkstack"><code>lua_checkstack</code></a></h3>
<pre>int lua_checkstack (lua_State *L, int extra);</pre>

<p>
ȷ����ջ�������� <code>extra</code> ����λ��
������ܰѶ�ջ��չ����Ӧ�ĳߴ磬�������� false ��
���������Զ������С��ջ��
�����ջ�Ѿ�����Ҫ�Ĵ��ˣ���ô�ͷ������ﲻ������仯��


</p><hr><h3><a name="lua_close"><code>lua_close</code></a></h3>
<pre>void lua_close (lua_State *L);</pre>

<p>
����ָ�� Lua ״̬���е����ж�������������ռ���ص�Ԫ�����Ļ�����������ǣ���
�����ͷ�״̬����ʹ�õ����ж�̬�ڴ档
��һЩƽ̨�ϣ�����Բ��ص������������
��Ϊ���������������ʱ�����е���Դ����Ȼ���ͷŵ��ˡ�
��һ���棬�������еĳ��򣬱���һ����̨�������һ�� web ��������
��������Ҫ���ǵ�ʱ���Ӧ���ͷŵ����״̬�����������Ա���״̬�����ŵĹ���


</p><hr><h3><a name="lua_concat"><code>lua_concat</code></a></h3>
<pre>void lua_concat (lua_State *L, int n);</pre>

<p>
����ջ���� <code>n</code> ��ֵ��
Ȼ����Щֵ��ջ�����ѽ������ջ����
��� <code>n</code> Ϊ 1 ���������һ���ַ�������ջ�ϣ���������ʲô����������
��� <code>n</code> Ϊ 0 �������һ���մ���

�������� Lua �д���������ɣ��μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.4">��2.5.4</a> ����




</p><hr><h3><a name="lua_cpcall"><code>lua_cpcall</code></a></h3>
<pre>int lua_cpcall (lua_State *L, lua_CFunction func, void *ud);</pre>

<p>
�Ա���ģʽ���� C ���� <code>func</code> ��
<code>func</code> ֻ���ܴӶ�ջ���õ�һ�����������ǰ����� <code>ud</code> �� light userdata��
���д���ʱ��
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_cpcall"><code>lua_cpcall</code></a> ���غ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> ��ͬ�Ĵ�����룬
����ջ�����´������
�����������㣬�������޸Ķ�ջ��
���д� <code>func</code> �ڷ��ص�ֵ���ᱻ�ӵ���





</p><hr><h3><a name="lua_createtable"><code>lua_createtable</code></a></h3>
<pre>void lua_createtable (lua_State *L, int narr, int nrec);</pre>

<p>
����һ���µĿ� table ѹ���ջ��
����� table ����Ԥ���� <code>narr</code> ��Ԫ�ص�����ռ�
�Լ� <code>nrec</code> ��Ԫ�صķ�����ռ䡣
������ȷ֪��������Ҫ���ٸ�Ԫ��ʱ��Ԥ����ͷǳ����á�
����㲻֪��������ʹ�ú��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newtable"><code>lua_newtable</code></a>��





</p><hr><h3><a name="lua_dump"><code>lua_dump</code></a></h3>
<pre>int lua_dump (lua_State *L, lua_Writer writer, void *data);</pre>

<p>
�Ѻ��� dump �ɶ����� chunk ��
��������ջ���� Lua ������������Ȼ���������Ķ����� chunk ��
���� dump �����Ķ������ٴμ��أ����صĽ�����൱��ԭ���ĺ�����
�����ڲ��� chunk ��ʱ��<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> 
ͨ�����ú��� <code>writer</code> ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Writer"><code>lua_Writer</code></a>��
��д�����ݣ������ <code>data</code> �����ᱻ���� <code>writer</code> ��

</p><p>
���һ����д���� (writer) ����ֵ����Ϊ��������ķ���ֵ���أ�
0 ��ʾû�д���

</p><p>
������������ Lua ���ص�����ջ��



</p><hr><h3><a name="lua_equal"><code>lua_equal</code></a></h3>
<pre>int lua_equal (lua_State *L, int index1, int index2);</pre>

<p>
������� Lua �� <code>==</code> ���������壬���� <code>index1</code> �� <code>index2</code>
�е�ֵ��ͬ�Ļ������� 1 ��
���򷵻� 0 ��
����κ�һ��������ЧҲ�᷵�� 0��



</p><hr><h3><a name="lua_error"><code>lua_error</code></a></h3>
<pre>int lua_error (lua_State *L);</pre>

<p>
����һ�� Lua ����
������Ϣ��ʵ���Ͽ������κ����͵� Lua ֵ�����뱻����ջ����
�����������һ�γ���ת������������ٷ��ء�
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_error"><code>luaL_error</code></a>����





</p><hr><h3><a name="lua_gc"><code>lua_gc</code></a></h3>
<pre>int lua_gc (lua_State *L, int what, int data);</pre>

<p>
���������ռ�����


</p><p>
���������������� <code>what</code> �����ֲ�ͬ������

</p><ul>

<li><b><code>LUA_GCSTOP</code>:</b>
ֹͣ�����ռ�����
</li>

<li><b><code>LUA_GCRESTART</code>:</b>
���������ռ�����
</li>

<li><b><code>LUA_GCCOLLECT</code>:</b>
����һ�������������ռ�ѭ����
</li>

<li><b><code>LUA_GCCOUNT</code>:</b>
���� Lua ʹ�õ��ڴ��������� K �ֽ�Ϊ��λ����
</li>

<li><b><code>LUA_GCCOUNTB</code>:</b>
���ص�ǰ�ڴ�ʹ�������� 1024 ��������
</li>

<li><b><code>LUA_GCSTEP</code>:</b>
����һ�����������ռ���
������ <code>data</code> ���ƣ�Խ���ֵ��ζ��Խ�ಽ����
������庬�壨�������ֱ�ʾ�˶��٣���δ��׼����
�����������������������ʵ���ԵĲ���
<code>data</code> ��ֵ��
�����һ��������һ�������ռ����ڣ����ط��� 1 ��
</li>

<li><b><code>LUA_GCSETPAUSE</code>:</b>
�� <code>data</code>/100 ����Ϊ <em>garbage-collector pause</em> ����ֵ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.10">��2.10</a>����
����������ǰ��ֵ��
</li>

<li><b><code>LUA_GCSETSTEPMUL</code>:</b>
�� <code>arg</code>/100 ���ó� <em>step multiplier</em> ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.10">��2.10</a>����
����������ǰ��ֵ��
</li>

</ul>




<hr><h3><a name="lua_getallocf"><code>lua_getallocf</code></a></h3>
<pre>lua_Alloc lua_getallocf (lua_State *L, void **ud);</pre>

<p>
���ظ���״̬�����ڴ������������
��� <code>ud</code> ���� <code>NULL</code> ��Lua �ѵ���
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> ʱ������Ǹ�ָ����� <code>*ud</code> ��




</p><hr><h3><a name="lua_getfenv"><code>lua_getfenv</code></a></h3>
<pre>void lua_getfenv (lua_State *L, int index);</pre>

<p>
��������ֵ�Ļ�����ѹ���ջ��




</p><hr><h3><a name="lua_getfield"><code>lua_getfield</code></a></h3>
<pre>void lua_getfield (lua_State *L, int index, const char *k);</pre>

<p>
�� <code>t[k]</code> ֵѹ���ջ��
����� <code>t</code> ��ָ��Ч���� <code>index</code> ָ���ֵ��
�� Lua �У�����������ܴ�����Ӧ "index" �¼���Ԫ����
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����





</p><hr><h3><a name="lua_getglobal"><code>lua_getglobal</code></a></h3>
<pre>void lua_getglobal (lua_State *L, const char *name);</pre>

<p>
��ȫ�ֱ��� <code>name</code> ���ֵѹ���ջ��
�������һ���궨������ģ�

</p><pre>     #define lua_getglobal(L,s)  lua_getfield(L, LUA_GLOBALSINDEX, s)
</pre>




<hr><h3><a name="lua_getmetatable"><code>lua_getmetatable</code></a></h3>
<pre>int lua_getmetatable (lua_State *L, int index);</pre>

<p>
�Ѹ�������ָ���ֵ��Ԫ��ѹ���ջ��
���������Ч���������ֵû��Ԫ����
���������� 0 ���Ҳ�����ջ��ѹ�κζ�����


</p><hr><h3><a name="lua_gettable"><code>lua_gettable</code></a></h3>
<pre>void lua_gettable (lua_State *L, int index);</pre>

<p>
�� <code>t[k]</code> ֵѹ���ջ��
����� <code>t</code> ��ָ��Ч���� <code>index</code> ָ���ֵ��
�� <code>k</code> ����ջ���ŵ�ֵ��

</p><p>
��������ᵯ����ջ�ϵ� key ���ѽ������ջ����ͬλ�ã���
�� Lua �У�����������ܴ�����Ӧ "index" �¼���Ԫ����
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����



</p><hr><h3><a name="lua_gettop"><code>lua_gettop</code></a></h3>
<pre>int lua_gettop (lua_State *L);</pre>

<p>
����ջ��Ԫ�ص�������
��Ϊ�����Ǵ� 1 ��ʼ��ŵģ�
�������������ڶ�ջ�ϵ�Ԫ�ظ�������˷��� 0 ��ʾ��ջΪ�գ���



</p><hr><h3><a name="lua_insert"><code>lua_insert</code></a></h3>
<pre>void lua_insert (lua_State *L, int index);</pre>

<p>
��ջ��Ԫ�ز���ָ������Ч��������
�������ƶ��������֮�ϵ�Ԫ�ء�
��Ҫ��α�������������������
��Ϊα������������ָ���ջ�ϵ�λ�á�



</p><hr><h3><a name="lua_Integer"><code>lua_Integer</code></a></h3>
<pre>typedef ptrdiff_t lua_Integer;</pre>

<p>
������ͱ����� Lua API ��������ֵ��

</p><p>
ȱʡʱ���������Ϊ <code>ptrdiff_t</code> ��
�������ͨ���ǻ����ܴ���������������͡�



</p><hr><h3><a name="lua_isboolean"><code>lua_isboolean</code></a></h3>
<pre>int lua_isboolean (lua_State *L, int index);</pre>

<p>
������������ֵ����Ϊ boolean ʱ������ 1 �����򷵻� 0 ��



</p><hr><h3><a name="lua_iscfunction"><code>lua_iscfunction</code></a></h3>
<pre>int lua_iscfunction (lua_State *L, int index);</pre>

<p>
������������ֵ��һ�� C ����ʱ������ 1 �����򷵻� 0 ��




</p><hr><h3><a name="lua_isfunction"><code>lua_isfunction</code></a></h3>
<pre>int lua_isfunction (lua_State *L, int index);</pre>

<p>
������������ֵ��һ�������� C �� Lua �������ɣ�ʱ������ 1 �����򷵻� 0 ��


</p><hr><h3><a name="lua_islightuserdata"><code>lua_islightuserdata</code></a></h3>
<pre>int lua_islightuserdata (lua_State *L, int index);</pre>

<p>
������������ֵ��һ�� light userdata ʱ������ 1 �����򷵻� 0 ��


</p><hr><h3><a name="lua_isnil"><code>lua_isnil</code></a></h3>
<pre>int lua_isnil (lua_State *L, int index);</pre>

<p>
������������ֵ�� <b>nil</b> ʱ������ 1 �����򷵻� 0 ��



</p><hr><h3><a name="lua_isnumber"><code>lua_isnumber</code></a></h3>
<pre>int lua_isnumber (lua_State *L, int index);</pre>

<p>
������������ֵ��һ�����֣�����һ����ת��Ϊ���ֵ��ַ���ʱ������ 1 �����򷵻� 0 ��



</p><hr><h3><a name="lua_isstring"><code>lua_isstring</code></a></h3>
<pre>int lua_isstring (lua_State *L, int index);</pre>

<p>
������������ֵ��һ���ַ�������һ�����֣���������ת�����ַ�����ʱ������ 1 �����򷵻� 0 ��


</p><hr><h3><a name="lua_istable"><code>lua_istable</code></a></h3>
<pre>int lua_istable (lua_State *L, int index);</pre>

<p>
������������ֵ��һ�� table ʱ������ 1 �����򷵻� 0 ��



</p><hr><h3><a name="lua_isthread"><code>lua_isthread</code></a></h3>
<pre>int lua_isthread (lua_State *L, int index);</pre>

<p>
������������ֵ��һ�� thread ʱ������ 1 �����򷵻� 0 ��


</p><hr><h3><a name="lua_isuserdata"><code>lua_isuserdata</code></a></h3>
<pre>int lua_isuserdata (lua_State *L, int index);</pre>

<p>
������������ֵ��һ�� userdata �������������� userdata ���� light userdata ��ʱ������ 1 �����򷵻� 0 ��


</p><hr><h3><a name="lua_lessthan"><code>lua_lessthan</code></a></h3>
<pre>int lua_lessthan (lua_State *L, int index1, int index2);</pre>

<p>
������� <code>index1</code> ����ֵС��
���� <code>index2</code> ����ֵʱ������ 1 ��
���򷵻� 0 ��
��������ѭ Lua �е� <code>&lt;</code> ������������˵���п��ܵ���Ԫ��������
����κ�һ��������Ч��Ҳ�᷵�� 0 ��


</p><hr><h3><a name="lua_load"><code>lua_load</code></a></h3>
<pre>int lua_load (lua_State *L,
              lua_Reader reader,
              void *data,
              const char *chunkname);</pre>

<p>
����һ�� Lua chunk ��
���û�д���
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> ��һ������õ� chunk ��Ϊһ��
Lua ����ѹ���ջ��
����ѹ�������Ϣ��
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> �ķ���ֵ�����ǣ�

</p><ul>

<li><b>0:</b> û�д���</li>

<li><b><a name="pdf-LUA_ERRSYNTAX"><code>LUA_ERRSYNTAX</code></a>:</b>
��Ԥ����ʱ�����﷨����</li>

<li><b><a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-LUA_ERRMEM"><code>LUA_ERRMEM</code></a>:</b>
�ڴ�������</li>

</ul>

<p>
��������������� chunk ��������ȥ��������


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> ���Զ���� chunk ���ı��Ļ��Ƕ����Ƶģ�
Ȼ������Ӧ�ļ��ز������μ����� <code>luac</code>����


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> ����ʹ��һ���û��ṩ�� <code>reader</code> ������
��ȡ chunk ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Reader"><code>lua_Reader</code></a>����
<code>data</code> �����ᱻ�����ȡ��������


</p><p>
<code>chunkname</code> ����������Ը��� chunk һ�����֣�
������ֱ����ڳ�����Ϣ�͵�����Ϣ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.8">��3.8</a>����



</p><hr><h3><a name="lua_newstate"><code>lua_newstate</code></a></h3>
<pre>lua_State *lua_newstate (lua_Alloc f, void *ud);</pre>

<p>
������һ���µĶ�����״̬����
����������ˣ���Ϊ�ڴ����⣩���� <code>NULL</code> ��
���� <code>f</code> ��һ��������������
Lua ��ͨ�����������״̬�������е��ڴ���������
�ڶ������� <code>ud</code> �����ָ�뽫��ÿ�ε��÷�����ʱ��ֱ�Ӵ��롣


</p><hr><h3><a name="lua_newtable"><code>lua_newtable</code></a></h3>
<pre>void lua_newtable (lua_State *L);</pre>

<p>
����һ���� table ������֮ѹ���ջ��
���ȼ��� <code>lua_createtable(L, 0, 0)</code> ��





</p><hr><h3><a name="lua_newthread"><code>lua_newthread</code></a></h3>
<pre>lua_State *lua_newthread (lua_State *L);</pre>

<p>
����һ�����̣߳�������ѹ���ջ��
������ά������̵߳� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_State"><code>lua_State</code></a> ָ�롣
����������ص���״̬������ԭ��״̬���е����ж��󣨱���һЩ table����
�������ж�����ִ�ж�ջ��

</p><p>
û����ʽ�ĺ������������رջ����ٵ�һ���̡߳�
�̸߳����� Lua ����һ���������ռ�����Ŀ֮һ��


</p><hr><h3><a name="lua_newuserdata"><code>lua_newuserdata</code></a></h3>
<pre>void *lua_newuserdata (lua_State *L, size_t size);</pre>

<p>
��������������һ��ָ����С���ڴ�飬
���ڴ���ַ��Ϊһ�������� userdata ѹ���ջ�������������ַ��


</p><p>
userdata ���� Lua �е� C ֵ��
������ userdata ����һ���ڴ档
����һ�����󣨾��� table �����Ķ��󣩣�
����봴�������������Լ���Ԫ�����������ڱ�����ʱ�����Ա���⵽��
һ�������� userdata ֻ�����Լ���ȣ��ڵ��ڵ�ԭ�������£���

</p><p>
�� Lua ͨ�� <code>gc</code> Ԫ��������һ�������� userdata ʱ��
Lua �������Ԫ�������� userdata ���Ϊ����ֹ��
�ȵ���� userdata �ٴα��ռ���ʱ��Lua ���ͷŵ���ص��ڴ档


</p><hr><h3><a name="lua_next"><code>lua_next</code></a></h3>
<pre>int lua_next (lua_State *L, int index);</pre>

<p>
��ջ�ϵ���һ�� key��������
Ȼ�������ָ���ı��� key-value����ֵ����ѹ���ջ
��ָ�� key �������һ (next) �ԣ���
����������޸���Ԫ�أ�
��ô <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_next"><code>lua_next</code></a> ������ 0 ��ʲôҲ��ѹ���ջ����


</p><p>
���͵ı��������������ģ�

</p><pre>     /* table �������� 't' �� */
     lua_pushnil(L);  /* ��һ�� key */
     while (lua_next(L, t) != 0) {
       /* ��һ�� 'key' �������� -2 ���� �� 'value' �������� -1 ���� */
       printf("%s - %s\n",
              lua_typename(L, lua_type(L, -2)),
              lua_typename(L, lua_type(L, -1)));
       /* �Ƴ� 'value' ������ 'key' ����һ�ε��� */
       lua_pop(L, 1);
     }
</pre>

<p>
�ڱ���һ�ű���ʱ��
��Ҫֱ�Ӷ� key ���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> ��
������֪����� key һ����һ���ַ�����
���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> �п��ܸı��������λ�õ�ֵ��
������һ�ε��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_next"><code>lua_next</code></a> ���Ӱ�졣




</p><hr><h3><a name="lua_Number"><code>lua_Number</code></a></h3>
<pre>typedef double lua_Number;</pre>

<p>
Lua �����ֵ����͡�
ȷʡ�� double ������������� <code>luaconf.h</code> ���޸�����


</p><p>
ͨ���޸������ļ�����Ըı� Lua �������������������ͣ����磺float ���� long ����



</p><hr><h3><a name="lua_objlen"><code>lua_objlen</code></a></h3>
<pre>size_t lua_objlen (lua_State *L, int index);</pre>

<p>
����ָ������������ֵ�ĳ��ȡ�
���� string ���Ǿ����ַ����ĳ��ȣ�
���� table ����ȡ���Ȳ����� ('<code>#</code>') �Ľ����
���� userdata ������Ϊ�������ڴ��ĳߴ磻
��������ֵ��Ϊ 0 ��


</p><hr><h3><a name="lua_pcall"><code>lua_pcall</code></a></h3>
<pre>lua_pcall (lua_State *L, int nargs, int nresults, int errfunc);</pre>

<p>
�Ա���ģʽ����һ��������


</p><p>
<code>nargs</code> �� <code>nresults</code> �ĺ�����
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a> �е���ͬ��
����ڵ��ù�����û�з�������
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> ����Ϊ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a> ��ȫһ�¡�
���ǣ�����д������Ļ���
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> �Ჶ������
Ȼ��ѵ�һ��ֵ��������Ϣ��ѹ���ջ��Ȼ�󷵻ش����롣
ͬ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a> һ����
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> ���ǰѺ������������Ĳ�����ջ���Ƴ���


</p><p>
��� <code>errfunc</code> �� 0 ��
������ջ���Ĵ�����Ϣ�ͺ�ԭʼ������Ϣ��ȫһ�¡�
����<code>errfunc</code> �ͱ������Ǵ�����������ջ�ϵ�������
���ڵ�ǰ��ʵ����������������α��������
�ڷ�������ʱ����ʱ��
��������ᱻ���ö��������Ǵ�����Ϣ��
�����������ķ���ֵ���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> ��Ϊ������Ϣ�����ڶ�ջ�ϡ�


</p><p>
���͵��÷��У������������������ڳ�����Ϣ�ϼ��ϸ���ĵ�����Ϣ������ջ������Ϣ (stack traceback) ��
��Щ��Ϣ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> ���غ���Ϊջ�Ѿ�չ�� (unwound) ��
�����ռ������ˡ�


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a> �����ڵ��óɹ�ʱ���� 0 ��
���򷵻����£������� <code>lua.h</code> �еģ���������е�һ����

</p><ul>

<li><b><a name="pdf-LUA_ERRRUN"><code>LUA_ERRRUN</code></a>:</b>
����ʱ����
</li>

<li><b><a name="pdf-LUA_ERRMEM"><code>LUA_ERRMEM</code></a>:</b>
�ڴ�������
�������ִ���Lua ���ò��˴�����������
</li>

<li><b><a name="pdf-LUA_ERRERR"><code>LUA_ERRERR</code></a>:</b>
�����д���������ʱ�����Ĵ���
</li>

</ul>




<hr><h3><a name="lua_pop"><code>lua_pop</code></a></h3>
<pre>void lua_pop (lua_State *L, int n);</pre>

<p>
�Ӷ�ջ�е��� <code>n</code> ��Ԫ�ء�


</p><hr><h3><a name="lua_pushboolean"><code>lua_pushboolean</code></a></h3>
<pre>void lua_pushboolean (lua_State *L, int b);</pre>

<p>
�� <code>b</code> ��Ϊһ�� boolean ֵѹ���ջ��



</p><hr><h3><a name="lua_pushcclosure"><code>lua_pushcclosure</code></a></h3>
<pre>void lua_pushcclosure (lua_State *L, lua_CFunction fn, int n);</pre>

<p>
��һ���µ� C closure ѹ���ջ��

</p><p>
��������һ�� C ����������Ը�������һЩֵ�����������ڴ���һ�� C closure
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.4">��3.4</a>����
���������ۺ�����ʱ�����ã���Щֵ�����Ա�����������ʵ���
Ϊ�˽�һЩֵ������һ�� C �����ϣ�
������Щֵ��Ҫ�ȱ�ѹ���ջ������ж��ֵ����һ����ѹ����
���������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushcclosure"><code>lua_pushcclosure</code></a>
�������� closure ������� C ����ѹ����ջ�ϡ�
���� <code>n</code> ��֮�����ж��ٸ�ֵ��Ҫ�����������ϡ�
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushcclosure"><code>lua_pushcclosure</code></a> Ҳ�����Щֵ��ջ�ϵ�����



</p><hr><h3><a name="lua_pushcfunction"><code>lua_pushcfunction</code></a></h3>
<pre>void lua_pushcfunction (lua_State *L, lua_CFunction f);</pre>

<p>
��һ�� C ����ѹ���ջ��
�����������һ�� C ����ָ�룬����һ������Ϊ <code>function</code> �� Lua ֵ
ѹ���ջ�������ջ����ֵ������ʱ����������Ӧ�� C ������

</p><p>
ע�ᵽ Lua �е��κκ�����������ѭ��ȷ��Э�������ղ����ͷ���ֵ
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_CFunction"><code>lua_CFunction</code></a>����


</p><p>
<code>lua_pushcfunction</code> ����Ϊһ���궨����ֵģ�

</p><pre>     #define lua_pushcfunction(L,f)  lua_pushcclosure(L,f,0)
</pre>




<hr><h3><a name="lua_pushfstring"><code>lua_pushfstring</code></a></h3>
<pre>const char *lua_pushfstring (lua_State *L, const char *fmt, ...);</pre>

<p>
��һ����ʽ�������ַ���ѹ���ջ��Ȼ�󷵻�����ַ�����ָ�롣
���� C ���� <code>sprintf</code> �Ƚ��񣬲�����һЩ��Ҫ������

</p><ul>

<li>
������ҪΪ�������ռ䣺
������һ�� Lua �ַ������� Lua ���������ڴ����
��ͬʱͨ�������ռ����ͷ��ڴ棩��
</li>

<li>
���ת���ǳ������ޡ�
��֧�� flag �����ȣ�����ָ�����ȡ�
��ֻ֧��������Щ��
'<code>%%</code>' ������һ�� '<code>%</code>'����
'<code>%s</code>' ������һ��������ֹ�����ַ�����û�г������ƣ���
'<code>%f</code>' ������һ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Number"><code>lua_Number</code></a>����
'<code>%p</code>' ������һ��ָ�����һ��ʮ������������
'<code>%d</code>' ������һ�� <code>int</code>)��
'<code>%c</code>' ����һ�� <code>int</code> ��Ϊһ���ַ����룩��
</li>

</ul>




<hr><h3><a name="lua_pushinteger"><code>lua_pushinteger</code></a></h3>
<pre>void lua_pushinteger (lua_State *L, lua_Integer n);</pre>

<p>
�� <code>n</code> ��Ϊһ������ѹջ��





</p><hr><h3><a name="lua_pushlightuserdata"><code>lua_pushlightuserdata</code></a></h3>
<pre>void lua_pushlightuserdata (lua_State *L, void *p);</pre>

<p>
��һ�� light userdata ѹջ��


</p><p>
userdata �� Lua �б�ʾһ�� C ֵ��
light userdata ��ʾһ��ָ�롣
����һ��������һ����ֵ��
�㲻��Ҫר�Ŵ���������Ҳû�ж����� metatable ��
����Ҳ���ᱻ�ռ�����Ϊ��������Ҫ��������
ֻҪ��ʾ�� C ��ַ��ͬ������ light userdata ����ȡ�



</p><hr><h3><a name="lua_pushlstring"><code>lua_pushlstring</code></a></h3>
<pre>void lua_pushlstring (lua_State *L, const char *s, size_t len);</pre>

<p>
��ָ�� <code>s</code> ָ��ĳ���Ϊ <code>len</code> ���ַ���ѹջ��
Lua ������ַ�����һ���ڴ濽�������Ǹ���һ����������
��� <code>s</code> �����ڴ��ں������غ󣬿����ͷŵ�����������������;��
�ַ����ڿ��Ա��������ַ���



</p><hr><h3><a name="lua_pushnil"><code>lua_pushnil</code></a></h3>
<pre>void lua_pushnil (lua_State *L);</pre>

<p>
��һ�� nil ѹջ��




</p><hr><h3><a name="lua_pushnumber"><code>lua_pushnumber</code></a></h3>
<pre>void lua_pushnumber (lua_State *L, lua_Number n);</pre>

<p>
��һ������ <code>n</code> ѹջ��




</p><hr><h3><a name="lua_pushstring"><code>lua_pushstring</code></a></h3>
<pre>void lua_pushstring (lua_State *L, const char *s);</pre>

<p>
��ָ�� <code>s</code> ָ��������β���ַ���ѹջ��
Lua ������ַ�����һ���ڴ濽�������Ǹ���һ����������
��� <code>s</code> �����ڴ��ں������غ󣬿����ͷŵ�����������������;��
�ַ����в��ܰ��������ַ�����һ�����������ַ�����Ϊ���ַ����Ľ�����




</p><hr><h3><a name="lua_pushthread"><code>lua_pushthread</code></a></h3>
<pre>int lua_pushthread (lua_State *L);</pre>

<p>
�� <code>L</code> ���ṩ���߳�ѹջ��
�������߳��ǵ�ǰ״̬�������̵߳Ļ������� 1 ��


</p><hr><h3><a name="lua_pushvalue"><code>lua_pushvalue</code></a></h3>
<pre>void lua_pushvalue (lua_State *L, int index);</pre>

<p>
�Ѷ�ջ�ϸ�����Ч����������Ԫ����һ������ѹջ��



</p><hr><h3><a name="lua_pushvfstring"><code>lua_pushvfstring</code></a></h3>
<pre>const char *lua_pushvfstring (lua_State *L,
                              const char *fmt,
                              va_list argp);</pre>

<p>
�ȼ��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushfstring"><code>lua_pushfstring</code></a>��
�������� <code>va_list</code> ���ղ������������ÿɱ�������ʵ�ʲ�����



</p><hr><h3><a name="lua_rawequal"><code>lua_rawequal</code></a></h3>
<pre>int lua_rawequal (lua_State *L, int index1, int index2);</pre>

<p>
����������� <code>index1</code> �� <code>index2</code> ����ֵ�򵥵����
��������Ԫ�������򷵻� 1 ��
���򷵻� 0 ��
����κ�һ��������ЧҲ���� 0 ��


</p><hr><h3><a name="lua_rawget"><code>lua_rawget</code></a></h3>
<pre>void lua_rawget (lua_State *L, int index);</pre>

<p>
������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_gettable"><code>lua_gettable</code></a>��
������һ��ֱ�ӷ��ʣ�������Ԫ��������



</p><hr><h3><a name="lua_rawgeti"><code>lua_rawgeti</code></a></h3>
<pre>void lua_rawgeti (lua_State *L, int index, int n);</pre>

<p>
�� <code>t[n]</code> ��ֵѹջ��
����� <code>t</code> ��ָ�������� <code>index</code> ����һ��ֵ��
����һ��ֱ�ӷ��ʣ�����˵�������ᴥ��Ԫ������


</p><hr><h3><a name="lua_rawset"><code>lua_rawset</code></a></h3>
<pre>void lua_rawset (lua_State *L, int index);</pre>

<p>
������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_settable"><code>lua_settable</code></a>��
��������һ��ֱ�Ӹ�ֵ��������Ԫ��������


</p><hr><h3><a name="lua_rawseti"><code>lua_rawseti</code></a></h3>
<pre>void lua_rawseti (lua_State *L, int index, int n);</pre>

<p>
�ȼ��� <code>t[n] = v</code>��
����� <code>t</code> ��ָ�������� <code>index</code> ����һ��ֵ��
�� <code>v</code> ��ջ����ֵ��


</p><p>
�����������ֵ����ջ��
��ֵ������ֱ�ӵģ�����˵�����ᴥ��Ԫ������


</p><hr><h3><a name="lua_Reader"><code>lua_Reader</code></a></h3>
<pre>typedef const char * (*lua_Reader) (lua_State *L,
                                    void *data,
                                    size_t *size);</pre>

<p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> �õ��Ķ�ȡ��������
ÿ������Ҫһ���µ� chunk ��ʱ��
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> �͵��ö�ȡ����
ÿ�ζ��ᴫ��һ������ <code>data</code> ��
��ȡ����Ҫ���غ����µ� chunk ��һ���ڴ��ָ�룬
���� <code>size</code> ��Ϊ����ڴ�Ĵ�С��
�ڴ���������һ�κ���������֮ǰһֱ���ڡ�
��ȡ������ͨ������һ�� <code>NULL</code> ��ָʾ chunk ������
��ȡ�����ܷ��ض���飬ÿ�������������Ĵ�����ĳߴ硣



</p><hr><h3><a name="lua_register"><code>lua_register</code></a></h3>
<pre>void lua_register (lua_State *L,
                   const char *name,
                   lua_CFunction f);</pre>

<p>
�� C ���� <code>f</code> �赽ȫ�ֱ��� <code>name</code> �С�
��ͨ��һ���궨�壺

</p><pre>     #define lua_register(L,n,f) \
            (lua_pushcfunction(L, f), lua_setglobal(L, n))
</pre>




<hr><h3><a name="lua_remove"><code>lua_remove</code></a></h3>
<pre>void lua_remove (lua_State *L, int index);</pre>

<p>
�Ӹ�����Ч�������Ƴ�һ��Ԫ�أ�
���������֮�ϵ�����Ԫ����������������϶��
������α�������������������
��Ϊα��������ָ����ʵ��ջ�ϵ�λ�á�




</p><hr><h3><a name="lua_replace"><code>lua_replace</code></a></h3>
<pre>void lua_replace (lua_State *L, int index);</pre>

<p>
��ջ��Ԫ���ƶ�������λ�ã����Ұ����ջ��Ԫ�ص�������
���ƶ��κ�Ԫ�أ�������Ǹ�λ�ô���ֵ�����ǵ�����





</p><hr><h3><a name="lua_resume"><code>lua_resume</code></a></h3>
<pre>int lua_resume (lua_State *L, int narg);</pre>

<p>
�ڸ����߳������������һ�� coroutine ��

</p><p>
Ҫ����һ�� coroutine �Ļ���������Ҫ����һ�����߳�
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newthread"><code>lua_newthread</code></a> ����
Ȼ��������������ɲ���ѹ�����̵߳Ķ�ջ�ϣ�
������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> ��
�� <code>narg</code> ��Ϊ�����ĸ�����
��ε��û��� coroutine ����ʱ���ǽ������к󷵻ء�
����������ʱ����ջ�л��д��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_yield"><code>lua_yield</code></a> ������ֵ��
���������������з���ֵ��
��� coroutine �л�ʱ��<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> ����
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-LUA_YIELD"><code>LUA_YIELD</code></a> ��
���� coroutine ����������û���κδ���ʱ������ 0 ��
����д��򷵻ش�����루�μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pcall"><code>lua_pcall</code></a>����
�ڷ������������£�
��ջû��չ����
��������ʹ�� debug API ����������
������Ϣ����ջ����
Ҫ��������һ�� coroutine �Ļ��������Ҫ���� <code>yield</code>
������ķ���ֵѹ���ջ��Ȼ����� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> ��





</p><hr><h3><a name="lua_setallocf"><code>lua_setallocf</code></a></h3>
<pre>void lua_setallocf (lua_State *L, lua_Alloc f, void *ud);</pre>

<p>
��ָ��״̬���ķ������������ɴ���ָ�� <code>ud</code> �� <code>f</code> ��



</p><hr><h3><a name="lua_setfenv"><code>lua_setfenv</code></a></h3>
<pre>int lua_setfenv (lua_State *L, int index);</pre>

<p>
�Ӷ�ջ�ϵ���һ�� table ��������Ϊָ��������ֵ���»�����
���ָ����������ֵ�����Ǻ����ֲ����̻߳��� userdata ��
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_setfenv"><code>lua_setfenv</code></a> �᷵�� 0 ��
���򷵻� 1 ��



</p><hr><h3><a name="lua_setfield"><code>lua_setfield</code></a></h3>
<pre>void lua_setfield (lua_State *L, int index, const char *k);</pre>

<p>
��һ���ȼ��� <code>t[k] = v</code> �Ĳ�����
���� <code>t</code> �Ǹ�������Ч���� <code>index</code> ����ֵ��
�� <code>v</code> ��ջ�����Ǹ�ֵ��


</p><p>
��������������ֵ������ջ��
���� Lua ��һ��������������ܴ���һ�� "newindex" �¼���Ԫ����
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����





</p><hr><h3><a name="lua_setglobal"><code>lua_setglobal</code></a></h3>
<pre>void lua_setglobal (lua_State *L, const char *name);</pre>

<p>
�Ӷ�ջ�ϵ���һ��ֵ���������赽ȫ�ֱ��� <code>name</code> �С�
����һ���궨�������

</p><pre>     #define lua_setglobal(L,s)   lua_setfield(L, LUA_GLOBALSINDEX, s)
</pre>




<hr><h3><a name="lua_setmetatable"><code>lua_setmetatable</code></a></h3>
<pre>int lua_setmetatable (lua_State *L, int index);</pre>

<p>
��һ�� table ������ջ����������Ϊ������������ֵ�� metatable ��



</p><hr><h3><a name="lua_settable"><code>lua_settable</code></a></h3>
<pre>void lua_settable (lua_State *L, int index);</pre>

<p>
��һ���ȼ��� <code>t[k] = v</code> �Ĳ�����
���� <code>t</code> ��һ��������Ч���� <code>index</code> ����ֵ��
<code>v</code> ָջ����ֵ��
�� <code>k</code> ��ջ��֮�µ��Ǹ�ֵ��


</p><p>
���������Ѽ���ֵ���Ӷ�ջ�е�����
���� Lua ��һ��������������ܴ��� "newindex" �¼���Ԫ����
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.8">��2.8</a>����





</p><hr><h3><a name="lua_settop"><code>lua_settop</code></a></h3>
<pre>void lua_settop (lua_State *L, int index);</pre>

<p>
�������������κοɽ��ܵ������Լ� 0 ��
�����Ѷ�ջ��ջ����Ϊ���������
����µ�ջ����ԭ���Ĵ󣬳������ֵ���Ԫ�ؽ�����Ϊ <b>nil</b> ��
��� <code>index</code> Ϊ 0 ����ջ������Ԫ���Ƴ���





</p><hr><h3><a name="lua_State"><code>lua_State</code></a></h3>
<pre>typedef struct lua_State lua_State;</pre>

<p>
һ����͸���Ľṹ�������������� Lua ��������״̬��
Lua ������ȫ������ģ�
��û���κ�ȫ�ֱ�����
����ע���� C �﷨����˵��Ҳ����Ȼ�����磬�� table ��ʵ����
����һ����̬ȫ�ֱ��� dummynode_ ����������ȷʹ��ʱ����Ӱ��������ԡ�
ֻ����һ����������� lua �⣬��С����ͬһ���̿ռ��д������� lua ��ʵ�ֵĴ���Ļ���
��� dummynode_ ��ͬ�ĵ�ַ�ᵼ��һЩ���⡣��
���е���Ϣ������������ṹ�С�

</p><p>
���״̬����ָ�������Ϊ��һ���������ݸ�ÿһ���⺯����
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> ��һ�����⣬
����������ͷ����һ�� Lua ״̬����





</p><hr><h3><a name="lua_status"><code>lua_status</code></a></h3>
<pre>int lua_status (lua_State *L);</pre>

<p>
�����߳� <code>L</code> ��״̬��


</p><p>
�������߳�״̬�� 0 ��
���߳�ִ����ϻ���һ������ʱ��״ֵ̬�Ǵ����롣
����̱߳�����״̬Ϊ <a name="pdf-LUA_YIELD"><code>LUA_YIELD</code></a> ��





</p><hr><h3><a name="lua_toboolean"><code>lua_toboolean</code></a></h3>
<pre>int lua_toboolean (lua_State *L, int index);</pre>

<p>
��ָ�����������ĵ� Lua ֵת��Ϊһ�� C �е� boolean ֵ�� 0 ���� 1 ����
�� Lua ���������в���һ����
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_toboolean"><code>lua_toboolean</code></a> ����κ�
��ͬ�� <b>false</b> �� <b>nil</b> ��ֵ���� 1 ���أ�
����ͷ��� 0 ��
�����һ����Ч����ȥ����Ҳ�᷵�� 0 ��
���������ֻ���������� boolean ֵ������Ҫʹ��
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_isboolean"><code>lua_isboolean</code></a> ������ֵ�����͡���





</p><hr><h3><a name="lua_tocfunction"><code>lua_tocfunction</code></a></h3>
<pre>lua_CFunction lua_tocfunction (lua_State *L, int index);</pre>

<p>
�Ѹ����������� Lua ֵת��Ϊһ�� C ������
���ֵ������һ�� C ������������Ǿͷ���
<code>NULL</code> ��





</p><hr><h3><a name="lua_tointeger"><code>lua_tointeger</code></a></h3>
<pre>lua_Integer lua_tointeger (lua_State *L, int idx);</pre>

<p>
�Ѹ����������� Lua ֵת��Ϊ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Integer"><code>lua_Integer</code></a> 
����һ���з����������͡�
��� Lua ֵ������һ�����ֻ���һ������ת��Ϊ���ֵ��ַ���
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">��2.2.1</a>����
����<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tointeger"><code>lua_tointeger</code></a> ���� 0 ��


</p><p>
������ֲ���һ��������
�ض�С�����ֵķ�ʽû�б���ȷ���塣




</p><hr><h3><a name="lua_tolstring"><code>lua_tolstring</code></a></h3>
<pre>const char *lua_tolstring (lua_State *L, int index, size_t *len);</pre>

<p>
�Ѹ����������� Lua ֵת��Ϊһ�� C �ַ�����
��� <code>len</code> ��Ϊ <code>NULL</code> ��
�������ַ��������赽 <code>*len</code> �С�
��� Lua ֵ������һ���ַ�������һ�����֣�
���򷵻ط��� <code>NULL</code> ��
���ֵ��һ�����֣�<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> 
����Ѷ�ջ�е��Ǹ�ֵ��ʵ������ת��Ϊһ���ַ�����
��������һ������ʱ�򣬰� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a>
�����ڼ��ϣ����ת���п��ܵ��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_next"><code>lua_next</code></a> Ū������


</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> ���� Lua ״̬����
�ַ������Զ���ָ�롣
����ַ������ܱ�֤ �� C Ҫ��ģ����һ���ַ�Ϊ�� ('<code>\0</code>') ��
�������������ַ����ڰ�������������㡣
��Ϊ Lua �п��ܷ��������ռ���
���Բ���֤ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> ���ص�ָ�룬
�ڶ�Ӧ��ֵ�Ӷ�ջ���Ƴ�����Ȼ��Ч��




</p><hr><h3><a name="lua_tonumber"><code>lua_tonumber</code></a></h3>
<pre>lua_Number lua_tonumber (lua_State *L, int index);</pre>

<p>
�Ѹ����������� Lua ֵת��Ϊ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Number"><code>lua_Number</code></a>
����һ�� C ���ͣ��μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Number"><code>lua_Number</code></a> ����
��� Lua ֵ������һ�����ֻ���һ����ת��Ϊ���ֵ��ַ���
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.2.1">��2.2.1</a> ����
����<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tonumber"><code>lua_tonumber</code></a> ���� 0 ��




</p><hr><h3><a name="lua_topointer"><code>lua_topointer</code></a></h3>
<pre>const void *lua_topointer (lua_State *L, int index);</pre>

<p>
�Ѹ�����������ֵת��Ϊһ��� C ָ�� (<code>void*</code>) ��
���ֵ������һ�� userdata ��table ��thread ����һ�� function ��
����<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_topointer"><code>lua_topointer</code></a> ���� <code>NULL</code> ��
��ͬ�Ķ����в�ͬ��ָ�롣
�����ڰ�ָ����ת��ԭ�����͵ķ�����


</p><p>
�������ͨ��ֻΪ���� debug ��Ϣ�á�




</p><hr><h3><a name="lua_tostring"><code>lua_tostring</code></a></h3>
<pre>const char *lua_tostring (lua_State *L, int index);</pre>

<p>
�ȼ��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_tolstring"><code>lua_tolstring</code></a> �������� <code>len</code> ��Ϊ <code>NULL</code> ��


</p><hr><h3><a name="lua_tothread"><code>lua_tothread</code></a></h3>
<pre>lua_State *lua_tothread (lua_State *L, int index);</pre>

<p>
�Ѹ�����������ֵת��Ϊһ�� Lua �̣߳��� <code>lua_State*</code> ��������
���ֵ������һ���̣߳����������� <code>NULL</code> ��




</p><hr><h3><a name="lua_touserdata"><code>lua_touserdata</code></a></h3>
<pre>void *lua_touserdata (lua_State *L, int index);</pre>

<p>
���������������ֵ��һ�������� userdata �����������ڴ��ĵ�ַ��
���ֵ��һ�� light userdata ����ô�ͷ�������ʾ��ָ�롣
���򣬷��� <code>NULL</code> ��



</p><hr><h3><a name="lua_type"><code>lua_type</code></a></h3>
<pre>int lua_type (lua_State *L, int index);</pre>

<p>
���ظ�����������ֵ�����ͣ�
��������Чʱ�򷵻� <code>LUA_TNONE</code>
������ָһ��ָ���ջ�ϵĿ�λ�õ���������
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_type"><code>lua_type</code></a> ���ص�������һЩ���� <code>lua.h</code> �ж���ĳ�����
<code>LUA_TNIL</code> ��
<code>LUA_TNUMBER</code> ��
<code>LUA_TBOOLEAN</code> ��
<code>LUA_TSTRING</code> ��
<code>LUA_TTABLE</code> ��
<code>LUA_TFUNCTION</code> ��
<code>LUA_TUSERDATA</code> ��
<code>LUA_TTHREAD</code> ��
<code>LUA_TLIGHTUSERDATA</code> ��





</p><hr><h3><a name="lua_typename"><code>lua_typename</code></a></h3>
<pre>const char *lua_typename  (lua_State *L, int tp);</pre>

<p>
���� <code>tp</code> ��ʾ����������
��� <code>tp</code> ������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_type"><code>lua_type</code></a> ���ܷ��ص�ֵ��֮һ��





</p><hr><h3><a name="lua_Writer"><code>lua_Writer</code></a></h3>
<pre>typedef int (*lua_Writer) (lua_State *L,
                           const void* p,
                           size_t sz,
                           void* ud);</pre>

<p>
�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> �õ���д����������
ÿ�� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> ������һ���µ� chunk �����������д������
����Ҫд��Ļ��� (<code>p</code>) �����ĳߴ� (<code>sz</code>) ��
���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> �Ĳ��� <code>data</code> ��


</p><p>
д�����᷵��һ�������룺
0 ��ʾû�д���
���ֵ����ʾһ�����󣬲��һ��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_dump"><code>lua_dump</code></a> ֹͣ�ٴε���д������


</p><hr><h3><a name="lua_xmove"><code>lua_xmove</code></a></h3>
<pre>void lua_xmove (lua_State *from, lua_State *to, int n);</pre>

<p>
���� <em>ͬһ��</em> ȫ��״̬���²�ͬ�߳��е�ֵ��

</p><p>
���������� <code>from</code> �Ķ�ջ�е��� <code>n</code> ��ֵ��
Ȼ�������ѹ�� <code>to</code> �Ķ�ջ�С�





</p><hr><h3><a name="lua_yield"><code>lua_yield</code></a></h3>
<pre>int lua_yield  (lua_State *L, int nresults);</pre>

<p>
�г�һ�� coroutine ��

</p><p>
�������ֻ����һ�� C �����ķ��ر���ʽ�е��á����£�

</p><pre>     return lua_yield (L, nresults);
</pre><p>
��һ�� C ������������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_yield"><code>lua_yield</code></a> ��
���������е� coroutine ���������й���
Ȼ��������� coroutine �õ��Ǵζ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> �ĵ��þͷ����ˡ�
���� <code>nresults</code> ָ���Ƕ�ջ����Ҫ���صĽ����������Щ����ֵ�������ݸ�
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_resume"><code>lua_resume</code></a> ��







</p><h2>3.8 - <a name="3.8">���Խӿ�</a></h2>

<p>
Lua û���ڽ��ĵ�����ʩ��
ȡ����֮�����ṩ��һЩ�����ӿں͹��ӡ�
������Щ�ӿڣ���������һЩ��ͬ���͵ĵ�������
���ܷ���������������һЩ��Ҫ�ӽ�������ȡ�����ڲ���Ϣ���Ĺ��ߡ�


</p><hr><h3><a name="lua_Debug"><code>lua_Debug</code></a></h3>
<pre>typedef struct lua_Debug {
  int event;
  const char *name;           /* (n) */
  const char *namewhat;       /* (n) */
  const char *what;           /* (S) */
  const char *source;         /* (S) */
  int currentline;            /* (l) */
  int nups;                   /* (u) upvalue ���� */
  int linedefined;            /* (S) */
  int lastlinedefined;        /* (S) */
  char short_src[LUA_IDSIZE]; /* (S) */
  /* ˽�в��� */
  <em>������</em>
} lua_Debug;</pre>

<p>
һ������Я����к����ĸ�����Ϣ�Ľṹ��
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getstack"><code>lua_getstack</code></a> ����д����ṹ�е�˽�в��֣�
��Щ�����Ժ���õ���
���� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getinfo"><code>lua_getinfo</code></a> ���������
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Debug"><code>lua_Debug</code></a>
��������Ϣ����Щ��

</p><p>
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Debug"><code>lua_Debug</code></a> �еĸ����������к��壺

</p><ul>

<li><b><code>source</code>:</b>
��������Ƕ�����һ���ַ����У�<code>source</code> ��������ַ�����
�������������һ���ļ��У�
<code>source</code> ��һ���� '<code>@</code>' ��ͷ���ļ�����
</li>

<li><b><code>short_src</code>:</b>
һ�����ɴ�ӡ�汾���� <code>source</code>�����ڳ�����Ϣ��
</li>

<li><b><code>linedefined</code>:</b>
�������忪ʼ�����кš�
</li>

<li><b><code>lastlinedefined</code>:</b>
����������������кš�
</li>

<li><b><code>what</code>:</b>
���������һ�� Lua ��������Ϊһ���ַ��� <code>"Lua"</code> ��
�����һ�� C ��������Ϊ <code>"C"</code>��
�������һ�� chunk �����岿�֣���Ϊ <code>"main"</code>��
�����һ������β���õĺ�������Ϊ <code>"tail"</code> ��
�������£�Lua û�й��ں����ı����Ϣ��
</li>

<li><b><code>currentline</code>:</b>
������������ִ�е���һ�С�
���ṩ�����к���Ϣ��ʱ��<code>currentline</code> ����Ϊ -1 ��
</li>

<li><b><code>name</code>:</b>
����������һ�����������֡�
��Ϊ Lua �еĺ���Ҳ��һ��ֵ��
��������û�й̶������֣�
һЩ����������ȫ�ָ��ϱ�����ֵ��
��һЩ���ܽ���ֻ�Ǳ�������һ�� table �С�
<code>lua_getinfo</code> �������麯�������������õģ��Դ����ҵ�һ���ʺϵ����֡�
������Ҳ������֣�<code>name</code> �ͱ�����Ϊ <code>NULL</code> ��
</li>

<li><b><code>namewhat</code>:</b>
��ʵ <code>name</code> ��
<code>namewhat</code> ��ֵ������
<code>"global"</code>, <code>"local"</code>, <code>"method"</code>,
<code>"field"</code>, <code>"upvalue"</code>, ���� <code>""</code> ���մ�����
��ȡ���ں������������á�
��Lua �ÿմ���ʾ����ѡ������ϣ�
</li>

<li><b><code>nups</code>:</b>
������ upvalue �ĸ�����
</li>

</ul>




<hr><h3><a name="lua_gethook"><code>lua_gethook</code></a></h3>
<pre>lua_Hook lua_gethook (lua_State *L);</pre>

<p>
���ص�ǰ�Ĺ��Ӻ�����




</p><hr><h3><a name="lua_gethookcount"><code>lua_gethookcount</code></a></h3>
<pre>int lua_gethookcount (lua_State *L);</pre>

<p>
���ص�ǰ���Ӽ�����





</p><hr><h3><a name="lua_gethookmask"><code>lua_gethookmask</code></a></h3>
<pre>int lua_gethookmask (lua_State *L);</pre>

<p>
���ص�ǰ�Ĺ������� (mask) ��




</p><hr><h3><a name="lua_getinfo"><code>lua_getinfo</code></a></h3>
<pre>int lua_getinfo (lua_State *L, const char *what, lua_Debug *ar);</pre>

<p>
����һ��ָ���ĺ����������õ���Ϣ��


</p><p>
������ȡ��һ�κ������õ���Ϣʱ��
���� <code>ar</code> ������һ����Ч�Ļ�ļ�¼��
������¼������ǰһ�ε��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getstack"><code>lua_getstack</code></a> �õ��ģ�
����һ������ ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Hook"><code>lua_Hook</code></a>���õ��Ĳ�����


</p><p>
���ڻ�ȡһ����������Ϣʱ�����԰��������ѹ���ջ��
Ȼ��� <code>what</code> �ַ������ַ� '<code>&gt;</code>' ��ͷ��
���������£�<code>lua_getinfo</code> ��ջ���ϵ�����������

���磬��֪������ <code>f</code> ����һ�ж���ģ�
����������д��룺

</p><pre>     lua_Debug ar;
     lua_getfield(L, LUA_GLOBALSINDEX, "f");  /* ȡ��ȫ�ֱ��� 'f' */
     lua_getinfo(L, "&gt;S", &amp;ar);
     printf("%d\n", ar.linedefined);
</pre>

<p>
<code>what</code> �ַ����е�ÿ���ַ���ɸѡ���ṹ <code>ar</code>
�ṹ��һЩ��������䣬���ǰ�һ��ֵѹ���ջ��

</p><ul>

<li><b>'<code>n</code>':</b> ��� <code>name</code> �� <code>namewhat</code> ��
</li>

<li><b>'<code>S</code>':</b>
��� <code>source</code>�� <code>short_src</code>��
<code>linedefined</code>�� <code>lastlinedefined</code>���Լ� <code>what</code> ��
</li>

<li><b>'<code>l</code>':</b> ��� <code>currentline</code> ��
</li>

<li><b>'<code>u</code>':</b> ��� <code>nups</code> ��
</li>

<li><b>'<code>f</code>':</b>
������������ָ�����𴦺���ѹ���ջ��
����ע��һ�����ڻ�ȡ���������е���Ϣ��
�������� ar �е�˽�в������ṩ��
������ڻ�ȡ��̬��������ô��ֱ�Ӱ�ָ����������ѹ�ض�ջ��
��������ͨ���������塣�� 

</li>

<li><b>'<code>L</code>':</b>
ѹһ�� table ��ջ����� table �е�������������������������Щ������Ч�С�
����Ч��ָ��ʵ�ʴ�����У�
�����������ϵ���С�
��Ч�а������к�ֻ��ע�͵��С���
</li>

</ul>

<p>
������������᷵�� 0
�����磬<code>what</code> ����һ����Чѡ���


</p><hr><h3><a name="lua_getlocal"><code>lua_getlocal</code></a></h3>
<pre>const char *lua_getlocal (lua_State *L, lua_Debug *ar, int n);</pre>

<p>
�Ӹ������¼�л�ȡһ���ֲ���������Ϣ��
���� <code>ar</code> ������һ����Ч�Ļ�ļ�¼��
������¼������ǰһ�ε��� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getstack"><code>lua_getstack</code></a> �õ��ģ�
����һ������ ���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Hook"><code>lua_Hook</code></a>���õ��Ĳ�����
���� <code>n</code> ����ѡ��Ҫ�����ĸ��ֲ�����
�� 1 ��ʾ��һ���������Ǽ���ĵ�һ���ֲ��������Դ����ƣ�ֱ�����һ���ֲ���������
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getlocal"><code>lua_getlocal</code></a> �ѱ�����ֵѹ���ջ�������������֡�


</p><p>
�� '(' ����С���ţ���ʼ�ı���ָ�ڲ�����
��ѭ�����Ʊ�������ʱ������C �����ֲ���������


</p><p>
���������ھֲ������ĸ���ʱ������ <code>NULL</code> ��ʲôҲ��ѹ�룩��



</p><hr><h3><a name="lua_getstack"><code>lua_getstack</code></a></h3>
<pre>int lua_getstack (lua_State *L, int level, lua_Debug *ar);</pre>

<p>
��ȡ������������ʱջ����Ϣ��


</p><p>
������������������еĸ������𴦵ĺ����Ļ��¼����д
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Debug"><code>lua_Debug</code></a> �ṹ��һ���֡�
0 ����ʾ��ǰ���еĺ�����
�� n+1 �����ĺ������ǵ��õ� n ����������һ����
���û�д���<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getstack"><code>lua_getstack</code></a> ���� 1 ��
�����ô���ļ�����ڶ�ջ��ȵ�ʱ�򣬷��� 0 ��



</p><hr><h3><a name="lua_getupvalue"><code>lua_getupvalue</code></a></h3>
<pre>const char *lua_getupvalue (lua_State *L, int funcindex, int n);</pre>

<p>
��ȡһ�� closure �� upvalue ��Ϣ��
������ Lua ������upvalue �Ǻ�����Ҫʹ�õ��ⲿ�ֲ�������
�����Щ������������ closure �С���
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getupvalue"><code>lua_getupvalue</code></a> ��ȡ�� <code>n</code> �� upvalue ��
����� upvalue ��ֵѹ���ջ�����ҷ����������֡�
<code>funcindex</code> ָ���ջ�� closure ��λ�á�
�� ��Ϊ upvalue �����������ж���Ч����������û���ر�Ĵ���
��ˣ���������ĸ��������š���


</p><p>
�������ű� upvalue �������ʱ�򣬷��� <code>NULL</code> �����Ҳ���ѹ���κζ�����
���� C ��������������ÿմ� <code>""</code> ��ʾ���� upvalue �����֡�


</p><hr><h3><a name="lua_Hook"><code>lua_Hook</code></a></h3>
<pre>typedef void (*lua_Hook) (lua_State *L, lua_Debug *ar);</pre>

<p>
���ڵ��ԵĹ��Ӻ������͡�

</p><p>
���ۺ�ʱ���ӱ����ã����Ĳ��� <code>ar</code> �е� <code>event</code> ��
������Ϊ�������ӵ��¼���
Lua ����Щ�¼�����Ϊ���³�����
<a name="pdf-LUA_HOOKCALL"><code>LUA_HOOKCALL</code></a>�� <a name="pdf-LUA_HOOKRET"><code>LUA_HOOKRET</code></a>,
<a name="pdf-LUA_HOOKTAILRET"><code>LUA_HOOKTAILRET</code></a>�� <a name="pdf-LUA_HOOKLINE"><code>LUA_HOOKLINE</code></a>��
and <a name="pdf-LUA_HOOKCOUNT"><code>LUA_HOOKCOUNT</code></a>��
����֮�⣬���� line �¼���<code>currentline</code> ��Ҳ�����á�
Ҫ���� <code>ar</code> �е�������
���ӱ������ <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getinfo"><code>lua_getinfo</code></a>��
���ڷ����¼���<code>event</code> ������ֵ������ <code>LUA_HOOKRET</code>��
������ <code>LUA_HOOKTAILRET</code> ��
���ں�һ�������Lua ���һ����������β����Ҳģ���һ�������¼�������
�������ģ��ķ����¼������� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getinfo"><code>lua_getinfo</code></a> û��ʲô���á�

</p><p>
�� Lua ������һ�������ڲ�ʱ���������ε������Թ��ӵĵ��á�
Ҳ����˵�����һ�����Ӻ������ٵ��� Lua ��ִ��һ����������һ�� chunk ��
���ִ�в������ᴥ���κεĹ��ӡ�



</p><hr><h3><a name="lua_sethook"><code>lua_sethook</code></a></h3>
<pre>int lua_sethook (lua_State *L, lua_Hook f, int mask, int count);</pre>

<p>
����һ�������ù��Ӻ�����

</p><p>
���� <code>f</code> �ǹ��Ӻ�����
<code>mask</code> ָ������Щ�¼�ʱ����ã�
��������һ��λ��������
<a name="pdf-LUA_MASKCALL"><code>LUA_MASKCALL</code></a>��
<a name="pdf-LUA_MASKRET"><code>LUA_MASKRET</code></a>��
<a name="pdf-LUA_MASKLINE"><code>LUA_MASKLINE</code></a>��
�Լ� <a name="pdf-LUA_MASKCOUNT"><code>LUA_MASKCOUNT</code></a>��
���� <code>count</code> ֻ�� mask �а����� <code>LUA_MASKCOUNT</code> �������塣
����ÿ���¼������ӱ����õ�����������£�

</p><ul>

<li><b>call hook:</b> �ڽ���������һ������ʱ�����á�
���ӽ��� Lua ����һ���º����󣬺�����ȡ����ǰ�����á�
</li>

<li><b>return hook:</b> �ڽ�������һ�������з���ʱ���á�
���ӽ��� Lua �뿪����֮ǰ����һ�̱����á�
����Ȩ���ʱ��������س�ȥ����Щֵ��
<small>����ע��ԭ�� (You have no access to the values to be returned by the function) ��ˡ�
������Ȩ���ʡ�һ��ֵ����ȶ��
ĳЩ���������Է��ʵ�һЩ������Ϊ (*temporary) �ľֲ�������
��Щ�������������� (*temporary) ����ָ�ľ��Ƿ���ֵ��
�������� Lua �������������һЩ�Ż�������ֱ�ӷ���һ���������ľֲ�������
��ô���Ҳ�����Ӧ�� (*temporary) �����ˡ������ϣ�����ֵһ�������ڴ˿̵ľֲ������У�
���ҿ��Է�������ֻ���޷�ȷ������Щ���ˡ��������ʱ�������ڵ������ֲ�������
�ǲ���֤��Ч�ġ����� return hook ����һ����ʵ���Ѿ��˳������ڲ������л��ڣ�
����ֵռ�õľֲ������ռ��Ժ�Ĳ��֣����п����� hook �����������Ƕ��ı䡣��
</small>
</li>

<li><b>line hook:</b> �ڽ�����׼����ʼִ���µ�һ�д���ʱ��
������ת�����д�����ʱ����ʹ��ͬһ������ת�������á�
������¼������� Lua ִ��һ�� Lua ����ʱ��������
</li>

<li><b>count hook:</b> �ڽ�����ÿִ�� <code>count</code> ��ָ��󱻵��á�
������¼������� Lua ִ��һ�� Lua ����ʱ��������
</li>

</ul>

<p>
���ӿ���ͨ������ <code>mask</code> Ϊ�����Ρ�




</p><hr><h3><a name="lua_setlocal"><code>lua_setlocal</code></a></h3>
<pre>const char *lua_setlocal (lua_State *L, lua_Debug *ar, int n);</pre>

<p>
���ø������¼�еľֲ�������ֵ��
���� <code>ar</code> �� <code>n</code> �� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getlocal"><code>lua_getlocal</code></a> �е�һ��
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getlocal"><code>lua_getlocal</code></a>����
<a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_setlocal"><code>lua_setlocal</code></a> ��ջ����ֵ��������Ȼ�󷵻ر��������֡�
���Ὣֵ��ջ��������


</p><p>
���������ھֲ������ĸ���ʱ������ <code>NULL</code> ��ʲôҲ����������




</p><hr><h3><a name="lua_setupvalue"><code>lua_setupvalue</code></a></h3>
<pre>const char *lua_setupvalue (lua_State *L, int funcindex, int n);</pre>

<p>
���� closure �� upvalue ��ֵ��
����ջ����ֵ���������� upvalue ������ upvalue �����֡�
���� <code>funcindex</code> �� <code>n</code> �� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getupvalue"><code>lua_getupvalue</code></a> �е�һ��
���μ� <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getupvalue"><code>lua_getupvalue</code></a>����


</p><p>
���������� upvalue �ĸ���ʱ������ <code>NULL</code> ��ʲôҲ����������





</p><h1>4 - <a name="4">The Auxiliary Library</a></h1>

<p>

The <em>auxiliary library</em> provides several convenient functions
to interface C with Lua.
While the basic API provides the primitive functions for all 
interactions between C and Lua,
the auxiliary library provides higher-level functions for some
common tasks.


</p><p>
All functions from the auxiliary library
are defined in header file <code>lauxlib.h</code> and
have a prefix <code>luaL_</code>.


</p><p>
All functions in the auxiliary library are built on
top of the basic API,
and so they provide nothing that cannot be done with this API.


</p><p>
Several functions in the auxiliary library are used to
check C&nbsp;function arguments.
Their names are always <code>luaL_check*</code> or <code>luaL_opt*</code>.
All of these functions raise an error if the check is not satisfied.
Because the error message is formatted for arguments
(e.g., "<code>bad argument #1</code>"),
you should not use these functions for other stack values.



</p><h2>4.1 - <a name="4.1">Functions and Types</a></h2>

<p>
Here we list all functions and types from the auxiliary library
in alphabetical order.



</p><hr><h3><a name="luaL_addchar"><code>luaL_addchar</code></a></h3>
<pre>void luaL_addchar (luaL_Buffer *B, char c);</pre>

<p>
Adds the character <code>c</code> to the buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).





</p><hr><h3><a name="luaL_addlstring"><code>luaL_addlstring</code></a></h3>
<pre>void luaL_addlstring (luaL_Buffer *B, const char *s, size_t l);</pre>

<p>
Adds the string pointed to by <code>s</code> with length <code>l</code> to
the buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).
The string may contain embedded zeros.





</p><hr><h3><a name="luaL_addsize"><code>luaL_addsize</code></a></h3>
<pre>void luaL_addsize (luaL_Buffer *B, size_t n);</pre>

<p>
Adds to the buffer <code>B</code> (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>)
a string of length <code>n</code> previously copied to the
buffer area (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_prepbuffer"><code>luaL_prepbuffer</code></a>).





</p><hr><h3><a name="luaL_addstring"><code>luaL_addstring</code></a></h3>
<pre>void luaL_addstring (luaL_Buffer *B, const char *s);</pre>

<p>
Adds the zero-terminated string pointed to by <code>s</code>
to the buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).
The string may not contain embedded zeros.





</p><hr><h3><a name="luaL_addvalue"><code>luaL_addvalue</code></a></h3>
<pre>void luaL_addvalue (luaL_Buffer *B);</pre>

<p>
Adds the value at the top of the stack
to the buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).
Pops the value.


</p><p>
This is the only function on string buffers that can (and must)
be called with an extra element on the stack,
which is the value to be added to the buffer.





</p><hr><h3><a name="luaL_argcheck"><code>luaL_argcheck</code></a></h3>
<pre>void luaL_argcheck (lua_State *L,
                    int cond,
                    int narg,
                    const char *extramsg);</pre>

<p>
Checks whether <code>cond</code> is true.
If not, raises an error with the following message,
where <code>func</code> is retrieved from the call stack:

</p><pre>     bad argument #&lt;narg&gt; to &lt;func&gt; (&lt;extramsg&gt;)
</pre>




<hr><h3><a name="luaL_argerror"><code>luaL_argerror</code></a></h3>
<pre>int luaL_argerror (lua_State *L, int narg, const char *extramsg);</pre>

<p>
Raises an error with the following message,
where <code>func</code> is retrieved from the call stack:

</p><pre>     bad argument #&lt;narg&gt; to &lt;func&gt; (&lt;extramsg&gt;)
</pre>

<p>
This function never returns,
but it is an idiom to use it in C&nbsp;functions
as <code>return luaL_argerror(<em>args</em>)</code>.





</p><hr><h3><a name="luaL_Buffer"><code>luaL_Buffer</code></a></h3>
<pre>typedef struct luaL_Buffer luaL_Buffer;</pre>

<p>
Type for a <em>string buffer</em>.


</p><p>
A string buffer allows C&nbsp;code to build Lua strings piecemeal.
Its pattern of use is as follows:

</p><ul>

<li>First you declare a variable <code>b</code> of type <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>.</li>

<li>Then you initialize it with a call <code>luaL_buffinit(L, &amp;b)</code>.</li>

<li>
Then you add string pieces to the buffer calling any of
the <code>luaL_add*</code> functions.
</li>

<li>
You finish by calling <code>luaL_pushresult(&amp;b)</code>.
This call leaves the final string on the top of the stack.
</li>

</ul>

<p>
During its normal operation,
a string buffer uses a variable number of stack slots.
So, while using a buffer, you cannot assume that you know where
the top of the stack is.
You can use the stack between successive calls to buffer operations
as long as that use is balanced;
that is,
when you call a buffer operation,
the stack is at the same level
it was immediately after the previous buffer operation.
(The only exception to this rule is <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_addvalue"><code>luaL_addvalue</code></a>.)
After calling <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_pushresult"><code>luaL_pushresult</code></a> the stack is back to its
level when the buffer was initialized,
plus the final string on its top.





</p><hr><h3><a name="luaL_buffinit"><code>luaL_buffinit</code></a></h3>
<pre>void luaL_buffinit (lua_State *L, luaL_Buffer *B);</pre>

<p>
Initializes a buffer <code>B</code>.
This function does not allocate any space;
the buffer must be declared as a variable
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).





</p><hr><h3><a name="luaL_callmeta"><code>luaL_callmeta</code></a></h3>
<pre>int luaL_callmeta (lua_State *L, int obj, const char *e);</pre>

<p>
Calls a metamethod.


</p><p>
If the object at index <code>obj</code> has a metatable and this
metatable has a field <code>e</code>,
this function calls this field and passes the object as its only argument.
In this case this function returns 1 and pushes onto the
stack the value returned by the call.
If there is no metatable or no metamethod,
this function returns 0 (without pushing any value on the stack).





</p><hr><h3><a name="luaL_checkany"><code>luaL_checkany</code></a></h3>
<pre>void luaL_checkany (lua_State *L, int narg);</pre>

<p>
Checks whether the function has an argument
of any type (including <b>nil</b>) at position <code>narg</code>.





</p><hr><h3><a name="luaL_checkint"><code>luaL_checkint</code></a></h3>
<pre>int luaL_checkint (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a number
and returns this number cast to an <code>int</code>.





</p><hr><h3><a name="luaL_checkinteger"><code>luaL_checkinteger</code></a></h3>
<pre>lua_Integer luaL_checkinteger (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a number
and returns this number cast to a <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Integer"><code>lua_Integer</code></a>.





</p><hr><h3><a name="luaL_checklong"><code>luaL_checklong</code></a></h3>
<pre>long luaL_checklong (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a number
and returns this number cast to a <code>long</code>.





</p><hr><h3><a name="luaL_checklstring"><code>luaL_checklstring</code></a></h3>
<pre>const char *luaL_checklstring (lua_State *L, int narg, size_t *l);</pre>

<p>
Checks whether the function argument <code>narg</code> is a string
and returns this string;
if <code>l</code> is not <code>NULL</code> fills <code>*l</code>
with the string's length.





</p><hr><h3><a name="luaL_checknumber"><code>luaL_checknumber</code></a></h3>
<pre>lua_Number luaL_checknumber (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a number
and returns this number.





</p><hr><h3><a name="luaL_checkoption"><code>luaL_checkoption</code></a></h3>
<pre>int luaL_checkoption (lua_State *L,
                      int narg,
                      const char *def,
                      const char *const lst[]);</pre>

<p>
Checks whether the function argument <code>narg</code> is a string and
searches for this string in the array <code>lst</code>
(which must be NULL-terminated).
Returns the index in the array where the string was found.
Raises an error if the argument is not a string or
if the string cannot be found.


</p><p>
If <code>def</code> is not <code>NULL</code>,
the function uses <code>def</code> as a default value when
there is no argument <code>narg</code> or if this argument is <b>nil</b>.


</p><p>
This is a useful function for mapping strings to C&nbsp;enums.
(The usual convention in Lua libraries is
to use strings instead of numbers to select options.)





</p><hr><h3><a name="luaL_checkstack"><code>luaL_checkstack</code></a></h3>
<pre>void luaL_checkstack (lua_State *L, int sz, const char *msg);</pre>

<p>
Grows the stack size to <code>top + sz</code> elements,
raising an error if the stack cannot grow to that size.
<code>msg</code> is an additional text to go into the error message.





</p><hr><h3><a name="luaL_checkstring"><code>luaL_checkstring</code></a></h3>
<pre>const char *luaL_checkstring (lua_State *L, int narg);</pre>

<p>
Checks whether the function argument <code>narg</code> is a string
and returns this string.





</p><hr><h3><a name="luaL_checktype"><code>luaL_checktype</code></a></h3>
<pre>void luaL_checktype (lua_State *L, int narg, int t);</pre>

<p>
Checks whether the function argument <code>narg</code> has type <code>t</code>.





</p><hr><h3><a name="luaL_checkudata"><code>luaL_checkudata</code></a></h3>
<pre>void *luaL_checkudata (lua_State *L, int narg, const char *tname);</pre>

<p>
Checks whether the function argument <code>narg</code> is a userdata
of the type <code>tname</code> (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_newmetatable"><code>luaL_newmetatable</code></a>).





</p><hr><h3><a name="luaL_dofile"><code>luaL_dofile</code></a></h3>
<pre>int luaL_dofile (lua_State *L, const char *filename);</pre>

<p>
Loads and runs the given file.
It is defined as the following macro:

</p><pre>     (luaL_loadfile(L, filename) || lua_pcall(L, 0, LUA_MULTRET, 0))
</pre><p>
It returns 0 if there are no errors
or 1 in case of errors.





</p><hr><h3><a name="luaL_dostring"><code>luaL_dostring</code></a></h3>
<pre>int luaL_dostring (lua_State *L, const char *str);</pre>

<p>
Loads and runs the given string.
It is defined as the following macro:

</p><pre>     (luaL_loadstring(L, str) || lua_pcall(L, 0, LUA_MULTRET, 0))
</pre><p>
It returns 0 if there are no errors
or 1 in case of errors.





</p><hr><h3><a name="luaL_error"><code>luaL_error</code></a></h3>
<pre>int luaL_error (lua_State *L, const char *fmt, ...);</pre>

<p>
Raises an error.
The error message format is given by <code>fmt</code>
plus any extra arguments,
following the same rules of <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_pushfstring"><code>lua_pushfstring</code></a>.
It also adds at the beginning of the message the file name and
the line number where the error occurred,
if this information is available.


</p><p>
This function never returns,
but it is an idiom to use it in C&nbsp;functions
as <code>return luaL_error(<em>args</em>)</code>.





</p><hr><h3><a name="luaL_getmetafield"><code>luaL_getmetafield</code></a></h3>
<pre>int luaL_getmetafield (lua_State *L, int obj, const char *e);</pre>

<p>
Pushes onto the stack the field <code>e</code> from the metatable
of the object at index <code>obj</code>.
If the object does not have a metatable,
or if the metatable does not have this field,
returns 0 and pushes nothing.





</p><hr><h3><a name="luaL_getmetatable"><code>luaL_getmetatable</code></a></h3>
<pre>void luaL_getmetatable (lua_State *L, const char *tname);</pre>

<p>
Pushes onto the stack the metatable associated with name <code>tname</code>
in the registry (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_newmetatable"><code>luaL_newmetatable</code></a>).





</p><hr><h3><a name="luaL_gsub"><code>luaL_gsub</code></a></h3>
<pre>const char *luaL_gsub (lua_State *L,
                       const char *s,
                       const char *p,
                       const char *r);</pre>

<p>
Creates a copy of string <code>s</code> by replacing
any occurrence of the string <code>p</code>
with the string <code>r</code>.
Pushes the resulting string on the stack and returns it.





</p><hr><h3><a name="luaL_loadbuffer"><code>luaL_loadbuffer</code></a></h3>
<pre>int luaL_loadbuffer (lua_State *L,
                     const char *buff,
                     size_t sz,
                     const char *name);</pre>

<p>
Loads a buffer as a Lua chunk.
This function uses <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> to load the chunk in the
buffer pointed to by <code>buff</code> with size <code>sz</code>.


</p><p>
This function returns the same results as <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>.
<code>name</code> is the chunk name,
used for debug information and error messages.





</p><hr><h3><a name="luaL_loadfile"><code>luaL_loadfile</code></a></h3>
<pre>int luaL_loadfile (lua_State *L, const char *filename);</pre>

<p>
Loads a file as a Lua chunk.
This function uses <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> to load the chunk in the file
named <code>filename</code>.
If <code>filename</code> is <code>NULL</code>,
then it loads from the standard input.
The first line in the file is ignored if it starts with a <code>#</code>.


</p><p>
This function returns the same results as <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>,
but it has an extra error code <a name="pdf-LUA_ERRFILE"><code>LUA_ERRFILE</code></a>
if it cannot open/read the file.


</p><p>
As <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>, this function only loads the chunk;
it does not run it.





</p><hr><h3><a name="luaL_loadstring"><code>luaL_loadstring</code></a></h3>
<pre>int luaL_loadstring (lua_State *L, const char *s);</pre>

<p>
Loads a string as a Lua chunk.
This function uses <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a> to load the chunk in
the zero-terminated string <code>s</code>.


</p><p>
This function returns the same results as <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>.


</p><p>
Also as <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_load"><code>lua_load</code></a>, this function only loads the chunk;
it does not run it.





</p><hr><h3><a name="luaL_newmetatable"><code>luaL_newmetatable</code></a></h3>
<pre>int luaL_newmetatable (lua_State *L, const char *tname);</pre>

<p>
If the registry already has the key <code>tname</code>,
returns 0.
Otherwise,
creates a new table to be used as a metatable for userdata,
adds it to the registry with key <code>tname</code>,
and returns 1.


</p><p>
In both cases pushes onto the stack the final value associated
with <code>tname</code> in the registry.





</p><hr><h3><a name="luaL_newstate"><code>luaL_newstate</code></a></h3>
<pre>lua_State *luaL_newstate (void);</pre>

<p>
Creates a new Lua state.
It calls <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> with an
allocator based on the standard&nbsp;C <code>realloc</code> function
and then sets a panic function (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_atpanic"><code>lua_atpanic</code></a>) that prints
an error message to the standard error output in case of fatal
errors.


</p><p>
Returns the new state,
or <code>NULL</code> if there is a memory allocation error.





</p><hr><h3><a name="luaL_openlibs"><code>luaL_openlibs</code></a></h3>
<pre>void luaL_openlibs (lua_State *L);</pre>

<p>
Opens all standard Lua libraries into the given state.





</p><hr><h3><a name="luaL_optint"><code>luaL_optint</code></a></h3>
<pre>int luaL_optint (lua_State *L, int narg, int d);</pre>

<p>
If the function argument <code>narg</code> is a number,
returns this number cast to an <code>int</code>.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_optinteger"><code>luaL_optinteger</code></a></h3>
<pre>lua_Integer luaL_optinteger (lua_State *L,
                             int narg,
                             lua_Integer d);</pre>

<p>
If the function argument <code>narg</code> is a number,
returns this number cast to a <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_Integer"><code>lua_Integer</code></a>.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_optlong"><code>luaL_optlong</code></a></h3>
<pre>long luaL_optlong (lua_State *L, int narg, long d);</pre>

<p>
If the function argument <code>narg</code> is a number,
returns this number cast to a <code>long</code>.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_optlstring"><code>luaL_optlstring</code></a></h3>
<pre>const char *luaL_optlstring (lua_State *L,
                             int narg,
                             const char *d,
                             size_t *l);</pre>

<p>
If the function argument <code>narg</code> is a string,
returns this string.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.


</p><p>
If <code>l</code> is not <code>NULL</code>,
fills the position <code>*l</code> with the results's length.





</p><hr><h3><a name="luaL_optnumber"><code>luaL_optnumber</code></a></h3>
<pre>lua_Number luaL_optnumber (lua_State *L, int narg, lua_Number d);</pre>

<p>
If the function argument <code>narg</code> is a number,
returns this number.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_optstring"><code>luaL_optstring</code></a></h3>
<pre>const char *luaL_optstring (lua_State *L,
                            int narg,
                            const char *d);</pre>

<p>
If the function argument <code>narg</code> is a string,
returns this string.
If this argument is absent or is <b>nil</b>,
returns <code>d</code>.
Otherwise, raises an error.





</p><hr><h3><a name="luaL_prepbuffer"><code>luaL_prepbuffer</code></a></h3>
<pre>char *luaL_prepbuffer (luaL_Buffer *B);</pre>

<p>
Returns an address to a space of size <a name="pdf-LUAL_BUFFERSIZE"><code>LUAL_BUFFERSIZE</code></a>
where you can copy a string to be added to buffer <code>B</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Buffer"><code>luaL_Buffer</code></a>).
After copying the string into this space you must call
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_addsize"><code>luaL_addsize</code></a> with the size of the string to actually add 
it to the buffer.





</p><hr><h3><a name="luaL_pushresult"><code>luaL_pushresult</code></a></h3>
<pre>void luaL_pushresult (luaL_Buffer *B);</pre>

<p>
Finishes the use of buffer <code>B</code> leaving the final string on
the top of the stack.





</p><hr><h3><a name="luaL_ref"><code>luaL_ref</code></a></h3>
<pre>int luaL_ref (lua_State *L, int t);</pre>

<p>
Creates and returns a <em>reference</em>,
in the table at index <code>t</code>,
for the object at the top of the stack (and pops the object).


</p><p>
A reference is a unique integer key.
As long as you do not manually add integer keys into table <code>t</code>,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_ref"><code>luaL_ref</code></a> ensures the uniqueness of the key it returns.
You can retrieve an object referred by reference <code>r</code>
by calling <code>lua_rawgeti(L, t, r)</code>.
Function <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_unref"><code>luaL_unref</code></a> frees a reference and its associated object.


</p><p>
If the object at the top of the stack is <b>nil</b>,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_ref"><code>luaL_ref</code></a> returns the constant <a name="pdf-LUA_REFNIL"><code>LUA_REFNIL</code></a>.
The constant <a name="pdf-LUA_NOREF"><code>LUA_NOREF</code></a> is guaranteed to be different
from any reference returned by <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_ref"><code>luaL_ref</code></a>.





</p><hr><h3><a name="luaL_Reg"><code>luaL_Reg</code></a></h3>
<pre>typedef struct luaL_Reg {
  const char *name;
  lua_CFunction func;
} luaL_Reg;</pre>

<p>
Type for arrays of functions to be registered by
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_register"><code>luaL_register</code></a>.
<code>name</code> is the function name and <code>func</code> is a pointer to
the function.
Any array of <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Reg"><code>luaL_Reg</code></a> must end with an sentinel entry
in which both <code>name</code> and <code>func</code> are <code>NULL</code>.





</p><hr><h3><a name="luaL_register"><code>luaL_register</code></a></h3>
<pre>void luaL_register (lua_State *L,
                    const char *libname,
                    const luaL_Reg *l);</pre>

<p>
Opens a library.


</p><p>
When called with <code>libname</code> equal to <code>NULL</code>,
it simply registers all functions in the list <code>l</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_Reg"><code>luaL_Reg</code></a>) into the table on the top of the stack.


</p><p>
When called with a non-null <code>libname</code>,
<code>luaL_register</code> creates a new table <code>t</code>,
sets it as the value of the global variable <code>libname</code>,
sets it as the value of <code>package.loaded[libname]</code>,
and registers on it all functions in the list <code>l</code>.
If there is a table in <code>package.loaded[libname]</code> or in
variable <code>libname</code>,
reuses this table instead of creating a new one.


</p><p>
In any case the function leaves the table
on the top of the stack.





</p><hr><h3><a name="luaL_typename"><code>luaL_typename</code></a></h3>
<pre>const char *luaL_typename (lua_State *L, int idx);</pre>

<p>
Returns the name of the type of the value at index <code>idx</code>.





</p><hr><h3><a name="luaL_typerror"><code>luaL_typerror</code></a></h3>
<pre>int luaL_typerror (lua_State *L, int narg, const char *tname);</pre>

<p>
Generates an error with a message like the following:

</p><pre>     <em>location</em>: bad argument <em>narg</em> to '<em>func</em>' (<em>tname</em> expected, got <em>rt</em>)
</pre><p>
where <code><em>location</em></code> is produced by <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_where"><code>luaL_where</code></a>,
<code><em>func</em></code> is the name of the current function,
and <code><em>rt</em></code> is the type name of the actual argument.





</p><hr><h3><a name="luaL_unref"><code>luaL_unref</code></a></h3>
<pre>void luaL_unref (lua_State *L, int t, int ref);</pre>

<p>
Releases reference <code>ref</code> from the table at index <code>t</code>
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_ref"><code>luaL_ref</code></a>).
The entry is removed from the table,
so that the referred object can be collected.
The reference <code>ref</code> is also freed to be used again.


</p><p>
If <code>ref</code> is <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-LUA_NOREF"><code>LUA_NOREF</code></a> or <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-LUA_REFNIL"><code>LUA_REFNIL</code></a>,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_unref"><code>luaL_unref</code></a> does nothing.





</p><hr><h3><a name="luaL_where"><code>luaL_where</code></a></h3>
<pre>void luaL_where (lua_State *L, int lvl);</pre>

<p>
Pushes onto the stack a string identifying the current position
of the control at level <code>lvl</code> in the call stack.
Typically this string has the following format:

</p><pre>     <em>chunkname</em>:<em>currentline</em>:
</pre><p>
Level&nbsp;0 is the running function,
level&nbsp;1 is the function that called the running function,
etc.


</p><p>
This function is used to build a prefix for error messages.







</p><h1>5 - <a name="5">Standard Libraries</a></h1>

<p>
The standard Lua libraries provide useful functions
that are implemented directly through the C&nbsp;API.
Some of these functions provide essential services to the language
(e.g., <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-type"><code>type</code></a> and <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-getmetatable"><code>getmetatable</code></a>);
others provide access to "outside" services (e.g., I/O);
and others could be implemented in Lua itself,
but are quite useful or have critical performance requirements that
deserve an implementation in C (e.g., <code>sort</code>).


</p><p>
All libraries are implemented through the official C&nbsp;API
and are provided as separate C&nbsp;modules.
Currently, Lua has the following standard libraries:

</p><ul>

<li>basic library;</li>

<li>package library;</li>

<li>string manipulation;</li>

<li>table manipulation;</li>

<li>mathematical functions (sin, log, etc.);</li>

<li>input and output;</li>

<li>operating system facilities;</li>

<li>debug facilities.</li>

</ul><p>
Except for the basic and package libraries,
each library provides all its functions as fields of a global table
or as methods of its objects.


</p><p>
To have access to these libraries,
the C&nbsp;host program should call the <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_openlibs"><code>luaL_openlibs</code></a> function,
which opens all standard libraries.
Alternatively,
it can open them individually by calling
<a name="pdf-luaopen_base"><code>luaopen_base</code></a> (for the basic library),
<a name="pdf-luaopen_package"><code>luaopen_package</code></a> (for the package library),
<a name="pdf-luaopen_string"><code>luaopen_string</code></a> (for the string library),
<a name="pdf-luaopen_table"><code>luaopen_table</code></a> (for the table library),
<a name="pdf-luaopen_math"><code>luaopen_math</code></a> (for the mathematical library),
<a name="pdf-luaopen_io"><code>luaopen_io</code></a> (for the I/O and the Operating System libraries),
and <a name="pdf-luaopen_debug"><code>luaopen_debug</code></a> (for the debug library).
These functions are declared in <a name="pdf-lualib.h"><code>lualib.h</code></a>
and should not be called directly:
you must call them like any other Lua C&nbsp;function,
e.g., by using <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_call"><code>lua_call</code></a>.



</p><h2>5.1 - <a name="5.1">Basic Functions</a></h2>

<p>
The basic library provides some core functions to Lua.
If you do not include this library in your application,
you should check carefully whether you need to provide 
implementations for some of its facilities.


</p><p>
</p><hr><h3><a name="pdf-assert"><code>assert (v [, message])</code></a></h3>
Issues an  error when
the value of its argument <code>v</code> is false (i.e., <b>nil</b> or <b>false</b>);
otherwise, returns all its arguments.
<code>message</code> is an error message;
when absent, it defaults to "assertion failed!"




<p>
</p><hr><h3><a name="pdf-collectgarbage"><code>collectgarbage (opt [, arg])</code></a></h3>


<p>
This function is a generic interface to the garbage collector.
It performs different functions according to its first argument, <code>opt</code>:

</p><ul>

<li><b>"stop":</b>
stops the garbage collector.
</li>

<li><b>"restart":</b>
restarts the garbage collector.
</li>

<li><b>"collect":</b>
performs a full garbage-collection cycle.
</li>

<li><b>"count":</b>
returns the total memory in use by Lua (in Kbytes).
</li>

<li><b>"step":</b>
performs a garbage-collection step.
The step "size" is controlled by <code>arg</code>
(larger values mean more steps) in a non-specified way.
If you want to control the step size
you must experimentally tune the value of <code>arg</code>.
Returns <b>true</b> if the step finished a collection cycle.
</li>

<li><b>"setpause":</b>
sets <code>arg</code>/100 as the new value for the <em>pause</em> of
the collector (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.10">��2.10</a>).
</li>

<li><b>"setstepmul":</b>
sets <code>arg</code>/100 as the new value for the <em>step multiplier</em> of
the collector (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.10">��2.10</a>).
</li>

</ul>



<p>
</p><hr><h3><a name="pdf-dofile"><code>dofile (filename)</code></a></h3>
Opens the named file and executes its contents as a Lua chunk.
When called without arguments,
<code>dofile</code> executes the contents of the standard input (<code>stdin</code>).
Returns all values returned by the chunk.
In case of errors, <code>dofile</code> propagates the error
to its caller (that is, <code>dofile</code> does not run in protected mode).




<p>
</p><hr><h3><a name="pdf-error"><code>error (message [, level])</code></a></h3>
Terminates the last protected function called
and returns <code>message</code> as the error message.
Function <code>error</code> never returns.


<p>
Usually, <code>error</code> adds some information about the error position
at the beginning of the message.
The <code>level</code> argument specifies how to get the error position.
With level&nbsp;1 (the default), the error position is where the
<code>error</code> function was called.
Level&nbsp;2 points the error to where the function
that called <code>error</code> was called; and so on.
Passing a level&nbsp;0 avoids the addition of error position information
to the message.




</p><p>
</p><hr><h3><a name="pdf-_G"><code>_G</code></a></h3>
A global variable (not a function) that
holds the global environment (that is, <code>_G._G = _G</code>).
Lua itself does not use this variable;
changing its value does not affect any environment,
nor vice-versa.
(Use <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-setfenv"><code>setfenv</code></a> to change environments.)




<p>
</p><hr><h3><a name="pdf-getfenv"><code>getfenv (f)</code></a></h3>
Returns the current environment in use by the function.
<code>f</code> can be a Lua function or a number
that specifies the function at that stack level:
Level&nbsp;1 is the function calling <code>getfenv</code>.
If the given function is not a Lua function,
or if <code>f</code> is 0,
<code>getfenv</code> returns the global environment.
The default for <code>f</code> is 1.




<p>
</p><hr><h3><a name="pdf-getmetatable"><code>getmetatable (object)</code></a></h3>


<p>
If <code>object</code> does not have a metatable, returns <b>nil</b>.
Otherwise,
if the object's metatable has a <code>"__metatable"</code> field,
returns the associated value.
Otherwise, returns the metatable of the given object.




</p><p>
</p><hr><h3><a name="pdf-ipairs"><code>ipairs (t)</code></a></h3>


<p>
Returns three values: an iterator function, the table <code>t</code>, and 0,
so that the construction

</p><pre>     for i,v in ipairs(t) do <em>body</em> end
</pre><p>
will iterate over the pairs (<code>1,t[1]</code>), (<code>2,t[2]</code>), ������,
up to the first integer key absent from the table.




</p><p>
</p><hr><h3><a name="pdf-load"><code>load (func [, chunkname])</code></a></h3>


<p>
Loads a chunk using function <code>func</code> to get its pieces.
Each call to <code>func</code> must return a string that concatenates
with previous results.
A return of <b>nil</b> (or no value) signals the end of the chunk.


</p><p>
If there are no errors, 
returns the compiled chunk as a function;
otherwise, returns <b>nil</b> plus the error message.
The environment of the returned function is the global environment.


</p><p>
<code>chunkname</code> is used as the chunk name for error messages
and debug information.




</p><p>
</p><hr><h3><a name="pdf-loadfile"><code>loadfile ([filename])</code></a></h3>


<p>
Similar to <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-load"><code>load</code></a>,
but gets the chunk from file <code>filename</code>
or from the standard input,
if no file name is given.




</p><p>
</p><hr><h3><a name="pdf-loadstring"><code>loadstring (string [, chunkname])</code></a></h3>


<p>
Similar to <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-load"><code>load</code></a>,
but gets the chunk from the given string.


</p><p>
To load and run a given string, use the idiom

</p><pre>     assert(loadstring(s))()
</pre>



<p>
</p><hr><h3><a name="pdf-next"><code>next (table [, index])</code></a></h3>


<p>
Allows a program to traverse all fields of a table.
Its first argument is a table and its second argument
is an index in this table.
<code>next</code> returns the next index of the table
and its associated value.
When called with <b>nil</b> as its second argument,
<code>next</code> returns an initial index
and its associated value.
When called with the last index,
or with <b>nil</b> in an empty table,
<code>next</code> returns <b>nil</b>.
If the second argument is absent, then it is interpreted as <b>nil</b>.
In particular,
you can use <code>next(t)</code> to check whether a table is empty.


</p><p>
The order in which the indices are enumerated is not specified,
<em>even for numeric indices</em>.
(To traverse a table in numeric order,
use a numerical <b>for</b> or the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-ipairs"><code>ipairs</code></a> function.)


</p><p>
The behavior of <code>next</code> is <em>undefined</em> if,
during the traversal,
you assign any value to a non-existent field in the table.
You may however modify existing fields.
In particular, you may clear existing fields.




</p><p>
</p><hr><h3><a name="pdf-pairs"><code>pairs (t)</code></a></h3>


<p>
Returns three values: the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-next"><code>next</code></a> function, the table <code>t</code>, and <b>nil</b>,
so that the construction

</p><pre>     for k,v in pairs(t) do <em>body</em> end
</pre><p>
will iterate over all key�Cvalue pairs of table <code>t</code>.


</p><p>
See function <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-next"><code>next</code></a> for the caveats of modifying
the table during its traversal.




</p><p>
</p><hr><h3><a name="pdf-pcall"><code>pcall (f, arg1, ������)</code></a></h3>


<p>
Calls function <code>f</code> with
the given arguments in <em>protected mode</em>.
This means that any error inside&nbsp;<code>f</code> is not propagated;
instead, <code>pcall</code> catches the error
and returns a status code.
Its first result is the status code (a boolean),
which is true if the call succeeds without errors.
In such case, <code>pcall</code> also returns all results from the call,
after this first result.
In case of any error, <code>pcall</code> returns <b>false</b> plus the error message.




</p><p>
</p><hr><h3><a name="pdf-print"><code>print (������)</code></a></h3>
Receives any number of arguments,
and prints their values to <code>stdout</code>,
using the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-tostring"><code>tostring</code></a> function to convert them to strings.
<code>print</code> is not intended for formatted output,
but only as a quick way to show a value,
typically for debugging.
For formatted output, use <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.format"><code>string.format</code></a>.




<p>
</p><hr><h3><a name="pdf-rawequal"><code>rawequal (v1, v2)</code></a></h3>
Checks whether <code>v1</code> is equal to <code>v2</code>,
without invoking any metamethod.
Returns a boolean.




<p>
</p><hr><h3><a name="pdf-rawget"><code>rawget (table, index)</code></a></h3>
Gets the real value of <code>table[index]</code>,
without invoking any metamethod.
<code>table</code> must be a table;
<code>index</code> may be any value.




<p>
</p><hr><h3><a name="pdf-rawset"><code>rawset (table, index, value)</code></a></h3>
Sets the real value of <code>table[index]</code> to <code>value</code>,
without invoking any metamethod.
<code>table</code> must be a table,
<code>index</code> any value different from <b>nil</b>,
and <code>value</code> any Lua value.


<p>
This function returns <code>table</code>.




</p><p>
</p><hr><h3><a name="pdf-select"><code>select (index, ������)</code></a></h3>


<p>
If <code>index</code> is a number,
returns all arguments after argument number <code>index</code>.
Otherwise, <code>index</code> must be the string <code>"#"</code>,
and <code>select</code> returns the total number of extra arguments it received.




</p><p>
</p><hr><h3><a name="pdf-setfenv"><code>setfenv (f, table)</code></a></h3>


<p>
Sets the environment to be used by the given function.
<code>f</code> can be a Lua function or a number
that specifies the function at that stack level:
Level&nbsp;1 is the function calling <code>setfenv</code>.
<code>setfenv</code> returns the given function.


</p><p>
As a special case, when <code>f</code> is 0 <code>setfenv</code> changes
the environment of the running thread.
In this case, <code>setfenv</code> returns no values.




</p><p>
</p><hr><h3><a name="pdf-setmetatable"><code>setmetatable (table, metatable)</code></a></h3>


<p>
Sets the metatable for the given table.
(You cannot change the metatable of other types from Lua, only from&nbsp;C.)
If <code>metatable</code> is <b>nil</b>,
removes the metatable of the given table.
If the original metatable has a <code>"__metatable"</code> field,
raises an error.


</p><p>
This function returns <code>table</code>.




</p><p>
</p><hr><h3><a name="pdf-tonumber"><code>tonumber (e [, base])</code></a></h3>
Tries to convert its argument to a number.
If the argument is already a number or a string convertible
to a number, then <code>tonumber</code> returns this number;
otherwise, it returns <b>nil</b>.


<p>
An optional argument specifies the base to interpret the numeral.
The base may be any integer between 2 and 36, inclusive.
In bases above&nbsp;10, the letter '<code>A</code>' (in either upper or lower case)
represents&nbsp;10, '<code>B</code>' represents&nbsp;11, and so forth,
with '<code>Z</code>' representing 35.
In base 10 (the default), the number may have a decimal part,
as well as an optional exponent part (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.1">��2.1</a>).
In other bases, only unsigned integers are accepted.




</p><p>
</p><hr><h3><a name="pdf-tostring"><code>tostring (e)</code></a></h3>
Receives an argument of any type and
converts it to a string in a reasonable format.
For complete control of how numbers are converted,
use <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.format"><code>string.format</code></a>.


<p>
If the metatable of <code>e</code> has a <code>"__tostring"</code> field,
then <code>tostring</code> calls the corresponding value
with <code>e</code> as argument,
and uses the result of the call as its result.




</p><p>
</p><hr><h3><a name="pdf-type"><code>type (v)</code></a></h3>
Returns the type of its only argument, coded as a string.
The possible results of this function are
"<code>nil</code>" (a string, not the value <b>nil</b>),
"<code>number</code>",
"<code>string</code>",
"<code>boolean</code>",
"<code>table</code>",
"<code>function</code>",
"<code>thread</code>",
and "<code>userdata</code>".




<p>
</p><hr><h3><a name="pdf-unpack"><code>unpack (list [, i [, j]])</code></a></h3>
Returns the elements from the given table.
This function is equivalent to

<pre>     return list[i], list[i+1], ������, list[j]
</pre><p>
except that the above code can be written only for a fixed number
of elements.
By default, <code>i</code> is&nbsp;1 and <code>j</code> is the length of the list,
as defined by the length operator (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.5">��2.5.5</a>).




</p><p>
</p><hr><h3><a name="pdf-_VERSION"><code>_VERSION</code></a></h3>
A global variable (not a function) that
holds a string containing the current interpreter version.
The current contents of this variable is "<code>Lua 5.1</code>".




<p>
</p><hr><h3><a name="pdf-xpcall"><code>xpcall (f, err)</code></a></h3>


<p>
This function is similar to <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-pcall"><code>pcall</code></a>,
except that you can set a new error handler.


</p><p>
<code>xpcall</code> calls function <code>f</code> in protected mode,
using <code>err</code> as the error handler.
Any error inside <code>f</code> is not propagated;
instead, <code>xpcall</code> catches the error,
calls the <code>err</code> function with the original error object,
and returns a status code.
Its first result is the status code (a boolean),
which is true if the call succeeds without errors.
In this case, <code>xpcall</code> also returns all results from the call,
after this first result.
In case of any error,
<code>xpcall</code> returns <b>false</b> plus the result from <code>err</code>.







</p><h2>5.2 - <a name="5.2">Coroutine Manipulation</a></h2>

<p>
The operations related to coroutines comprise a sub-library of
the basic library and come inside the table <a name="pdf-coroutine"><code>coroutine</code></a>.
See <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.11">��2.11</a> for a general description of coroutines.


</p><p>
</p><hr><h3><a name="pdf-coroutine.create"><code>coroutine.create (f)</code></a></h3>


<p>
Creates a new coroutine, with body <code>f</code>.
<code>f</code> must be a Lua function.
Returns this new coroutine,
an object with type <code>"thread"</code>.




</p><p>
</p><hr><h3><a name="pdf-coroutine.resume"><code>coroutine.resume (co [, val1, ������])</code></a></h3>


<p>
Starts or continues the execution of coroutine <code>co</code>.
The first time you resume a coroutine,
it starts running its body.
The values <code>val1</code>, ������ are passed
as the arguments to the body function.
If the coroutine has yielded,
<code>resume</code> restarts it;
the values <code>val1</code>, ������ are passed
as the results from the yield.


</p><p>
If the coroutine runs without any errors,
<code>resume</code> returns <b>true</b> plus any values passed to <code>yield</code>
(if the coroutine yields) or any values returned by the body function
(if the coroutine terminates).
If there is any error,
<code>resume</code> returns <b>false</b> plus the error message.




</p><p>
</p><hr><h3><a name="pdf-coroutine.running"><code>coroutine.running ()</code></a></h3>


<p>
Returns the running coroutine,
or <b>nil</b> when called by the main thread.




</p><p>
</p><hr><h3><a name="pdf-coroutine.status"><code>coroutine.status (co)</code></a></h3>


<p>
Returns the status of coroutine <code>co</code>, as a string:
<code>"running"</code>,
if the coroutine is running (that is, it called <code>status</code>);
<code>"suspended"</code>, if the coroutine is suspended in a call to <code>yield</code>,
or if it has not started running yet;
<code>"normal"</code> if the coroutine is active but not running
(that is, it has resumed another coroutine);
and <code>"dead"</code> if the coroutine has finished its body function,
or if it has stopped with an error.




</p><p>
</p><hr><h3><a name="pdf-coroutine.wrap"><code>coroutine.wrap (f)</code></a></h3>


<p>
Creates a new coroutine, with body <code>f</code>.
<code>f</code> must be a Lua function.
Returns a function that resumes the coroutine each time it is called.
Any arguments passed to the function behave as the
extra arguments to <code>resume</code>.
Returns the same values returned by <code>resume</code>,
except the first boolean.
In case of error, propagates the error.




</p><p>
</p><hr><h3><a name="pdf-coroutine.yield"><code>coroutine.yield (������)</code></a></h3>


<p>
Suspends the execution of the calling coroutine.
The coroutine cannot be running a C&nbsp;function,
a metamethod, or an iterator.
Any arguments to <code>yield</code> are passed as extra results to <code>resume</code>.







</p><h2>5.3 - <a name="5.3">Modules</a></h2>

<p>
The package library provides basic
facilities for loading and building modules in Lua.
It exports two of its functions directly in the global environment:
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> and <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-module"><code>module</code></a>.
Everything else is exported in a table <a name="pdf-package"><code>package</code></a>.


</p><p>
</p><hr><h3><a name="pdf-module"><code>module (name [, ������])</code></a></h3>


<p>
Creates a module.
If there is a table in <code>package.loaded[name]</code>,
this table is the module.
Otherwise, if there is a global table <code>t</code> with the given name,
this table is the module.
Otherwise creates a new table <code>t</code> and
sets it as the value of the global <code>name</code> and
the value of <code>package.loaded[name]</code>.
This function also initializes <code>t._NAME</code> with the given name,
<code>t._M</code> with the module (<code>t</code> itself),
and <code>t._PACKAGE</code> with the package name
(the full module name minus last component; see below).
Finally, <code>module</code> sets <code>t</code> as the new environment
of the current function and the new value of <code>package.loaded[name]</code>,
so that <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> returns <code>t</code>.


</p><p>
If <code>name</code> is a compound name
(that is, one with components separated by dots),
<code>module</code> creates (or reuses, if they already exist)
tables for each component.
For instance, if <code>name</code> is <code>a.b.c</code>,
then <code>module</code> stores the module table in field <code>c</code> of
field <code>b</code> of global <code>a</code>.


</p><p>
This function may receive optional <em>options</em> after
the module name,
where each option is a function to be applied over the module.




</p><p>
</p><hr><h3><a name="pdf-require"><code>require (modname)</code></a></h3>


<p>
Loads the given module.
The function starts by looking into the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.loaded"><code>package.loaded</code></a> table
to determine whether <code>modname</code> is already loaded.
If it is, then <code>require</code> returns the value stored
at <code>package.loaded[modname]</code>.
Otherwise, it tries to find a <em>loader</em> for the module.


</p><p>
To find a loader,
first <code>require</code> queries <code>package.preload[modname]</code>.
If it has a value,
this value (which should be a function) is the loader.
Otherwise <code>require</code> searches for a Lua loader using the
path stored in <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.path"><code>package.path</code></a>.
If that also fails, it searches for a C&nbsp;loader using the
path stored in <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.cpath"><code>package.cpath</code></a>.
If that also fails,
it tries an <em>all-in-one</em> loader (see below).


</p><p>
When loading a C&nbsp;library,
<code>require</code> first uses a dynamic link facility to link the
application with the library.
Then it tries to find a C&nbsp;function inside this library to
be used as the loader.
The name of this C&nbsp;function is the string "<code>luaopen_</code>"
concatenated with a copy of the module name where each dot
is replaced by an underscore.
Moreover, if the module name has a hyphen,
its prefix up to (and including) the first hyphen is removed.
For instance, if the module name is <code>a.v1-b.c</code>,
the function name will be <code>luaopen_b_c</code>.


</p><p>
If <code>require</code> finds neither a Lua library nor a
C&nbsp;library for a module,
it calls the <em>all-in-one loader</em>.
This loader searches the C&nbsp;path for a library for
the root name of the given module.
For instance, when requiring <code>a.b.c</code>,
it will search for a C&nbsp;library for <code>a</code>.
If found, it looks into it for an open function for
the submodule;
in our example, that would be <code>luaopen_a_b_c</code>.
With this facility, a package can pack several C&nbsp;submodules
into one single library,
with each submodule keeping its original open function.


</p><p>
Once a loader is found,
<code>require</code> calls the loader with a single argument, <code>modname</code>.
If the loader returns any value,
<code>require</code> assigns the returned value to <code>package.loaded[modname]</code>.
If the loader returns no value and
has not assigned any value to <code>package.loaded[modname]</code>,
then <code>require</code> assigns <b>true</b> to this entry.
In any case, <code>require</code> returns the
final value of <code>package.loaded[modname]</code>.


</p><p>
If there is any error loading or running the module,
or if it cannot find any loader for the module,
then <code>require</code> signals an error. 




</p><p>
</p><hr><h3><a name="pdf-package.cpath"><code>package.cpath</code></a></h3>


<p>
The path used by <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> to search for a C&nbsp;loader.


</p><p>
Lua initializes the C&nbsp;path <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.cpath"><code>package.cpath</code></a> in the same way
it initializes the Lua path <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.path"><code>package.path</code></a>,
using the environment variable <a name="pdf-LUA_CPATH"><code>LUA_CPATH</code></a>
(plus another default path defined in <code>luaconf.h</code>).




</p><p>

</p><hr><h3><a name="pdf-package.loaded"><code>package.loaded</code></a></h3>


<p>
A table used by <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> to control which
modules are already loaded.
When you require a module <code>modname</code> and
<code>package.loaded[modname]</code> is not false,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> simply returns the value stored there.




</p><p>
</p><hr><h3><a name="pdf-package.loadlib"><code>package.loadlib (libname, funcname)</code></a></h3>


<p>
Dynamically links the host program with the C&nbsp;library <code>libname</code>.
Inside this library, looks for a function <code>funcname</code>
and returns this function as a C&nbsp;function.
(So, <code>funcname</code> must follow the protocol (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_CFunction"><code>lua_CFunction</code></a>)).


</p><p>
This is a low-level function.
It completely bypasses the package and module system.
Unlike <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a>,
it does not perform any path searching and
does not automatically adds extensions.
<code>libname</code> must be the complete file name of the C&nbsp;library,
including if necessary a path and extension.
<code>funcname</code> must be the exact name exported by the C&nbsp;library
(which may depend on the C&nbsp;compiler and linker used).


</p><p>
This function is not supported by ANSI C.
As such, it is only available on some platforms
(Windows, Linux, Mac OS X, Solaris, BSD,
plus other Unix systems that support the <code>dlfcn</code> standard).




</p><p>
</p><hr><h3><a name="pdf-package.path"><code>package.path</code></a></h3>


<p>
The path used by <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> to search for a Lua loader.


</p><p>
At start-up, Lua initializes this variable with
the value of the environment variable <a name="pdf-LUA_PATH"><code>LUA_PATH</code></a> or
with a default path defined in <code>luaconf.h</code>,
if the environment variable is not defined.
Any "<code>;;</code>" in the value of the environment variable
is replaced by the default path.


</p><p>
A path is a sequence of <em>templates</em> separated by semicolons.
For each template, <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> will change each interrogation
mark in the template by <code>filename</code>,
which is <code>modname</code> with each dot replaced by a
"directory separator" (such as "<code>/</code>" in Unix);
then it will try to load the resulting file name.
So, for instance, if the Lua path is

</p><pre>     "./?.lua;./?.lc;/usr/local/?/init.lua"
</pre><p>
the search for a Lua loader for module <code>foo</code>
will try to load the files
<code>./foo.lua</code>, <code>./foo.lc</code>, and
<code>/usr/local/foo/init.lua</code>, in that order.




</p><p>
</p><hr><h3><a name="pdf-package.preload"><code>package.preload</code></a></h3>


<p>
A table to store loaders for specific modules
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a>).




</p><p>
</p><hr><h3><a name="pdf-package.seeall"><code>package.seeall (module)</code></a></h3>


<p>
Sets a metatable for <code>module</code> with
its <code>__index</code> field referring to the global environment,
so that this module inherits values
from the global environment.
To be used as an option to function <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-module"><code>module</code></a>.







</p><h2>5.4 - <a name="5.4">String Manipulation</a></h2>

<p>
This library provides generic functions for string manipulation,
such as finding and extracting substrings, and pattern matching.
When indexing a string in Lua, the first character is at position&nbsp;1
(not at&nbsp;0, as in C).
Indices are allowed to be negative and are interpreted as indexing backwards,
from the end of the string.
Thus, the last character is at position -1, and so on.


</p><p>
The string library provides all its functions inside the table
<a name="pdf-string"><code>string</code></a>.
It also sets a metatable for strings
where the <code>__index</code> field points to the <code>string</code> table.
Therefore, you can use the string functions in object-oriented style.
For instance, <code>string.byte(s, i)</code>
can be written as <code>s:byte(i)</code>.


</p><p>
</p><hr><h3><a name="pdf-string.byte"><code>string.byte (s [, i [, j]])</code></a></h3>
Returns the internal numerical codes of the characters <code>s[i]</code>,
<code>s[i+1]</code>, ������, <code>s[j]</code>.
The default value for <code>i</code> is&nbsp;1;
the default value for <code>j</code> is&nbsp;<code>i</code>.


<p>
Note that numerical codes are not necessarily portable across platforms.




</p><p>
</p><hr><h3><a name="pdf-string.char"><code>string.char (������)</code></a></h3>
Receives zero or more integers.
Returns a string with length equal to the number of arguments,
in which each character has the internal numerical code equal
to its corresponding argument.


<p>
Note that numerical codes are not necessarily portable across platforms.




</p><p>
</p><hr><h3><a name="pdf-string.dump"><code>string.dump (function)</code></a></h3>


<p>
Returns a string containing a binary representation of the given function,
so that a later <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-loadstring"><code>loadstring</code></a> on this string returns
a copy of the function.
<code>function</code> must be a Lua function without upvalues.




</p><p>
</p><hr><h3><a name="pdf-string.find"><code>string.find (s, pattern [, init [, plain]])</code></a></h3>
Looks for the first match of
<code>pattern</code> in the string <code>s</code>.
If it finds a match, then <code>find</code> returns the indices of&nbsp;<code>s</code>
where this occurrence starts and ends;
otherwise, it returns <b>nil</b>.
A third, optional numerical argument <code>init</code> specifies
where to start the search;
its default value is&nbsp;1 and may be negative.
A value of <b>true</b> as a fourth, optional argument <code>plain</code>
turns off the pattern matching facilities,
so the function does a plain "find substring" operation,
with no characters in <code>pattern</code> being considered "magic".
Note that if <code>plain</code> is given, then <code>init</code> must be given as well.


<p>
If the pattern has captures,
then in a successful match
the captured values are also returned,
after the two indices.




</p><p>
</p><hr><h3><a name="pdf-string.format"><code>string.format (formatstring, ������)</code></a></h3>
Returns a formatted version of its variable number of arguments
following the description given in its first argument (which must be a string).
The format string follows the same rules as the <code>printf</code> family of
standard C&nbsp;functions.
The only differences are that the options/modifiers
<code>*</code>, <code>l</code>, <code>L</code>, <code>n</code>, <code>p</code>,
and <code>h</code> are not supported
and that there is an extra option, <code>q</code>.
The <code>q</code> option formats a string in a form suitable to be safely read
back by the Lua interpreter:
the string is written between double quotes,
and all double quotes, newlines, embedded zeros,
and backslashes in the string
are correctly escaped when written.
For instance, the call

<pre>     string.format('%q', 'a string with "quotes" and \n new line')
</pre><p>
will produce the string:

</p><pre>     "a string with \"quotes\" and \
      new line"
</pre>

<p>
The options <code>c</code>, <code>d</code>, <code>E</code>, <code>e</code>, <code>f</code>,
<code>g</code>, <code>G</code>, <code>i</code>, <code>o</code>, <code>u</code>, <code>X</code>, and <code>x</code> all
expect a number as argument,
whereas <code>q</code> and <code>s</code> expect a string.


</p><p>
This function does not accept string values
containing embedded zeros.




</p><p>
</p><hr><h3><a name="pdf-string.gmatch"><code>string.gmatch (s, pattern)</code></a></h3>
Returns an iterator function that,
each time it is called,
returns the next captures from <code>pattern</code> over string <code>s</code>.


<p>
If <code>pattern</code> specifies no captures,
then the whole match is produced in each call.


</p><p>
As an example, the following loop

</p><pre>     s = "hello world from Lua"
     for w in string.gmatch(s, "%a+") do
       print(w)
     end
</pre><p>
will iterate over all the words from string <code>s</code>,
printing one per line.
The next example collects all pairs <code>key=value</code> from the
given string into a table:

</p><pre>     t = {}
     s = "from=world, to=Lua"
     for k, v in string.gmatch(s, "(%w+)=(%w+)") do
       t[k] = v
     end
</pre>



<p>
</p><hr><h3><a name="pdf-string.gsub"><code>string.gsub (s, pattern, repl [, n])</code></a></h3>
Returns a copy of <code>s</code>
in which all occurrences of the <code>pattern</code> have been
replaced by a replacement string specified by <code>repl</code>,
which may be a string, a table, or a function.
<code>gsub</code> also returns, as its second value,
the total number of substitutions made.


<p>
If <code>repl</code> is a string, then its value is used for replacement.
The character&nbsp;<code>%</code> works as an escape character:
any sequence in <code>repl</code> of the form <code>%<em>n</em></code>,
with <em>n</em> between 1 and 9,
stands for the value of the <em>n</em>-th captured substring (see below).
The sequence <code>%0</code> stands for the whole match.
The sequence <code>%%</code> stands for a single&nbsp;<code>%</code>.


</p><p>
If <code>repl</code> is a table, then the table is queried for every match,
using the first capture as the key;
if the pattern specifies no captures,
then the whole match is used as the key.


</p><p>
If <code>repl</code> is a function, then this function is called every time a
match occurs, with all captured substrings passed as arguments,
in order;
if the pattern specifies no captures,
then the whole match is passed as a sole argument.


</p><p>
If the value returned by the table query or by the function call
is a string or a number,
then it is used as the replacement string;
otherwise, if it is <b>false</b> or <b>nil</b>,
then there is no replacement
(that is, the original match is kept in the string).


</p><p>
The optional last parameter <code>n</code> limits
the maximum number of substitutions to occur.
For instance, when <code>n</code> is 1 only the first occurrence of
<code>pattern</code> is replaced.


</p><p>
Here are some examples:

</p><pre>     x = string.gsub("hello world", "(%w+)", "%1 %1")
     --&gt; x="hello hello world world"
     
     x = string.gsub("hello world", "%w+", "%0 %0", 1)
     --&gt; x="hello hello world"
     
     x = string.gsub("hello world from Lua", "(%w+)%s*(%w+)", "%2 %1")
     --&gt; x="world hello Lua from"
     
     x = string.gsub("home = $HOME, user = $USER", "%$(%w+)", os.getenv)
     --&gt; x="home = /home/roberto, user = roberto"
     
     x = string.gsub("4+5 = $return 4+5$", "%$(.-)%$", function (s)
           return loadstring(s)()
         end)
     --&gt; x="4+5 = 9"
     
     local t = {name="lua", version="5.1"}
     x = string.gsub("$name%-$version.tar.gz", "%$(%w+)", t)
     --&gt; x="lua-5.1.tar.gz"
</pre>



<p>
</p><hr><h3><a name="pdf-string.len"><code>string.len (s)</code></a></h3>
Receives a string and returns its length.
The empty string <code>""</code> has length 0.
Embedded zeros are counted,
so <code>"a\000bc\000"</code> has length 5.




<p>
</p><hr><h3><a name="pdf-string.lower"><code>string.lower (s)</code></a></h3>
Receives a string and returns a copy of this string with all
uppercase letters changed to lowercase.
All other characters are left unchanged.
The definition of what an uppercase letter is depends on the current locale.




<p>
</p><hr><h3><a name="pdf-string.match"><code>string.match (s, pattern [, init])</code></a></h3>
Looks for the first <em>match</em> of
<code>pattern</code> in the string <code>s</code>.
If it finds one, then <code>match</code> returns
the captures from the pattern;
otherwise it returns <b>nil</b>.
If <code>pattern</code> specifies no captures,
then the whole match is returned.
A third, optional numerical argument <code>init</code> specifies
where to start the search;
its default value is&nbsp;1 and may be negative.




<p>
</p><hr><h3><a name="pdf-string.rep"><code>string.rep (s, n)</code></a></h3>
Returns a string that is the concatenation of <code>n</code> copies of
the string <code>s</code>.




<p>
</p><hr><h3><a name="pdf-string.reverse"><code>string.reverse (s)</code></a></h3>
Returns a string that is the string <code>s</code> reversed.




<p>
</p><hr><h3><a name="pdf-string.sub"><code>string.sub (s, i [, j])</code></a></h3>
Returns the substring of <code>s</code> that
starts at <code>i</code>  and continues until <code>j</code>;
<code>i</code> and <code>j</code> may be negative.
If <code>j</code> is absent, then it is assumed to be equal to -1
(which is the same as the string length).
In particular,
the call <code>string.sub(s,1,j)</code> returns a prefix of <code>s</code>
with length <code>j</code>,
and <code>string.sub(s, -i)</code> returns a suffix of <code>s</code>
with length <code>i</code>.




<p>
</p><hr><h3><a name="pdf-string.upper"><code>string.upper (s)</code></a></h3>
Receives a string and returns a copy of this string with all
lowercase letters changed to uppercase.
All other characters are left unchanged.
The definition of what a lowercase letter is depends on the current locale.



<h3>5.4.1 - <a name="5.4.1">Patterns</a></h3>


<h4>Character Class:</h4><p>
A <em>character class</em> is used to represent a set of characters.
The following combinations are allowed in describing a character class:

</p><ul>

<li><b><em>x</em>:</b>
(where <em>x</em> is not one of the <em>magic characters</em>
<code>^$()%.[]*+-?</code>)
represents the character <em>x</em> itself.
</li>

<li><b><code>.</code>:</b> (a dot) represents all characters.</li>

<li><b><code>%a</code>:</b> represents all letters.</li>

<li><b><code>%c</code>:</b> represents all control characters.</li>

<li><b><code>%d</code>:</b> represents all digits.</li>

<li><b><code>%l</code>:</b> represents all lowercase letters.</li>

<li><b><code>%p</code>:</b> represents all punctuation characters.</li>

<li><b><code>%s</code>:</b> represents all space characters.</li>

<li><b><code>%u</code>:</b> represents all uppercase letters.</li>

<li><b><code>%w</code>:</b> represents all alphanumeric characters.</li>

<li><b><code>%x</code>:</b> represents all hexadecimal digits.</li>

<li><b><code>%z</code>:</b> represents the character with representation 0.</li>

<li><b><code>%<em>x</em></code>:</b> (where <em>x</em> is any non-alphanumeric character)
represents the character <em>x</em>.
This is the standard way to escape the magic characters.
Any punctuation character (even the non magic)
can be preceded by a '<code>%</code>'
when used to represent itself in a pattern.
</li>

<li><b><code>[<em>set</em>]</code>:</b>
represents the class which is the union of all
characters in <em>set</em>.
A range of characters may be specified by
separating the end characters of the range with a '<code>-</code>'.
All classes <code>%</code><em>x</em> described above may also be used as
components in <em>set</em>.
All other characters in <em>set</em> represent themselves.
For example, <code>[%w_]</code> (or <code>[_%w]</code>)
represents all alphanumeric characters plus the underscore,
<code>[0-7]</code> represents the octal digits,
and <code>[0-7%l%-]</code> represents the octal digits plus
the lowercase letters plus the '<code>-</code>' character.


<p>
The interaction between ranges and classes is not defined.
Therefore, patterns like <code>[%a-z]</code> or <code>[a-%%]</code>
have no meaning.
</p></li>

<li><b><code>[^<em>set</em>]</code>:</b>
represents the complement of <em>set</em>,
where <em>set</em> is interpreted as above.
</li>

</ul><p>
For all classes represented by single letters (<code>%a</code>, <code>%c</code>, etc.),
the corresponding uppercase letter represents the complement of the class.
For instance, <code>%S</code> represents all non-space characters.


</p><p>
The definitions of letter, space, and other character groups
depend on the current locale.
In particular, the class <code>[a-z]</code> may not be equivalent to <code>%l</code>.





</p><h4>Pattern Item:</h4><p>
A <em>pattern item</em> may be

</p><ul>

<li>
a single character class,
which matches any single character in the class;
</li>

<li>
a single character class followed by '<code>*</code>',
which matches 0 or more repetitions of characters in the class.
These repetition items will always match the longest possible sequence;
</li>

<li>
a single character class followed by '<code>+</code>',
which matches 1 or more repetitions of characters in the class.
These repetition items will always match the longest possible sequence;
</li>

<li>
a single character class followed by '<code>-</code>',
which also matches 0 or more repetitions of characters in the class.
Unlike '<code>*</code>',
these repetition items will always match the <em>shortest</em> possible sequence;
</li>

<li>
a single character class followed by '<code>?</code>',
which matches 0 or 1 occurrence of a character in the class;
</li>

<li>
<code>%<em>n</em></code>, for <em>n</em> between 1 and 9;
such item matches a substring equal to the <em>n</em>-th captured string
(see below);
</li>

<li>
<code>%b<em>xy</em></code>, where <em>x</em> and <em>y</em> are two distinct characters;
such item matches strings that start with&nbsp;<em>x</em>, end with&nbsp;<em>y</em>,
and where the <em>x</em> and <em>y</em> are <em>balanced</em>.
This means that, if one reads the string from left to right,
counting <em>+1</em> for an <em>x</em> and <em>-1</em> for a <em>y</em>,
the ending <em>y</em> is the first <em>y</em> where the count reaches 0.
For instance, the item <code>%b()</code> matches expressions with
balanced parentheses.
</li>

</ul>




<h4>Pattern:</h4><p>
A <em>pattern</em> is a sequence of pattern items.
A '<code>^</code>' at the beginning of a pattern anchors the match at the
beginning of the subject string.
A '<code>$</code>' at the end of a pattern anchors the match at the
end of the subject string.
At other positions,
'<code>^</code>' and '<code>$</code>' have no special meaning and represent themselves.





</p><h4>Captures:</h4><p>
A pattern may contain sub-patterns enclosed in parentheses;
they describe <em>captures</em>.
When a match succeeds, the substrings of the subject string
that match captures are stored (<em>captured</em>) for future use.
Captures are numbered according to their left parentheses.
For instance, in the pattern <code>"(a*(.)%w(%s*))"</code>,
the part of the string matching <code>"a*(.)%w(%s*)"</code> is
stored as the first capture (and therefore has number&nbsp;1);
the character matching "<code>.</code>" is captured with number&nbsp;2,
and the part matching "<code>%s*</code>" has number&nbsp;3.


</p><p>
As a special case, the empty capture <code>()</code> captures
the current string position (a number).
For instance, if we apply the pattern <code>"()aa()"</code> on the
string <code>"flaaap"</code>, there will be two captures: 3&nbsp;and&nbsp;5.


</p><p>
A pattern cannot contain embedded zeros.  Use <code>%z</code> instead.











</p><h2>5.5 - <a name="5.5">Table Manipulation</a></h2><p>
This library provides generic functions for table manipulation.
It provides all its functions inside the table <a name="pdf-table"><code>table</code></a>.


</p><p>
Most functions in the table library assume that the table
represents an array or a list.
For these functions, when we talk about the "length" of a table
we mean the result of the length operator.


</p><p>
</p><hr><h3><a name="pdf-table.concat"><code>table.concat (table [, sep [, i [, j]]])</code></a></h3>
Given an array where all elements are strings or numbers,
returns <code>table[i]..sep..table[i+1] ������ sep..table[j]</code>.
The default value for <code>sep</code> is the empty string,
the default for <code>i</code> is 1,
and the default for <code>j</code> is the length of the table.
If <code>i</code> is greater than <code>j</code>, returns the empty string.




<p>
</p><hr><h3><a name="pdf-table.insert"><code>table.insert (table, [pos,] value)</code></a></h3>


<p>
Inserts element <code>value</code> at position <code>pos</code> in <code>table</code>,
shifting up other elements to open space, if necessary.
The default value for <code>pos</code> is <code>n+1</code>,
where <code>n</code> is the length of the table (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#2.5.5">��2.5.5</a>),
so that a call <code>table.insert(t,x)</code> inserts <code>x</code> at the end
of table <code>t</code>.




</p><p>
</p><hr><h3><a name="pdf-table.maxn"><code>table.maxn (table)</code></a></h3>


<p>
Returns the largest positive numerical index of the given table,
or zero if the table has no positive numerical indices.
(To do its job this function does a linear traversal of
the whole table.) 




</p><p>
</p><hr><h3><a name="pdf-table.remove"><code>table.remove (table [, pos])</code></a></h3>


<p>
Removes from <code>table</code> the element at position <code>pos</code>,
shifting down other elements to close the space, if necessary.
Returns the value of the removed element.
The default value for <code>pos</code> is <code>n</code>,
where <code>n</code> is the length of the table,
so that a call <code>table.remove(t)</code> removes the last element
of table <code>t</code>.




</p><p>
</p><hr><h3><a name="pdf-table.sort"><code>table.sort (table [, comp])</code></a></h3>
Sorts table elements in a given order, <em>in-place</em>,
from <code>table[1]</code> to <code>table[n]</code>,
where <code>n</code> is the length of the table.
If <code>comp</code> is given,
then it must be a function that receives two table elements,
and returns true
when the first is less than the second
(so that <code>not comp(a[i+1],a[i])</code> will be true after the sort).
If <code>comp</code> is not given,
then the standard Lua operator <code>&lt;</code> is used instead.


<p>
The sort algorithm is not stable;
that is, elements considered equal by the given order
may have their relative positions changed by the sort.







</p><h2>5.6 - <a name="5.6">Mathematical Functions</a></h2>

<p>
This library is an interface to the standard C&nbsp;math library.
It provides all its functions inside the table <a name="pdf-math"><code>math</code></a>.


</p><p>
</p><hr><h3><a name="pdf-math.abs"><code>math.abs (x)</code></a></h3>


<p>
Returns the absolute value of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.acos"><code>math.acos (x)</code></a></h3>


<p>
Returns the arc cosine of <code>x</code> (in radians).




</p><p>
</p><hr><h3><a name="pdf-math.asin"><code>math.asin (x)</code></a></h3>


<p>
Returns the arc sine of <code>x</code> (in radians).




</p><p>
</p><hr><h3><a name="pdf-math.atan"><code>math.atan (x)</code></a></h3>


<p>
Returns the arc tangent of <code>x</code> (in radians).




</p><p>
</p><hr><h3><a name="pdf-math.atan2"><code>math.atan2 (x, y)</code></a></h3>


<p>
Returns the arc tangent of <code>x/y</code> (in radians),
but uses the signs of both parameters to find the
quadrant of the result.
(It also handles correctly the case of <code>y</code> being zero.)




</p><p>
</p><hr><h3><a name="pdf-math.ceil"><code>math.ceil (x)</code></a></h3>


<p>
Returns the smallest integer larger than or equal to <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.cos"><code>math.cos (x)</code></a></h3>


<p>
Returns the cosine of <code>x</code> (assumed to be in radians).




</p><p>
</p><hr><h3><a name="pdf-math.cosh"><code>math.cosh (x)</code></a></h3>


<p>
Returns the hyperbolic cosine of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.deg"><code>math.deg (x)</code></a></h3>


<p>
Returns the angle <code>x</code> (given in radians) in degrees.




</p><p>
</p><hr><h3><a name="pdf-math.exp"><code>math.exp (x)</code></a></h3>


<p>
Returns the the value <em>e<sup>x</sup></em>.




</p><p>
</p><hr><h3><a name="pdf-math.floor"><code>math.floor (x)</code></a></h3>


<p>
Returns the largest integer smaller than or equal to <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.fmod"><code>math.fmod (x, y)</code></a></h3>


<p>
Returns the remainder of the division of <code>x</code> by <code>y</code>.




</p><p>
</p><hr><h3><a name="pdf-math.frexp"><code>math.frexp (x)</code></a></h3>


<p>
Returns <code>m</code> and <code>e</code> such that <em>x = m2<sup>e</sup></em>,
<code>e</code> is an integer and the absolute value of <code>m</code> is
in the range <em>[0.5, 1)</em>
(or zero when <code>x</code> is zero).




</p><p>
</p><hr><h3><a name="pdf-math.huge"><code>math.huge</code></a></h3>


<p>
The value <code>HUGE_VAL</code>,
a value larger than or equal to any other numerical value.




</p><p>
</p><hr><h3><a name="pdf-math.ldexp"><code>math.ldexp (m, e)</code></a></h3>


<p>
Returns <em>m2<sup>e</sup></em> (<code>e</code> should be an integer).




</p><p>
</p><hr><h3><a name="pdf-math.log"><code>math.log (x)</code></a></h3>


<p>
Returns the natural logarithm of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.log10"><code>math.log10 (x)</code></a></h3>


<p>
Returns the base-10 logarithm of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.max"><code>math.max (x, ������)</code></a></h3>


<p>
Returns the maximum value among its arguments.




</p><p>
</p><hr><h3><a name="pdf-math.min"><code>math.min (x, ������)</code></a></h3>


<p>
Returns the minimum value among its arguments.




</p><p>
</p><hr><h3><a name="pdf-math.modf"><code>math.modf (x)</code></a></h3>


<p>
Returns two numbers,
the integral part of <code>x</code> and the fractional part of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.pi"><code>math.pi</code></a></h3>


<p>
The value of <em>pi</em>.




</p><p>
</p><hr><h3><a name="pdf-math.pow"><code>math.pow (x, y)</code></a></h3>


<p>
Returns <em>x<sup>y</sup></em>.
(You can also use the expression <code>x^y</code> to compute this value.)




</p><p>
</p><hr><h3><a name="pdf-math.rad"><code>math.rad (x)</code></a></h3>


<p>
Returns the angle <code>x</code> (given in degrees) in radians.




</p><p>
</p><hr><h3><a name="pdf-math.random"><code>math.random ([m [, n]])</code></a></h3>


<p>
This function is an interface to the simple
pseudo-random generator function <code>rand</code> provided by ANSI&nbsp;C.
(No guarantees can be given for its statistical properties.)


</p><p>
When called without arguments,
returns a pseudo-random real number
in the range <em>[0,1)</em>.  
When called with a number <code>m</code>,
<code>math.random</code> returns
a pseudo-random integer in the range <em>[1, m]</em>.
When called with two numbers <code>m</code> and <code>n</code>,
<code>math.random</code> returns a pseudo-random
integer in the range <em>[m, n]</em>.




</p><p>
</p><hr><h3><a name="pdf-math.randomseed"><code>math.randomseed (x)</code></a></h3>


<p>
Sets <code>x</code> as the "seed"
for the pseudo-random generator:
equal seeds produce equal sequences of numbers.




</p><p>
</p><hr><h3><a name="pdf-math.sin"><code>math.sin (x)</code></a></h3>


<p>
Returns the sine of <code>x</code> (assumed to be in radians).




</p><p>
</p><hr><h3><a name="pdf-math.sinh"><code>math.sinh (x)</code></a></h3>


<p>
Returns the hyperbolic sine of <code>x</code>.




</p><p>
</p><hr><h3><a name="pdf-math.sqrt"><code>math.sqrt (x)</code></a></h3>


<p>
Returns the square root of <code>x</code>.
(You can also use the expression <code>x^0.5</code> to compute this value.)




</p><p>
</p><hr><h3><a name="pdf-math.tan"><code>math.tan (x)</code></a></h3>


<p>
Returns the tangent of <code>x</code> (assumed to be in radians).




</p><p>
</p><hr><h3><a name="pdf-math.tanh"><code>math.tanh (x)</code></a></h3>


<p>
Returns the hyperbolic tangent of <code>x</code>.







</p><h2>5.7 - <a name="5.7">Input and Output Facilities</a></h2>

<p>
The I/O library provides two different styles for file manipulation.
The first one uses implicit file descriptors;
that is, there are operations to set a default input file and a
default output file,
and all input/output operations are over these default files.
The second style uses explicit file descriptors.


</p><p>
When using implicit file descriptors,
all operations are supplied by table <a name="pdf-io"><code>io</code></a>.
When using explicit file descriptors,
the operation <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-io.open"><code>io.open</code></a> returns a file descriptor
and then all operations are supplied as methods of the file descriptor.


</p><p>
The table <code>io</code> also provides
three predefined file descriptors with their usual meanings from C:
<a name="pdf-io.stdin"><code>io.stdin</code></a>, <a name="pdf-io.stdout"><code>io.stdout</code></a>, and <a name="pdf-io.stderr"><code>io.stderr</code></a>.


</p><p>
Unless otherwise stated,
all I/O functions return <b>nil</b> on failure
(plus an error message as a second result)
and some value different from <b>nil</b> on success.


</p><p>
</p><hr><h3><a name="pdf-io.close"><code>io.close ([file])</code></a></h3>


<p>
Equivalent to <code>file:close()</code>.
Without a <code>file</code>, closes the default output file.




</p><p>
</p><hr><h3><a name="pdf-io.flush"><code>io.flush ()</code></a></h3>


<p>
Equivalent to <code>file:flush</code> over the default output file.




</p><p>
</p><hr><h3><a name="pdf-io.input"><code>io.input ([file])</code></a></h3>


<p>
When called with a file name, it opens the named file (in text mode),
and sets its handle as the default input file.
When called with a file handle,
it simply sets this file handle as the default input file.
When called without parameters,
it returns the current default input file.


</p><p>
In case of errors this function raises the error,
instead of returning an error code.




</p><p>
</p><hr><h3><a name="pdf-io.lines"><code>io.lines ([filename])</code></a></h3>


<p>
Opens the given file name in read mode
and returns an iterator function that,
each time it is called,
returns a new line from the file.
Therefore, the construction

</p><pre>     for line in io.lines(filename) do <em>body</em> end
</pre><p>
will iterate over all lines of the file.
When the iterator function detects the end of file,
it returns <b>nil</b> (to finish the loop) and automatically closes the file.


</p><p>
The call <code>io.lines()</code> (with no file name) is equivalent
to <code>io.input():lines()</code>;
that is, it iterates over the lines of the default input file.
In this case it does not close the file when the loop ends.




</p><p>
</p><hr><h3><a name="pdf-io.open"><code>io.open (filename [, mode])</code></a></h3>


<p>
This function opens a file,
in the mode specified in the string <code>mode</code>.
It returns a new file handle,
or, in case of errors, <b>nil</b> plus an error message.


</p><p>
The <code>mode</code> string can be any of the following:

</p><ul>
<li><b>"r":</b> read mode (the default);</li>
<li><b>"w":</b> write mode;</li>
<li><b>"a":</b> append mode;</li>
<li><b>"r+":</b> update mode, all previous data is preserved;</li>
<li><b>"w+":</b> update mode, all previous data is erased;</li>
<li><b>"a+":</b> append update mode, previous data is preserved,
  writing is only allowed at the end of file.</li>
</ul><p>
The <code>mode</code> string may also have a '<code>b</code>' at the end,
which is needed in some systems to open the file in binary mode.
This string is exactly what is used in the
standard&nbsp;C function <code>fopen</code>.




</p><p>
</p><hr><h3><a name="pdf-io.output"><code>io.output ([file])</code></a></h3>


<p>
Similar to <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-io.input"><code>io.input</code></a>, but operates over the default output file.




</p><p>
</p><hr><h3><a name="pdf-io.popen"><code>io.popen (prog [, mode])</code></a></h3>


<p>
Starts program <code>prog</code> in a separated process and returns
a file handle that you can use to read data from this program
(if <code>mode</code> is <code>"r"</code>, the default)
or to write data to this program
(if <code>mode</code> is <code>"w"</code>).


</p><p>
This function is system dependent and is not available
on all platforms.




</p><p>
</p><hr><h3><a name="pdf-io.read"><code>io.read (������)</code></a></h3>


<p>
Equivalent to <code>io.input():read</code>.




</p><p>
</p><hr><h3><a name="pdf-io.tmpfile"><code>io.tmpfile ()</code></a></h3>


<p>
Returns a handle for a temporary file.
This file is opened in update mode
and it is automatically removed when the program ends.




</p><p>
</p><hr><h3><a name="pdf-io.type"><code>io.type (obj)</code></a></h3>


<p>
Checks whether <code>obj</code> is a valid file handle.
Returns the string <code>"file"</code> if <code>obj</code> is an open file handle,
<code>"closed file"</code> if <code>obj</code> is a closed file handle,
or <b>nil</b> if <code>obj</code> is not a file handle.




</p><p>
</p><hr><h3><a name="pdf-io.write"><code>io.write (������)</code></a></h3>


<p>
Equivalent to <code>io.output():write</code>.




</p><p>
</p><hr><h3><a name="pdf-file:close"><code>file:close ()</code></a></h3>


<p>
Closes <code>file</code>.
Note that files are automatically closed when
their handles are garbage collected,
but that takes an unpredictable amount of time to happen.




</p><p>
</p><hr><h3><a name="pdf-file:flush"><code>file:flush ()</code></a></h3>


<p>
Saves any written data to <code>file</code>.




</p><p>
</p><hr><h3><a name="pdf-file:lines"><code>file:lines ()</code></a></h3>


<p>
Returns an iterator function that,
each time it is called,
returns a new line from the file.
Therefore, the construction

</p><pre>     for line in file:lines() do <em>body</em> end
</pre><p>
will iterate over all lines of the file.
(Unlike <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-io.lines"><code>io.lines</code></a>, this function does not close the file
when the loop ends.)




</p><p>
</p><hr><h3><a name="pdf-file:read"><code>file:read (������)</code></a></h3>


<p>
Reads the file <code>file</code>,
according to the given formats, which specify what to read.
For each format,
the function returns a string (or a number) with the characters read,
or <b>nil</b> if it cannot read data with the specified format.
When called without formats,
it uses a default format that reads the entire next line
(see below).


</p><p>
The available formats are

</p><ul>

<li><b>"*n":</b>
reads a number;
this is the only format that returns a number instead of a string.
</li>

<li><b>"*a":</b>
reads the whole file, starting at the current position.
On end of file, it returns the empty string.
</li>

<li><b>"*l":</b>
reads the next line (skipping the end of line),
returning <b>nil</b> on end of file.
This is the default format.
</li>

<li><b><em>number</em>:</b>
reads a string with up to this number of characters,
returning <b>nil</b> on end of file.
If number is zero,
it reads nothing and returns an empty string,
or <b>nil</b> on end of file.
</li>

</ul>



<p>
</p><hr><h3><a name="pdf-file:seek"><code>file:seek ([whence] [, offset])</code></a></h3>


<p>
Sets and gets the file position,
measured from the beginning of the file,
to the position given by <code>offset</code> plus a base
specified by the string <code>whence</code>, as follows:

</p><ul>
<li><b>"set":</b> base is position 0 (beginning of the file);</li>
<li><b>"cur":</b> base is current position;</li>
<li><b>"end":</b> base is end of file;</li>
</ul><p>
In case of success, function <code>seek</code> returns the final file position,
measured in bytes from the beginning of the file.
If this function fails, it returns <b>nil</b>,
plus a string describing the error.


</p><p>
The default value for <code>whence</code> is <code>"cur"</code>,
and for <code>offset</code> is 0.
Therefore, the call <code>file:seek()</code> returns the current
file position, without changing it;
the call <code>file:seek("set")</code> sets the position to the
beginning of the file (and returns 0);
and the call <code>file:seek("end")</code> sets the position to the
end of the file, and returns its size.




</p><p>
</p><hr><h3><a name="pdf-file:setvbuf"><code>file:setvbuf (mode [, size])</code></a></h3>


<p>
Sets the buffering mode for an output file.
There are three available modes:

</p><ul>

<li><b>"no":</b>
no buffering; the result of any output operation appears immediately.
</li>

<li><b>"full":</b>
full buffering; output operation is performed only
when the buffer is full (or when you explicitly <code>flush</code> the file
(see <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-io.flush"><code>io.flush</code></a>)).
</li>

<li><b>"line":</b>
line buffering; output is buffered until a newline is output
or there is any input from some special files
(such as a terminal device).
</li>

</ul><p>
For the last two cases, <code>sizes</code>
specifies the size of the buffer, in bytes.
The default is an appropriate size.




</p><p>
</p><hr><h3><a name="pdf-file:write"><code>file:write (������)</code></a></h3>


<p>
Writes the value of each of its arguments to
the <code>file</code>.
The arguments must be strings or numbers.
To write other values,
use <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-tostring"><code>tostring</code></a> or <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.format"><code>string.format</code></a> before <code>write</code>.







</p><h2>5.8 - <a name="5.8">Operating System Facilities</a></h2>

<p>
This library is implemented through table <a name="pdf-os"><code>os</code></a>.


</p><p>
</p><hr><h3><a name="pdf-os.clock"><code>os.clock ()</code></a></h3>


<p>
Returns an approximation of the amount in seconds of CPU time
used by the program.




</p><p>
</p><hr><h3><a name="pdf-os.date"><code>os.date ([format [, time]])</code></a></h3>


<p>
Returns a string or a table containing date and time,
formatted according to the given string <code>format</code>.


</p><p>
If the <code>time</code> argument is present,
this is the time to be formatted
(see the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-os.time"><code>os.time</code></a> function for a description of this value).
Otherwise, <code>date</code> formats the current time.


</p><p>
If <code>format</code> starts with '<code>!</code>',
then the date is formatted in Coordinated Universal Time.
After this optional character,
if <code>format</code> is the string "<code>*t</code>",
then <code>date</code> returns a table with the following fields:
<code>year</code> (four digits), <code>month</code> (1--12), <code>day</code> (1--31),
<code>hour</code> (0--23), <code>min</code> (0--59), <code>sec</code> (0--61),
<code>wday</code> (weekday, Sunday is&nbsp;1),
<code>yday</code> (day of the year),
and <code>isdst</code> (daylight saving flag, a boolean).


</p><p>
If <code>format</code> is not "<code>*t</code>",
then <code>date</code> returns the date as a string,
formatted according to the same rules as the C&nbsp;function <code>strftime</code>.


</p><p>
When called without arguments,
<code>date</code> returns a reasonable date and time representation that depends on
the host system and on the current locale
(that is, <code>os.date()</code> is equivalent to <code>os.date("%c")</code>).




</p><p>
</p><hr><h3><a name="pdf-os.difftime"><code>os.difftime (t2, t1)</code></a></h3>


<p>
Returns the number of seconds from time <code>t1</code> to time <code>t2</code>.
In POSIX, Windows, and some other systems,
this value is exactly <code>t2</code><em>-</em><code>t1</code>.




</p><p>
</p><hr><h3><a name="pdf-os.execute"><code>os.execute ([command])</code></a></h3>


<p>
This function is equivalent to the C&nbsp;function <code>system</code>.
It passes <code>command</code> to be executed by an operating system shell.
It returns a status code, which is system-dependent.
If <code>command</code> is absent, then it returns nonzero if a shell is available
and zero otherwise.




</p><p>
</p><hr><h3><a name="pdf-os.exit"><code>os.exit ([code])</code></a></h3>


<p>
Calls the C&nbsp;function <code>exit</code>,
with an optional <code>code</code>,
to terminate the host program.
The default value for <code>code</code> is the success code.




</p><p>
</p><hr><h3><a name="pdf-os.getenv"><code>os.getenv (varname)</code></a></h3>


<p>
Returns the value of the process environment variable <code>varname</code>,
or <b>nil</b> if the variable is not defined.




</p><p>
</p><hr><h3><a name="pdf-os.remove"><code>os.remove (filename)</code></a></h3>


<p>
Deletes the file or directory with the given name.
Directories must be empty to be removed.
If this function fails, it returns <b>nil</b>,
plus a string describing the error.




</p><p>
</p><hr><h3><a name="pdf-os.rename"><code>os.rename (oldname, newname)</code></a></h3>


<p>
Renames file or directory named <code>oldname</code> to <code>newname</code>.
If this function fails, it returns <b>nil</b>,
plus a string describing the error.




</p><p>
</p><hr><h3><a name="pdf-os.setlocale"><code>os.setlocale (locale [, category])</code></a></h3>


<p>
Sets the current locale of the program.
<code>locale</code> is a string specifying a locale;
<code>category</code> is an optional string describing which category to change:
<code>"all"</code>, <code>"collate"</code>, <code>"ctype"</code>,
<code>"monetary"</code>, <code>"numeric"</code>, or <code>"time"</code>;
the default category is <code>"all"</code>.
The function returns the name of the new locale,
or <b>nil</b> if the request cannot be honored.


</p><p>
When called with <b>nil</b> as the first argument,
this function only returns the name of the current locale
for the given category.




</p><p>
</p><hr><h3><a name="pdf-os.time"><code>os.time ([table])</code></a></h3>


<p>
Returns the current time when called without arguments,
or a time representing the date and time specified by the given table.
This table must have fields <code>year</code>, <code>month</code>, and <code>day</code>,
and may have fields <code>hour</code>, <code>min</code>, <code>sec</code>, and <code>isdst</code>
(for a description of these fields, see the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-os.date"><code>os.date</code></a> function).


</p><p>
The returned value is a number, whose meaning depends on your system.
In POSIX, Windows, and some other systems, this number counts the number
of seconds since some given start time (the "epoch").
In other systems, the meaning is not specified,
and the number returned by <code>time</code> can be used only as an argument to
<code>date</code> and <code>difftime</code>.




</p><p>
</p><hr><h3><a name="pdf-os.tmpname"><code>os.tmpname ()</code></a></h3>


<p>
Returns a string with a file name that can
be used for a temporary file.
The file must be explicitly opened before its use
and explicitly removed when no longer needed.







</p><h2>5.9 - <a name="5.9">The Debug Library</a></h2>

<p>
This library provides
the functionality of the debug interface to Lua programs.
You should exert care when using this library.
The functions provided here should be used exclusively for debugging
and similar tasks, such as profiling.
Please resist the temptation to use them as a
usual programming tool:
they can be very slow.
Moreover, several of its functions
violate some assumptions about Lua code
(e.g., that variables local to a function
cannot be accessed from outside or
that userdata metatables cannot be changed by Lua code)
and therefore can compromise otherwise secure code.


</p><p>
All functions in this library are provided
inside the <a name="pdf-debug"><code>debug</code></a> table.
All functions that operate over a thread
have an optional first argument which is the
thread to operate over.
The default is always the current thread.


</p><p>
</p><hr><h3><a name="pdf-debug.debug"><code>debug.debug ()</code></a></h3>


<p>
Enters an interactive mode with the user,
running each string that the user enters.
Using simple commands and other debug facilities,
the user can inspect global and local variables,
change their values, evaluate expressions, and so on.
A line containing only the word <code>cont</code> finishes this function,
so that the caller continues its execution.


</p><p>
Note that commands for <code>debug.debug</code> are not lexically nested
within any function, and so have no direct access to local variables.




</p><p>
</p><hr><h3><a name="pdf-debug.getfenv"><code>debug.getfenv (o)</code></a></h3>
Returns the environment of object <code>o</code>.




<p>
</p><hr><h3><a name="pdf-debug.gethook"><code>debug.gethook ([thread])</code></a></h3>


<p>
Returns the current hook settings of the thread, as three values:
the current hook function, the current hook mask,
and the current hook count
(as set by the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-debug.sethook"><code>debug.sethook</code></a> function).




</p><p>
</p><hr><h3><a name="pdf-debug.getinfo"><code>debug.getinfo ([thread,] function [, what])</code></a></h3>


<p>
Returns a table with information about a function.
You can give the function directly,
or you can give a number as the value of <code>function</code>,
which means the function running at level <code>function</code> of the call stack
of the given thread:
level&nbsp;0 is the current function (<code>getinfo</code> itself);
level&nbsp;1 is the function that called <code>getinfo</code>;
and so on.
If <code>function</code> is a number larger than the number of active functions,
then <code>getinfo</code> returns <b>nil</b>.


</p><p>
The returned table may contain all the fields returned by <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_getinfo"><code>lua_getinfo</code></a>,
with the string <code>what</code> describing which fields to fill in.
The default for <code>what</code> is to get all information available,
except the table of valid lines.
If present,
the option '<code>f</code>'
adds a field named <code>func</code> with the function itself.
If present,
the option '<code>L</code>'
adds a field named <code>activelines</code> with the table of
valid lines.


</p><p>
For instance, the expression <code>debug.getinfo(1,"n").name</code> returns
a name of the current function, if a reasonable name can be found,
and the expression <code>debug.getinfo(print)</code>
returns a table with all available information
about the <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-print"><code>print</code></a> function.




</p><p>
</p><hr><h3><a name="pdf-debug.getlocal"><code>debug.getlocal ([thread,] level, local)</code></a></h3>


<p>
This function returns the name and the value of the local variable
with index <code>local</code> of the function at level <code>level</code> of the stack.
(The first parameter or local variable has index&nbsp;1, and so on,
until the last active local variable.)
The function returns <b>nil</b> if there is no local
variable with the given index,
and raises an error when called with a <code>level</code> out of range.
(You can call <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-debug.getinfo"><code>debug.getinfo</code></a> to check whether the level is valid.)


</p><p>
Variable names starting with '<code>(</code>' (open parentheses)
represent internal variables
(loop control variables, temporaries, and C&nbsp;function locals).




</p><p>
</p><hr><h3><a name="pdf-debug.getmetatable"><code>debug.getmetatable (object)</code></a></h3>


<p>
Returns the metatable of the given <code>object</code>
or <b>nil</b> if it does not have a metatable.




</p><p>
</p><hr><h3><a name="pdf-debug.getregistry"><code>debug.getregistry ()</code></a></h3>


<p>
Returns the registry table (see <a href="http://www.codingnow.com/2000/download/lua_manual.html#3.5">��3.5</a>).




</p><p>
</p><hr><h3><a name="pdf-debug.getupvalue"><code>debug.getupvalue (func, up)</code></a></h3>


<p>
This function returns the name and the value of the upvalue
with index <code>up</code> of the function <code>func</code>.
The function returns <b>nil</b> if there is no upvalue with the given index.




</p><p>
</p><hr><h3><a name="pdf-debug.setfenv"><code>debug.setfenv (object, table)</code></a></h3>


<p>
Sets the environment of the given <code>object</code> to the given <code>table</code>.
Returns <code>object</code>.




</p><p>
</p><hr><h3><a name="pdf-debug.sethook"><code>debug.sethook ([thread,] hook, mask [, count])</code></a></h3>


<p>
Sets the given function as a hook.
The string <code>mask</code> and the number <code>count</code> describe
when the hook will be called.
The string mask may have the following characters,
with the given meaning:

</p><ul>
<li><b><code>"c"</code>:</b> The hook is called every time Lua calls a function;</li>
<li><b><code>"r"</code>:</b> The hook is called every time Lua returns from a function;</li>
<li><b><code>"l"</code>:</b> The hook is called every time Lua enters a new line of code.</li>
</ul><p>
With a <code>count</code> different from zero,
the hook is called after every <code>count</code> instructions.


</p><p>
When called without arguments,
<a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-debug.sethook"><code>debug.sethook</code></a> turns off the hook.


</p><p>
When the hook is called, its first parameter is a string
describing the event that has triggered its call:
<code>"call"</code>, <code>"return"</code> (or <code>"tail return"</code>),
<code>"line"</code>, and <code>"count"</code>.
For line events,
the hook also gets the new line number as its second parameter.
Inside a hook,
you can call <code>getinfo</code> with level&nbsp;2 to get more information about
the running function
(level&nbsp;0 is the <code>getinfo</code> function,
and level&nbsp;1 is the hook function),
unless the event is <code>"tail return"</code>.
In this case, Lua is only simulating the return,
and a call to <code>getinfo</code> will return invalid data.




</p><p>
</p><hr><h3><a name="pdf-debug.setlocal"><code>debug.setlocal ([thread,] level, local, value)</code></a></h3>


<p>
This function assigns the value <code>value</code> to the local variable
with index <code>local</code> of the function at level <code>level</code> of the stack.
The function returns <b>nil</b> if there is no local
variable with the given index,
and raises an error when called with a <code>level</code> out of range.
(You can call <code>getinfo</code> to check whether the level is valid.)
Otherwise, it returns the name of the local variable.




</p><p>
</p><hr><h3><a name="pdf-debug.setmetatable"><code>debug.setmetatable (object, table)</code></a></h3>


<p>
Sets the metatable for the given <code>object</code> to the given <code>table</code>
(which can be <b>nil</b>).




</p><p>
</p><hr><h3><a name="pdf-debug.setupvalue"><code>debug.setupvalue (func, up, value)</code></a></h3>


<p>
This function assigns the value <code>value</code> to the upvalue
with index <code>up</code> of the function <code>func</code>.
The function returns <b>nil</b> if there is no upvalue
with the given index.
Otherwise, it returns the name of the upvalue.




</p><p>
</p><hr><h3><a name="pdf-debug.traceback"><code>debug.traceback ([thread,] [message] [, level])</code></a></h3>


<p>
Returns a string with a traceback of the call stack.
An optional <code>message</code> string is appended
at the beginning of the traceback.
An optional <code>level</code> number tells at which level
to start the traceback
(default is 1, the function calling <code>traceback</code>).







</p><h1>6 - <a name="6">Lua Stand-alone</a></h1>

<p>
Although Lua has been designed as an extension language,
to be embedded in a host C&nbsp;program,
it is also frequently used as a stand-alone language.
An interpreter for Lua as a stand-alone language,
called simply <code>lua</code>,
is provided with the standard distribution.
The stand-alone interpreter includes
all standard libraries, including the debug library.
Its usage is:

</p><pre>     lua [options] [script [args]]
</pre><p>
The options are:

</p><ul>
<li><b><code>-e <em>stat</em></code>:</b> executes string <em>stat</em>;</li>
<li><b><code>-l <em>mod</em></code>:</b> "requires" <em>mod</em>;</li>
<li><b><code>-i</code>:</b> enters interactive mode after running <em>script</em>;</li>
<li><b><code>-v</code>:</b> prints version information;</li>
<li><b><code>--</code>:</b> stops handling options;</li>
<li><b><code>-</code>:</b> executes <code>stdin</code> as a file and stops handling options.</li>
</ul><p>
After handling its options, <code>lua</code> runs the given <em>script</em>,
passing to it the given <em>args</em> as string arguments.
When called without arguments,
<code>lua</code> behaves as <code>lua -v -i</code>
when the standard input (<code>stdin</code>) is a terminal,
and as <code>lua -</code> otherwise.


</p><p>
Before running any argument,
the interpreter checks for an environment variable <a name="pdf-LUA_INIT"><code>LUA_INIT</code></a>.
If its format is <code>@<em>filename</em></code>,
then <code>lua</code> executes the file.
Otherwise, <code>lua</code> executes the string itself.


</p><p>
All options are handled in order, except <code>-i</code>.
For instance, an invocation like

</p><pre>     $ lua -e'a=1' -e 'print(a)' script.lua
</pre><p>
will first set <code>a</code> to 1, then print the value of <code>a</code> (which is '<code>1</code>'),
and finally run the file <code>script.lua</code> with no arguments.
(Here <code>$</code> is the shell prompt. Your prompt may be different.)


</p><p>
Before starting to run the script,
<code>lua</code> collects all arguments in the command line
in a global table called <code>arg</code>.
The script name is stored at index 0,
the first argument after the script name goes to index 1,
and so on.
Any arguments before the script name
(that is, the interpreter name plus the options)
go to negative indices.
For instance, in the call

</p><pre>     $ lua -la b.lua t1 t2
</pre><p>
the interpreter first runs the file <code>a.lua</code>,
then creates a table

</p><pre>     arg = { [-2] = "lua", [-1] = "-la",
             [0] = "b.lua",
             [1] = "t1", [2] = "t2" }
</pre><p>
and finally runs the file <code>b.lua</code>.
The script is called with <code>arg[1]</code>, <code>arg[2]</code>, ������
as arguments;
it can also access these arguments with the vararg expression '<code>...</code>'.


</p><p>
In interactive mode,
if you write an incomplete statement,
the interpreter waits for its completion
by issuing a different prompt.


</p><p>
If the global variable <a name="pdf-_PROMPT"><code>_PROMPT</code></a> contains a string,
then its value is used as the prompt.
Similarly, if the global variable <a name="pdf-_PROMPT2"><code>_PROMPT2</code></a> contains a string,
its value is used as the secondary prompt
(issued during incomplete statements).
Therefore, both prompts can be changed directly on the command line.
For instance,

</p><pre>     $ lua -e"_PROMPT='myprompt&gt; '" -i
</pre><p>
(the outer pair of quotes is for the shell,
the inner pair is for Lua),
or in any Lua programs by assigning to <code>_PROMPT</code>.
Note the use of <code>-i</code> to enter interactive mode; otherwise,
the program would just end silently right after the assignment to <code>_PROMPT</code>.


</p><p>
To allow the use of Lua as a
script interpreter in Unix systems,
the stand-alone interpreter skips
the first line of a chunk if it starts with <code>#</code>.
Therefore, Lua scripts can be made into executable programs
by using <code>chmod +x</code> and the&nbsp;<code>#!</code> form,
as in

</p><pre>     #!/usr/local/bin/lua
</pre><p>
(Of course,
the location of the Lua interpreter may be different in your machine.
If <code>lua</code> is in your <code>PATH</code>,
then 

</p><pre>     #!/usr/bin/env lua
</pre><p>
is a more portable solution.) 



</p><h1>7 - <a name="7">Incompatibilities with the Previous Version</a></h1>

<p>
Here we list the incompatibilities that you may found when moving a program
from Lua&nbsp;5.0 to Lua&nbsp;5.1.
You can avoid most of the incompatibilities compiling Lua with
appropriate options (see file <code>luaconf.h</code>).
However,
all these compatibility options will be removed in the next version of Lua.



</p><h2>7.1 - <a name="7.1">Changes in the Language</a></h2>
<ul>

<li>
The vararg system changed from the pseudo-argument <code>arg</code> with a
table with the extra arguments to the vararg expression.
(See compile-time option <code>LUA_COMPAT_VARARG</code> in <code>luaconf.h</code>.)
</li>

<li>
There was a subtle change in the scope of the implicit
variables of the <b>for</b> statement and for the <b>repeat</b> statement.
</li>

<li>
The long string/long comment syntax (<code>[[<em>string</em>]]</code>)
does not allow nesting.
You can use the new syntax (<code>[=[<em>string</em>]=]</code>) in these cases.
(See compile-time option <code>LUA_COMPAT_LSTR</code> in <code>luaconf.h</code>.)
</li>

</ul>




<h2>7.2 - <a name="7.2">Changes in the Libraries</a></h2>
<ul>

<li>
Function <code>string.gfind</code> was renamed <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.gmatch"><code>string.gmatch</code></a>.
(See compile-time option <code>LUA_COMPAT_GFIND</code> in <code>luaconf.h</code>.)
</li>

<li>
When <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-string.gsub"><code>string.gsub</code></a> is called with a function as its
third argument,
whenever this function returns <b>nil</b> or <b>false</b> the
replacement string is the whole match,
instead of the empty string.
</li>

<li>
Function <code>table.setn</code> was deprecated.
Function <code>table.getn</code> corresponds
to the new length operator (<code>#</code>);
use the operator instead of the function.
(See compile-time option <code>LUA_COMPAT_GETN</code> in <code>luaconf.h</code>.)
</li>

<li>
Function <code>loadlib</code> was renamed <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.loadlib"><code>package.loadlib</code></a>.
(See compile-time option <code>LUA_COMPAT_LOADLIB</code> in <code>luaconf.h</code>.)
</li>

<li>
Function <code>math.mod</code> was renamed <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-math.fmod"><code>math.fmod</code></a>.
(See compile-time option <code>LUA_COMPAT_MOD</code> in <code>luaconf.h</code>.)
</li>

<li>
Functions <code>table.foreach</code> and <code>table.foreachi</code> are deprecated.
You can use a for loop with <code>pairs</code> or <code>ipairs</code> instead.
</li>

<li>
There were substantial changes in function <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-require"><code>require</code></a> due to
the new module system.
However, the new behavior is mostly compatible with the old,
but <code>require</code> gets the path from <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-package.path"><code>package.path</code></a> instead
of from <code>LUA_PATH</code>.
</li>

<li>
Function <a href="http://www.codingnow.com/2000/download/lua_manual.html#pdf-collectgarbage"><code>collectgarbage</code></a> has different arguments.
Function <code>gcinfo</code> is deprecated;
use <code>collectgarbage("count")</code> instead.
</li>

</ul>




<h2>7.3 - <a name="7.3">Changes in the API</a></h2>
<ul>

<li>
The <code>luaopen_*</code> functions (to open libraries)
cannot be called directly,
like a regular C function.
They must be called through Lua,
like a Lua function.
</li>

<li>
Function <code>lua_open</code> was replaced by <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_newstate"><code>lua_newstate</code></a> to
allow the user to set a memory-allocation function.
You can use <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_newstate"><code>luaL_newstate</code></a> from the standard library to
create a state with a standard allocation function
(based on <code>realloc</code>).
</li>

<li>
Functions <code>luaL_getn</code> and <code>luaL_setn</code>
(from the auxiliary library) are deprecated.
Use <a href="http://www.codingnow.com/2000/download/lua_manual.html#lua_objlen"><code>lua_objlen</code></a> instead of <code>luaL_getn</code>
and nothing instead of <code>luaL_setn</code>.
</li>

<li>
Function <code>luaL_openlib</code> was replaced by <a href="http://www.codingnow.com/2000/download/lua_manual.html#luaL_register"><code>luaL_register</code></a>.
</li>

<li>
Function <code>luaL_checkudata</code> now throws an error when the given value
is not a userdata of the expected type.
(In Lua&nbsp;5.0 it returned <code>NULL</code>.)
</li>

</ul>




<h1>8 - <a name="8">The Complete Syntax of Lua</a></h1>

<p>
Here is the complete syntax of Lua in extended BNF.
(It does not describe operator precedences.)




</p><pre>
	chunk ::= {stat [`<b>;</b>��]} [laststat [`<b>;</b>��]]

	block ::= chunk

	stat ::=  varlist1 `<b>=</b>�� explist1 | 
		 functioncall | 
		 <b>do</b> block <b>end</b> | 
		 <b>while</b> exp <b>do</b> block <b>end</b> | 
		 <b>repeat</b> block <b>until</b> exp | 
		 <b>if</b> exp <b>then</b> block {<b>elseif</b> exp <b>then</b> block} [<b>else</b> block] <b>end</b> | 
		 <b>for</b> Name `<b>=</b>�� exp `<b>,</b>�� exp [`<b>,</b>�� exp] <b>do</b> block <b>end</b> | 
		 <b>for</b> namelist <b>in</b> explist1 <b>do</b> block <b>end</b> | 
		 <b>function</b> funcname funcbody | 
		 <b>local</b> <b>function</b> Name funcbody | 
		 <b>local</b> namelist [`<b>=</b>�� explist1] 

	laststat ::= <b>return</b> [explist1] | <b>break</b>

	funcname ::= Name {`<b>.</b>�� Name} [`<b>:</b>�� Name]

	varlist1 ::= var {`<b>,</b>�� var}

	var ::=  Name | prefixexp `<b>[</b>�� exp `<b>]</b>�� | prefixexp `<b>.</b>�� Name 

	namelist ::= Name {`<b>,</b>�� Name}

	explist1 ::= {exp `<b>,</b>��} exp

	exp ::=  <b>nil</b> | <b>false</b> | <b>true</b> | Number | String | `<b>...</b>�� | function | 
		 prefixexp | tableconstructor | exp binop exp | unop exp 

	prefixexp ::= var | functioncall | `<b>(</b>�� exp `<b>)</b>��

	functioncall ::=  prefixexp args | prefixexp `<b>:</b>�� Name args 

	args ::=  `<b>(</b>�� [explist1] `<b>)</b>�� | tableconstructor | String 

	function ::= <b>function</b> funcbody

	funcbody ::= `<b>(</b>�� [parlist1] `<b>)</b>�� block <b>end</b>

	parlist1 ::= namelist [`<b>,</b>�� `<b>...</b>��] | `<b>...</b>��

	tableconstructor ::= `<b>{</b>�� [fieldlist] `<b>}</b>��

	fieldlist ::= field {fieldsep field} [fieldsep]

	field ::= `<b>[</b>�� exp `<b>]</b>�� `<b>=</b>�� exp | Name `<b>=</b>�� exp | exp

	fieldsep ::= `<b>,</b>�� | `<b>;</b>��

	binop ::= `<b>+</b>�� | `<b>-</b>�� | `<b>*</b>�� | `<b>/</b>�� | `<b>^</b>�� | `<b>%</b>�� | `<b>..</b>�� | 
		 `<b>&lt;</b>�� | `<b>&lt;=</b>�� | `<b>&gt;</b>�� | `<b>&gt;=</b>�� | `<b>==</b>�� | `<b>~=</b>�� | 
		 <b>and</b> | <b>or</b>

	unop ::= `<b>-</b>�� | <b>not</b> | `<b>#</b>��

</pre>

<p>






</p><hr>
<small>
Last update:
Tue Oct  3 21:27:28 BRT 2006
<br>
���������£��޸ļ�������
2009��4��7��
</small>
<!--
Last change: minor edit
-->



<div id="feedly-mini" title="feedly Mini tookit"></div>

<!--
</body>
<div></div>
</html>
-->