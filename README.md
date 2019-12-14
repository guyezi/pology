<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html><head>
<meta name="generator" content="HTML Tidy for Linux (vers 25 March 2009), see www.w3.org">
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>第2章&nbsp;.&nbsp;PO 格式</title>
<link rel="stylesheet" type="text/css" href="http://pology.nedohodnik.net/doc/user/en_US/style.css">
<meta name="generator" content="DocBook XSL Stylesheets V1.78.1">
<link rel="home" href="http://pology.nedohodnik.net/doc/user/en_US/index.html" title="Pology User Manual">
<link rel="up" href="http://pology.nedohodnik.net/doc/user/en_US/index.html" title="Pology User Manual">
<link rel="prev" href="http://pology.nedohodnik.net/doc/user/en_US/ch-about.html" title="Chapter&nbsp;1.&nbsp;A Study of PO">
<link rel="next" href="http://pology.nedohodnik.net/doc/user/en_US/ch-sieve.html" title="Chapter&nbsp;3.&nbsp;Sieving">
</head>
<body vlink="#840084" text="black" link="#0000FF" bgcolor="white" alink="#0000FF">
<div class="navheader">
<table summary="Navigation header" width="100%">
<tbody><tr>
<th colspan="3" align="center">第2章&nbsp;.&nbsp;PO 格式</th>
</tr>
<tr>
<td width="20%" align="left"><a accesskey="p" href="http://pology.nedohodnik.net/doc/user/en_US/ch-about.html">上一页</a></td>
<th width="60%" align="center">&nbsp;</th>
<td width="20%" align="right"><a accesskey="n" href="http://pology.nedohodnik.net/doc/user/en_US/ch-sieve.html">下一页</a></td>
</tr>
</tbody></table>
<hr></div>
<div class="chapter">
<div class="titlepage">
<div>
<div>
<h1 class="title"><a name="ch-poformat" id="ch-poformat"></a>第2章&nbsp;.&nbsp;PO 格式</h1>
</div>
</div>
</div>
<p>There is no formal specification of the PO format; instead, the related parts of <a class="ulink" href="http://www.gnu.org/software/gettext/manual/html_node/index.html" target="_top">the Gettext manual</a>
 serve as its working definition. Although the PO format has been 
documented both by the Gettext manual and elsewhere, in smaller and 
greater detail, it will be presented here as well. This is in order to 
thoroughly explain how the format elements influence the translation 
practice, and to make sure that the terms used in the rest of this 
manual are understood in their precise meaning.</p>
<p>PO格式没有正式的规范；相反，Gettext手册的相关部分作为其工作定义。尽管这个PO格式已经被<a class="ulink" href="http://www.gnu.org/software/gettext/manual/html_node/index.html" target="_top">Gettext手册</a>和其他地方记录下来了，但是在这里也会有详细的介绍。这是为了彻底解释格式元素如何影响翻译实践，并确保本手册其余部分中使用的术语在其准确含义中得到理解。</p>
 <br />
<p>Before going into the format description, it is useful to give an 
overview of usage contexts for the PO format and of the basic principles
 behind it.</p>
 <p>在进入格式描述之前，概述PO格式的使用上下文及其背后的基本原则是很有用的.</p>
 <br />

<p><a name="p-dynstattr" id="p-dynstattr"></a>There are three distinct contexts in which PO files are used:</p>
<p><a name="p-dynstattr" id="p-dynstattr"></a>有三个不同的上下文中使用PO文件:</p>
<br />
<div class="itemizedlist">
<ul class="itemizedlist" style="list-style-type: disc;">
<li class="listitem">
<p><span class="emphasis"><em>Native dynamic translations</em></span>. 
Many programs use the PO format as the native format for their user 
interface text. These include the KDE and Gnome desktop environments, 
GNU tools, etc. Translated PO files are compiled into binary MO files 
(which is done by the <span class="command"><strong>msgfmt</strong></span>
 command from Gettext) and installed in a proper location. Then the 
program fetches translations from them at runtime, which is what makes 
this "dynamic" translation.</p>
</li>
<li class="listitem">
<p><span class="emphasis"><em>Intermediate dynamic translations</em></span>.
 Some software keeps user interface text in their own custom format. 
This is the case, for example, with Mozilla and OpenOffice programs. 
Such custom format files are first converted into PO files, translated, 
and then converted back into the original format, for runtime 
consumption by these programs.</p>
</li>
<li class="listitem">
<p><a name="p-intsttr" id="p-intsttr"></a><span class="emphasis"><em>Intermediate static translations</em></span>.
 Static text data, such as software documentation, is converted from its
 source format into the PO format, translated, and then converted back 
into the original format. An example of such documentation format would 
be the <a class="ulink" href="http://www.docbook.org/" target="_top">Docbook</a>.
 Out of translated files in the original format, the final documents for
 user consumption are created, such as PDF files or HTML pages.</p>
</li>
</ul>
</div>
<p>This variety of usage should be kept in mind, as while the PO format 
is one, the text exposed for translation in PO files will have embedded 
elements which are tightly related to the source of what is translated. 
For example, user interface text will frequently contain <span class="emphasis"><em>format directives</em></span>,
 while documentation text may be written with HTML-like markup. This 
means that the translator should be aware, in general, of what kind of 
source is being translated through a particular PO file.</p>
<p>The development of the PO format has been driven solely by the needs 
of its users, as with time these needs became well formulated and 
generalizable. Thanks to this, features of the PO format other than the 
very basic can be gradually introduced as necessary, and stay out of the
 way when they are not. The format is quite compact, human-readable and 
editable without special-purpose tools (though, of course, these come in
 handy). These aspects benefit the learning curve, everyday usage, and 
instructional texts such as this one.</p>
<p>Although translators will frequently prefer to work on PO files using
 dedicated PO editors, which purport to hide "technical details" such as
 the underlying file format, they should nevertheless understand the PO 
format well. This is because the PO format is more than a simple 
container of the text to be translated, instead it reflects important 
concepts in the translation workflow. To put it more concretely, the 
translator should determine out how a given dedicated PO editor exposes 
the bits of information from the PO file in its interface, and whether 
it trully exposes all of them.</p>
<div class="sect1">
<div class="titlepage">
<div>
<div>
<h2 class="title" style="clear: both"><a name="sec-pobasic" id="sec-pobasic"></a>2.1.&nbsp;Basic Syntax</h2>
</div>
</div>
</div>
<p>The PO format is a plain text format, written in files with <code class="filename">.po</code> extension. A PO file contains a number of <span class="emphasis"><em>messages</em></span>,
 partly independent text segments to be translated, which have been 
grouped into one file according to some logical division of what is 
being translated. For example, a standalone program will frequently have
 all its user interface messages in one PO file, and all documentation 
messages in another; or, user interface may be split into several PO 
files by major program modules, documentation split by chapters, etc. PO
 files are also called <span class="emphasis"><em>message catalogs</em></span>.</p>
<p>Here is an excerpt from the middle of a PO file, showing three simple messages, which are untranslated:</p>
<pre class="programlisting"><span class="nl">#: finddialog.cpp:38</span>
<span class="nv">msgid</span> <span class="s">"Globular Clusters"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: finddialog.cpp:39</span>
<span class="nv">msgid</span> <span class="s">"Gaseous Nebulae"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: finddialog.cpp:40</span>
<span class="nv">msgid</span> <span class="s">"Planetary Nebulae"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>Each message contains the keyword <code class="varname">msgid</code>, which is followed by the original string (usually in English for software), wrapped in double quotes. The keyword <code class="varname">msgstr</code>
 denotes the string which to become the translation, also double-quoted.
 After you go through the PO file and add translations, these messages 
would read:</p>
<pre class="programlisting"><span class="nl">#: finddialog.cpp:38</span>
<span class="nv">msgid</span> <span class="s">"Globular Clusters"</span>
<span class="nv">msgstr</span> <span class="s">"Globularna jata"</span>
⁠
<span class="nl">#: finddialog.cpp:39</span>
<span class="nv">msgid</span> <span class="s">"Gaseous Nebulae"</span>
<span class="nv">msgstr</span> <span class="s">"Gasne magline"</span>
⁠
<span class="nl">#: finddialog.cpp:40</span>
<span class="nv">msgid</span> <span class="s">"Planetary Nebulae"</span>
<span class="nv">msgstr</span> <span class="s">"Planetarne magline"</span>
</pre>
<p>Based on this example, translating a PO file looks rather simple, and
 for the most part it is. There exists, however, a number of details 
which you have to take into account from time to time, in order to 
produce translation of high quality. The rest of this chapter deals with
 such details.</p>
<p>As is usual with text formats, immediately something must be said about the <span class="emphasis"><em>text encoding</em></span> of a PO file. While you could use encodings other than UTF-8 if no non-ASCII letters are used in the original text, you really <span class="emphasis"><em>should</em></span>
 use UTF-8. The encoding is specified within the PO file itself, and by 
default it is UTF-8; if you want to use another encoding, you must 
specify it in the <a class="link" href="http://pology.nedohodnik.net/doc/user/en_US/ch-poformat.html#sec-poheader" title="2.6.&nbsp;PO Header">PO header</a> (described later).</p>
<p>Leaving some messages in the PO file untranslated is technically not a
 problem. For every untranslated message, programs will typically show 
the original text to the user, so that not all information is lost. 
Format converters (such as used in <a class="link" href="http://pology.nedohodnik.net/doc/user/en_US/ch-poformat.html#p-intsttr">intermediate static</a>
 translations) may do the same, or decline to create the target file 
unless the PO file is translated fully or over a prescribed threshold. 
Of course, you should strive to have the PO files under your maintenance
 completely translated, in order for the users not to be faced with 
mixed original and translated text.</p>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-posrcref" id="sec-posrcref"></a>2.1.1.&nbsp;Source References</h3>
</div>
</div>
</div>
<p>Each message in the previous example also contains the <span class="emphasis"><em>source reference comment</em></span>, which is the line starting with <code class="literal">#:</code> above the <code class="literal">msgid "..."</code>
 line. It tells from which source file of the program code (or source 
document of any kind), and the line in that source file, the message has
 been extracted into the PO file. This piece of data may look strange at
 first--of what use is it to translators, to merit inclusion in the PO 
file? Since the PO format has been developed in context of free 
software, the source reference enables you to actually look up the 
message in the source file, when you need <span class="emphasis"><em>more context</em></span>
 to translate a certain message. This does not require of you to be a 
programmer, as source code is frequently readable enough to infer the 
message context without actually understanding the code.</p>
<p>For example, in the translation the text in title position may need 
to have a certain grammatical or ortographical form, and it may not be 
apparent from the PO file alone if the message:</p>
<pre class="programlisting"><span class="nl">#: addcatdialog.cpp:45</span>
<span class="nv">msgid</span> <span class="s">"Import Catalog"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>is used in title position. By following the source reference, you find this statement in the source file <code class="filename">addcatdialog.cpp</code>, line 45:</p>
<pre class="programlisting"><span class="n">setCaption</span><span class="p">(</span> <span class="n">i18n</span><span class="p">(</span> <span class="s">"Import Catalog"</span> <span class="p">)</span> <span class="p">);</span>
</pre>
<p>The <code class="literal">setCaption(...)</code> bit makes it highly 
likely that the message is indeed being used in a title position. Some 
dedicated PO editors provide ways to quickly and comfortably look up 
source references, just by pressing a keyboard shortcut, which makes 
this approach to context determination that much easier.</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-powrap" id="sec-powrap"></a>2.1.2.&nbsp;String Wrapping</h3>
</div>
</div>
</div>
<p>When a message is long or contains some logical line-breaks, its original and translation strings may be <span class="emphasis"><em>wrapped</em></span> in the PO file (with wrapping boundary usually at column 80), such as this:</p>
<pre class="programlisting"><span class="nl">#: indimenu.cpp:96</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"No INDI devices currently running. To run devices, please select devices "</span>
<span class="s">"from the Device Manager in the devices menu."</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>This wrapping is entirely invisible to the consumer of the PO file. 
PO processing tools introduce wrapping mostly as a convenience to 
translators who like to work on PO files with plain text editors. This 
means that you are free to wrap the translation (the <code class="varname">msgstr</code>
 string) in the same way, differently, or not to wrap it at all. You 
should only not forget to enclose each wrapped line in double quotes, 
same as it is done for <code class="varname">msgid</code>. For example, this translation of the previous message:</p>
<pre class="programlisting"><span class="nl">#: indimenu.cpp:96</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"No INDI devices (...)"</span>
<span class="s">"(...) in the devices menu."</span>
<span class="nv">msgstr</span> <span class="s">""</span>
<span class="s">"Nema INDI uređaja (...)"</span>
<span class="s">"(...) u meniju uređaja."</span>
</pre>
<p>is equivalent to this one:</p>
<pre class="programlisting"><span class="nl">#: indimenu.cpp:96</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"No INDI devices (...)"</span>
<span class="s">"(...) in the devices menu."</span>
<span class="nv">msgstr</span> <span class="s">"Nema INDI uređaja (...) u meniju uređaja."</span>
</pre>
<p>Dedicated PO editors may even not show wrapping to the translator, or
 wrap lines on their own independently of the underlying PO file. 
Curiosly enough, most PO editors seem to follow the original wrapping, 
at least by default. At any rate, if you would like to have all strings 
non-wrapped (including <code class="varname">msgid</code>) or vice versa, there are command line tools to achieve this.</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-pomsguniq" id="sec-pomsguniq"></a>2.1.3.&nbsp;Uniqueness of Messages</h3>
</div>
</div>
</div>
<p>A message in the PO file is <span class="emphasis"><em>uniquely identified</em></span> by its <code class="varname">msgid</code>
 string (this is not entirely true, as will be explained shortly, but 
consider it approximately true for the moment). This means that, as the 
source which is translated evolves in time, a message may change some of
 its elements or the position within the PO file, but as long as it has 
the same <code class="varname">msgid</code> string, it is the same message. Those other, non-identifying elements include the translation (<code class="varname">msgstr</code>
 string), source reference comments, etc. Position means either the line
 number in the PO file, or relative position to other messages.</p>
<p>The first consequence of this fact is that the only reliable way to report a message to someone is to state its <code class="varname">msgid</code> string, in full or in sufficient part, even if the other person has access to the PO file where the message is found.<a href="#ftn.idp54108592" class="footnote" name="idp54108592" id="idp54108592"><sup class="footnote">[3]</sup></a>
 Newcomer translators are sometimes not briefed about this, and then 
they at first report the line number of the message, or its ordinal 
number in the range of all messages, without giving the <code class="varname">msgid</code>.
 Line numbers cannot work because, for example, of the arbitrary line 
wrapping as described previously. Ordinal numbers do not work because 
your PO file may be slightly older or newer than that of the other 
person, and the ordinals may have changed in the meantime.</p>
<p>The second consequence is that there cannot be two messages with the same <code class="varname">msgid</code>
 in the same PO file (again not exactly true, see later). If the same 
text has been used two or more times in the source, then in the PO file 
it will appear as a single message, with its source reference comment (<code class="literal">#:</code>) listing all appearances. For example, the source reference of this message:</p>
<pre class="programlisting"><span class="nl">#: colorscheme.cpp:79 skycomponents/equator.cpp:31</span>
<span class="nv">msgid</span> <span class="s">"Equator"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>shows that it is used at two places in the program source code. This 
feature of the PO format prevents needless duplication of work, by 
assuring that any duplicate text in the source is translated only once. 
This efficiency optimization can sometimes be a double-edged sword, but 
with an elegant solution for the problem that can arise, as you will see
 shortly.</p>
<p>The third, so to say, consequence, though more of a remark for clarity, is this: you should never modify the <code class="varname">msgid</code> string. Not only that doing so would have no purpose, but if the <code class="varname">msgid</code>
 is modified, the consumer of the translated PO file will not see the 
message as translated, since it will fetch messages by matching their <code class="varname">msgid</code> strings.</p>
</div>
</div>
<div class="sect1">
<div class="titlepage">
<div>
<div>
<h2 class="title" style="clear: both"><a name="sec-pocontext" id="sec-pocontext"></a>2.2.&nbsp;Message Context</h2>
</div>
</div>
</div>
<p>Depending on the language of translation, sometimes it may be hard to
 translate a message properly by considering it in isolation, without 
any additional context. Naive translation may break style guidelines, or
 worse, misinterpret the meaning of the original text. To avoid this, 
there are several ways in which you can infer the context in which the 
message is used.</p>
<p>One way you have seen already: looking into the source file of the 
message, as pointed to by the source reference comment. But, this way 
can be tedious. Not only because the source code may look menacing to a 
translator, but also, while readily available for free software, it is 
usually not very comfortable to keep all that source code around just 
for the sake of context checking. This is a well understood difficulty, 
so additional context indicators have been devised.</p>
<p>One simple way to keep track of the context is to, when translating a
 given message, keep in sight several messages that precede and follow 
it. As a trivial example, the following four messages:</p>
<pre class="programlisting"><span class="nl">#: locationdialog.cpp:228</span>
<span class="nv">msgid</span> <span class="s">"Really override original data for this city?"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: locationdialog.cpp:229</span>
<span class="nv">msgid</span> <span class="s">"Override Existing Data?"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: locationdialog.cpp:229</span>
<span class="nv">msgid</span> <span class="s">"Override Data"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: locationdialog.cpp:229</span>
<span class="nv">msgid</span> <span class="s">"Do Not Override"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>are rather obviously a question in some kind of a message dialog, the
 title of that dialog, and the two answer buttons, so that you know 
exactly how the messages are related. Aside from the pure meaning, 
conclusions such as this may be further supported by the style 
conventions of original text (for English, title word case for dialog 
titles, but also for push buttons), and the source reference comments 
(here they reveal that all four messages are in two adjacent lines of 
the same source file). With time you will start to pick up patterns of 
this kind which are typical for the source which you translate, and be 
more confident in your estimates.</p>
<p>Up to this point, all the context gathering rested on the shoulders 
of the translator. However, when authors of the original text, for 
example programmers, are themselves sufficiently aware of the 
translation issues, they can explicitly provide some context for 
translators. This is particularly warranted when a message is quite 
strange, when it puts technical limitations on the translation, when it 
is used in an unexpected way, and so on.</p>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-poautocmnt" id="sec-poautocmnt"></a>2.2.1.&nbsp;Extracted Comments</h3>
</div>
</div>
</div>
<p>One place where explicit context provided by the authors can be found in a message, is within <span class="emphasis"><em>extracted comments</em></span>, which start with <code class="literal">#.</code>. For example, the message:</p>
<pre class="programlisting"><span class="c1">#. TRANSLATORS: A test phrase with all letters of the English alphabet.</span>
<span class="c1">#. Replace it with a sample text in your language, such that it is</span>
<span class="c1">#. representative of language's writing system.</span>
<span class="nl">#: kdeui/fonts/kfontchooser.cpp:382</span>
<span class="nv">msgid</span> <span class="s">"The Quick Brown Fox Jumps Over The Lazy Dog"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>has an extracted comment which tells you to avoid translating the 
English phrase for what it is, but to instead construct a phrase with 
the described property in your language.</p>
<p>This kind of context usually begins with an agreed-upon keyword, which in the above case is <code class="literal">TRANSLATORS:</code>, which is recommended by Gettext, but in principle depends on the source environment. It could be, for example, <code class="literal">i18n:</code> (short for "internationalization").</p>
<p>Extracted comments can sometimes be added not by a human author, but 
by a tool used to create or process PO files. For example, when 
markup-text documents are translated, such as HTML, or Docbook for 
documentation, the extracted comment frequently states the tag which 
wraps the text in the original document:</p>
<pre class="programlisting"><span class="c1">#. Tag: title</span>
<span class="nl">#: skycoords.docbook:73</span>
<span class="nv">msgid</span> <span class="s">"The Horizontal Coordinate System"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>In this example, the <code class="literal">#. Tag: title</code> comment informs you that the message is a title, so that you can adjust the translation accordingly.</p>
<p>Another frequent example where processing tools provide extracted 
comments is when the PO file is created in a slightly roundabout way, 
such that source references do not really point to the source file, but 
to a temporary source file which existed only during the creation of the
 PO file. To make this less misleading, the extracted comment may state 
the true source:</p>
<pre class="programlisting"><span class="c1">#. i18n: file: tools/observinglist.ui:263</span>
<span class="c1">#. i18n: ectx: property (toolTip), widget (KPushButton, ScopeButton)</span>
<span class="nl">#: rc.cpp:5865</span>
<span class="nv">msgid</span> <span class="s">"Point telescope at highlighted object"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>Here <code class="literal">rc.cpp:5865</code> is the reference to the temporary source file, whereas the true source file is given as <code class="literal">file: tools/observinglist.ui:263</code>. (The other automatically extracted comment, <code class="literal">ectx: ...</code>, may look a bit cryptic, but you can still easily conclude from it that this message is a tooltip for a push button.)</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-podisamb" id="sec-podisamb"></a>2.2.2.&nbsp;Disambiguating Contexts</h3>
</div>
</div>
</div>
<p>Consider the following two messages from an program user interface:</p>
<pre class="programlisting"><span class="c1">#. TRANSLATORS: First letter in 'Scope'</span>
<span class="nl">#: tools/observinglist.cpp:700</span>
<span class="nv">msgid</span> <span class="s">"S"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="c1">#. TRANSLATORS: South</span>
<span class="nl">#: skycomponents/horizoncomponent.cpp:429</span>
<span class="nv">msgid</span> <span class="s">"S"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>At first sight, you could think that it was nice of the programmer to add the explicit context (<code class="literal">#. TRANSLATORS: ...</code>
 lines), informing that the "S" of the first message is short for 
"Scope", and the "S" of the second message short for "South", so that 
translators know that they should use the letters corresponding to these
 words in their languages. But, can you spot the problem?</p>
<p>The problem is that these messages cannot be part of a valid PO file, since, as it was <a class="link" href="http://pology.nedohodnik.net/doc/user/en_US/ch-poformat.html#sec-pomsguniq" title="2.1.3.&nbsp;Uniqueness of Messages">mentioned earlier</a>, all messages must have unique <code class="varname">msgid</code> strings. Instead, in a real PO file, these two messages would be collapsed into one:</p>
<pre class="programlisting"><span class="c1">#. TRANSLATORS: First letter in 'Scope'</span>
<span class="c1">#. TRANSLATORS: South</span>
<span class="nl">#: tools/observinglist.cpp:700 skycomponents/horizoncomponent.cpp:429</span>
<span class="nv">msgid</span> <span class="s">"S"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>Both contexts are still present, translators are still well informed,
 but it is now required that the words "Scope" and "South" also begin 
with the same letter in the target language--an extremely unlikely 
proposal.</p>
<p>In situations such as this, the programmer can equip messages with a different type of context, the <span class="emphasis"><em>disambiguating context</em></span>. These contexts are no longer presented as extracted comments, but through another keyword string, the <code class="varname">msgctxt</code>:</p>
<pre class="programlisting"><span class="nl">#: tools/observinglist.cpp:700</span>
<span class="nv">msgctxt</span> <span class="s">"First letter in 'Scope'"</span>
<span class="nv">msgid</span> <span class="s">"S"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: skycomponents/horizoncomponent.cpp:429</span>
<span class="nv">msgctxt</span> <span class="s">"South"</span>
<span class="nv">msgid</span> <span class="s">"S"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>This is now a valid PO file, and you can translate each "S" on its own.</p>
<p>This updates the earlier approximation that messages must be unique by <code class="varname">msgid</code> strings to the real requirement: messages must be unique by the combination of <code class="varname">msgctxt</code> and <code class="varname">msgid</code> strings. If the <code class="varname">msgctxt</code> string is missing, as it usually is, you can think of it as being present but null-valued.<a href="#ftn.idp52577568" class="footnote" name="idp52577568" id="idp52577568"><sup class="footnote">[4]</sup></a></p>
<p>A rather frequent example of need for disambiguating contexts is when
 the original text is a single adjective in English, and used at several
 places in the source:</p>
<pre class="programlisting"><span class="nl">#: utils/kateautoindent.cpp:78 utils/katestyletreewidget.cpp:132</span>
<span class="nv">msgid</span> <span class="s">"Normal"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>In many languages the adjective form must match the gender of the 
noun to which it refers, so if the "Normal" above refers both to 
indentation mode and text style, it is almost certainly necessary to 
provide disambiguating contexts:</p>
<pre class="programlisting"><span class="nl">#: utils/katestyletreewidget.cpp:132</span>
<span class="nv">msgctxt</span> <span class="s">"Text style"</span>
<span class="nv">msgid</span> <span class="s">"Normal"</span>
<span class="nv">msgstr</span> <span class="s">"običan"</span>
⁠
<span class="nl">#: utils/kateautoindent.cpp:78</span>
<span class="nv">msgctxt</span> <span class="s">"Autoindent mode"</span>
<span class="nv">msgid</span> <span class="s">"Normal"</span>
<span class="nv">msgstr</span> <span class="s">"obično"</span>
</pre>
<p>You can imagine that programmers in general cannot know when a 
certain phrase, same in English when used in two contexts, needs 
different translations in some other language. This means that you, the 
translator, should inform them to add a disambiguating context when you 
determine that you need one.<a href="#ftn.idp52583712" class="footnote" name="idp52583712" id="idp52583712"><sup class="footnote">[5]</sup></a></p>
<p><a name="p-embctxt" id="p-embctxt"></a>At the moment of this writing, the <code class="varname">msgctxt</code>
 string is one of the younger additions to the PO format. But the need 
for disambiguating contexts was observed much earlier, and different 
translation environments have historically used different custom 
solutions to provide them. Such older PO files can still be encountered,
 so it is useful to present a few examples of custom disambiguating 
contexts. Before the <code class="varname">msgctxt</code> was introduced, messages indeed had to be unique by <code class="varname">msgid</code> alone, so disambiguating context had to be a part of the <code class="varname">msgid</code>,
 embedded with some special syntax. Here is how the first message from 
the previous example would look like in a PO file comming from a KDE 
program of circa 2006:</p>
<pre class="programlisting"><span class="nl">#: utils/katestyletreewidget.cpp:132</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"_⁠: Text style</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Normal"</span>
<span class="nv">msgstr</span> <span class="s">"običan"</span>
</pre>
<p>The disambiguating context has been embedded at the beginning of the <code class="varname">msgid</code>, surrounded by <code class="literal">_⁠: ...\n</code>. In a contemporary Gnome program, the same message would look something like this:</p>
<pre class="programlisting"><span class="nl">#: utils/gatestyletreewidget.c:132</span>
<span class="nv">msgid</span> <span class="s">"Text style|Normal"</span>
<span class="nv">msgstr</span> <span class="s">"običan"</span>
</pre>
<p>Here the context is again at the beginning of <code class="varname">msgid</code>, but it is separated from the text only by the pipe character (<code class="literal">|</code>).</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-pomancmnt" id="sec-pomancmnt"></a>2.2.3.&nbsp;Translator Comments</h3>
</div>
</div>
</div>
<p>Sometimes you will need to translate a message without explicit 
context in a non-obvious way, after you have determined that such 
translation is needed by looking into the source or seeing the message 
in user interface at runtime. This may present a difficulty when the 
message is revisited, for example, by a proof-reader in the review 
process, or by another translator if the message got modified later on. 
This other person may conclude that the translation is wrong and "fix" 
it, or at the very least waste time by asking around why it was 
translated in that way.</p>
<p>Conversely, sometimes you may be unsure if your translation is 
exactly correct, for example if you have correctly guessed the context, 
or whether you have used correct terminology. In that case you can, of 
course, consult with fellow translators, but this would break you out of
 the "flow" state while working. It is better if such communication is 
delayed to the moment when the translation of the PO file is otherwise 
complete.</p>
<p>For these situations, you can write down your own inferred context, doubts or notes, in another type of comment, the <span class="emphasis"><em>translator comment</em></span>. These comments start simply with <code class="literal">#</code>
 (hash and space), followed by any text whatsoever. As with other 
comments, there may be any number of them. A hypothetical example:</p>
<pre class="programlisting"><span class="c1"># Wikipedia says that ‘etrurski’ is our name for this script.</span>
<span class="nl">#: viewpart/UnicodeBlocks.h:151</span>
<span class="nv">msgid</span> <span class="s">"Old Italic"</span>
<span class="nv">msgstr</span> <span class="s">"etrurski"</span>
</pre>
<p>In reality, a translator comment such as the one above would probably
 be written in the language of translation, as there is no reason for it
 to be in English. This is not to say that translator comments should 
never be in English, there may be situations when that could be 
advantageous.</p>
<p>It is particularly important to know that translator comments are the <span class="emphasis"><em>only</em></span>
 type of comment that all well-behaved PO processing tools are 
guaranteed to preserve in the same way as translation. For example, if 
you would write something into an extracted comment (<code class="literal">#.</code>),
 it would very soon dissapear in one of the standard maintenance 
procedures. So make sure you add any personal remarks into translator 
comments, and nowhere else.</p>
</div>
</div>
<div class="sect1">
<div class="titlepage">
<div>
<div>
<h2 class="title" style="clear: both"><a name="sec-poconssub" id="sec-poconssub"></a>2.3.&nbsp;Constructive Substrings</h2>
</div>
</div>
</div>
<p>Message text sometimes contains substrings which are not visible to 
the user of the program or to the reader of the manual, but are used by 
the program or the rendering engine to construct the final visible text.
 Translators should reproduce such substrings in the translation as 
well, most of the time exactly as they are in the original, but 
sometimes also with some modifications.</p>
<p>For better or worse, constructive substrings tend to be tightly 
linked to the source environment of the text, for example the particular
 programming language in which the program is written, or the particular
 markup language for static content like documentation. To produce high 
quality translations, you will benefit from having basic understanding 
of the constructive substrings possible in the source environment, of 
their function and behavior. The prerequisite to this, as mentioned in 
the opening of this chapter, is that you are aware of what is the source
 of the text in the PO file.</p>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-poformdir" id="sec-poformdir"></a>2.3.1.&nbsp;Format Directives</h3>
</div>
</div>
</div>
<p>When a file manager shows a message like "Really delete file 
tmp10.txt?" or "Open with Froobaz", the "tmp10.txt" and "Froobaz" parts 
had to be added to the rest of the text at runtime. In such cases, the 
original text as seen by the translator will contain <span class="emphasis"><em>format directives</em></span>,
 substrings which the program will replace with dynamically determined 
arguments to complete the message to be shown to the user.</p>
<p>For example, in the PO file comming from a KDE program, there will be messages like this one:</p>
<pre class="programlisting"><span class="nl">#: skycomponents/constellationlines.cpp:106</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"No star named %1 found."</span>
<span class="nv">msgstr</span> <span class="s">"Nema zvezde po imenu %1."</span>
</pre>
<p>The format directive in this message is <code class="literal">%1</code>,
 and it will be substituted at runtime with the text provided by the 
user as the name to search for. If several arguments need to be 
substituted in the text, there can be more format directives with 
increasing numbers: <code class="literal">%1</code>, <code class="literal">%2</code>, <code class="literal">%3</code>...</p>
<p>A new type of comment has appeared as well, the <span class="emphasis"><em>flags comment</em></span>. This comment begins with <code class="literal">#,</code>,
 followed by the comma-separated list of keywords--the flags--which 
clarify the state or the type of the message. In this example the flag 
is <code class="literal">kde-format</code>, indicating that format directives in the message are of KDE type.</p>
<p>Format directives differ across source environments, but they are 
usually easy to recognize. The previous message, if it would be found in
 a Gnome program, would look like this:</p>
<pre class="programlisting"><span class="nl">#: skycomponents/constellationlines.c:106</span>
<span class="nd">#, c-format</span>
<span class="nv">msgid</span> <span class="s">"No star named </span><span class="si">%s</span><span class="s"> found."</span>
<span class="nv">msgstr</span> <span class="s">"Nema zvezde po imenu </span><span class="si">%s</span><span class="s">."</span>
</pre>
<p>The format directive changed to <code class="literal">%s</code>, and the format flag to <code class="literal">c-format</code>. This is the format used by most programs written in C, and by many written in C++. In C format, the <code class="literal">%s</code> directive is for substituting string arguments, and another frequent directive is <code class="literal">%d</code> for integer numbers; but there are many more.</p>
<p>For one more example, to illustrate the diversity of format 
directives, if the program would have been written in Python the message
 could look like:</p>
<pre class="programlisting"><span class="nl">#: skycomponents/constellationlines.cpp:106</span>
<span class="nd">#, python-format</span>
<span class="nv">msgid</span> <span class="s">"No star named </span><span class="si">%(s</span><span class="s">tarname)s found."</span>
<span class="nv">msgstr</span> <span class="s">"Nema zvezde po imenu </span><span class="si">%(s</span><span class="s">tarname)s."</span>
</pre>
<p>Here the format directive is <code class="literal">%(starname)s</code>, which indicates the argument type similar to C format (<code class="literal">%s</code>), but also its name in parenthesis. Hence the <code class="literal">python-format</code>
 flag. This name must not be changed in translation, as otherwise the 
program will not be able to match the directive and make the substitute.
 This would probably make the program crash when it tries to display the
 message.</p>
<p>You only need to make sure that each directive from the original 
string is found in the translation, and very rarely to modify the 
directives themselves. Format flags, such as <code class="literal">kde-format</code>, <code class="literal">c-format</code>,
 etc., are there not only as information for translators, but they are 
also used by tools for validating PO files. For example, if you forget 
or mistype a format directive in the translation, such tools will report
 it. Dedicated PO editors may warn on the spot, or when saving the PO 
file. This provides you with a "safety net", so long as you remember to 
perform the checks after completing the translation (if the PO editor 
does not do it automatically).</p>
<p>One situation that may require modification of directives is when 
there are several of them, and they need to be ordered differently in 
the translation:</p>
<pre class="programlisting"><span class="nl">#: kxsldbgpart/libxsldbg/xsldbg.cpp:256</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"%1 took %2 ms to complete."</span>
<span class="nv">msgstr</span> <span class="s">"Trebalo je %2 ms da se %1 završi."</span>
</pre>
<p>With KDE format directives, which are numbered, reordering is as 
simple as above. Similarly for the Python format, where directives are 
named. But for formats where directives are neither numbered nor named 
by default, like in C format (where they only state argument type), you 
can sometimes modify directives to the desired effect:</p>
<pre class="programlisting"><span class="nl">#: gxsldbgpart/libxsldbg/xsldbg.c:256</span>
<span class="nd">#, c-format</span>
<span class="nv">msgid</span> <span class="s">"</span><span class="si">%s</span><span class="s"> took </span><span class="si">%d</span><span class="s"> ms to complete."</span>
<span class="nv">msgstr</span> <span class="s">"Trebalo je %2$d ms da se %1$s završi."</span>
</pre>
<p>If the directives are numbered or named, and there is more than one 
same-number or same-name directive, usually any of the duplicates can be
 dropped in the translation. This may be useful in a longer text, for 
example when in the translation a pronoun can be safely used instead of 
repeating the argument:</p>
<pre class="programlisting"><span class="nl">#: hypothetical.cpp:100</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"%1 is the blah, blah, blah. With %1 you can blah, blah."</span>
<span class="nv">msgstr</span> <span class="s">"%1 je bla, bla, bla. Pomoću njega možete bla, bla."</span>
</pre>
<p>Here "njega" is a pronoun used instead of repeating the <code class="literal">%1</code>.
 Conversely, it is possible to repeat the directive where the original 
text had used a pronoun, if it better fits the translation.</p>
<p>Sometimes, instead of using a format directive, the programmer may try to concatenate the full text out of separate messages:</p>
<pre class="programlisting"><span class="nl">#: hypothetical.cpp:100</span>
<span class="nv">msgid</span> <span class="s">"No star named "</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: hypothetical.cpp:100</span>
<span class="nv">msgid</span> <span class="s">" found."</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>Here the program will fetch the first message, append to it the 
argument, and then append the second message. This kind of programming 
is considered as one of the basic errors when making a translatable 
program, because it forces translators to "piece the puzzle", which may 
not even be possible in every language. This is thankfully rare today, 
but when it does happen, while you can try to work around, it is better 
that you contact the authors to have the source code fixed.</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-pomarkup" id="sec-pomarkup"></a>2.3.2.&nbsp;Text Markup</h3>
</div>
</div>
</div>
<p>Programs sometimes show parts of the text in non-plain text: certain 
words may be italic or bold, titles in larger font size, list items with
 graphical bullets, etc. This is frequent, for example, in tooltips and 
message boxes. Yet richer typographic elements of this kind are usually 
found in documentation and other static content, which may need to be 
suitable both for reading on screen and printing on paper. In such 
messages, the original text will contain <span class="emphasis"><em>markup</em></span>, where words, phrases, and whole paragraphs are wrapped with special <span class="emphasis"><em>tags</em></span>.</p>
<p>The following messages show typical examples of markup in program user interface:</p>
<pre class="programlisting"><span class="nl">#: rc.cpp:1632 rc.cpp:3283</span>
<span class="nv">msgid</span> <span class="s">"</span><span class="sx">&lt;b&gt;</span><span class="s">Name:</span><span class="sx">&lt;/b&gt;</span><span class="s">"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: kgeography.cpp:375</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"</span><span class="sx">&lt;qt&gt;</span><span class="s">Current map:</span><span class="sx">&lt;br/&gt;&lt;b&gt;</span><span class="s">%1</span><span class="sx">&lt;/b&gt;&lt;/qt&gt;</span><span class="s">"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: rc.cpp:2537 rc.cpp:4188</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"</span><span class="sx">&lt;b&gt;</span><span class="s">Tip</span><span class="sx">&lt;/b&gt;&lt;br/&gt;</span><span class="s">Some non-Meade telescopes support a subset of the LX200 "</span>
<span class="s">"command set. Select </span><span class="sx">&lt;tt&gt;</span><span class="s">LX200 Basic</span><span class="sx">&lt;/tt&gt;</span><span class="s"> to control such devices."</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>The markup in these messages is XML-like, where tags for visual formatting are specified as <code class="literal">&lt;<em class="replaceable"><code>tag</code></em>&gt;...&lt;/<em class="replaceable"><code>tag</code></em>&gt;</code> wrappings around the visible text segments. For example <code class="literal">&lt;b&gt;...&lt;/b&gt;</code> tells that the text inside should be shown in boldface, while <code class="literal">&lt;tt&gt;...&lt;/tt&gt;</code> that a monospace font should be used, and lone <code class="literal">&lt;br/&gt;</code> introduces the line break. A reader knowing some HTML will instantly recognize these tags.</p>
<p>Another frequent XML-like markup is used in documentation PO files, 
which are in many environments (like KDE or Gnome) mostly written in the
 Docboox XML format:</p>
<pre class="programlisting"><span class="c1">#. Tag: title</span>
<span class="nl">#: blackbody.docbook:13</span>
<span class="nv">msgid</span> <span class="s">"</span><span class="sx">&lt;title&gt;</span><span class="s">Blackbody Radiation</span><span class="sx">&lt;/title&gt;</span><span class="s">"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="c1">#. Tag: para</span>
<span class="nl">#: geocoords.docbook:28</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"The Equator is obviously an important part of this coordinate system; "</span>
<span class="s">"it represents the </span><span class="sx">&lt;emphasis&gt;</span><span class="s">zeropoint</span><span class="sx">&lt;/emphasis&gt;</span><span class="s"> of the latitude angle, "</span>
<span class="s">"and the halfway point between the poles. The Equator is the "</span>
<span class="s">"</span><span class="sx">&lt;firstterm&gt;</span><span class="s">Fundamental Plane</span><span class="sx">&lt;/firstterm&gt;</span><span class="s"> of the geographic coordinate "</span>
<span class="s">"system. </span><span class="sx">&lt;link linkend='ai-skycoords'&gt;</span><span class="s">All Spherical</span><span class="sx">&lt;/link&gt;</span><span class="s"> Coordinate "</span>
<span class="s">"Systems define such a Fundamental Plane."</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>The Docbook tags are named somewhat differently to the HTML-like tags
 from the previous example. The describe the meaning of text that they 
wrap, rather than the visual appearance (the so called <span class="emphasis"><em>semantic</em></span>
 markup). But it is all the same for translator, except that knowing the
 meanings of text parts may be benefitial for context. Docbook tags will
 also sometimes provide one or few <span class="emphasis"><em>attributes</em></span> following the opening tag, such as <code class="literal">&lt;link linkend=...&gt;</code> in the second message above (HTML tags may have this too).</p>
<p>When translating markup text, you should, in general, reproduce the 
same set of tags in the translation, assigning them to appropriate 
translated segments. Under no circumstances may the tags themselves be 
translated (e.g. <code class="literal">&lt;title&gt;</code> or <code class="literal">&lt;emphasis&gt;</code>), since they are processed by the computer to produce the final formatted text. As for tag attributes (<code class="literal">linkend='ai-skycoords'</code>
 in the example above), attribute names are also never translated, but 
in rare occasions their values in quotes may be (usually when a value is
 clearly a human-readable text).</p>
<p>However, this is not to say that you should never modify markup. 
Especially with HTML-like tags, not so rarely the markup in the original
 text is sloppy (missing closing tags), and you are free to correct it 
in translation. Another example would be in CJK languages<a href="#ftn.idp52648768" class="footnote" name="idp52648768" id="idp52648768"><sup class="footnote">[6]</sup></a>, where bold text is hard to read at normal font sizes, so CJK translators tend to remove <code class="literal">&lt;b&gt;</code>
 tags in favor of quotes. In general, the more you are familiar with the
 particular markup, the more you can think of doing something other than
 directly copying it from the original text.</p>
<p>Sometimes there are parts in the original text that may look somewhat like XML-like markup, but are actually not. For example:</p>
<pre class="programlisting"><span class="nl">#: utils/katecmds.cpp:180</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"Missing argument. Usage: %1 </span><span class="sx">&lt;value&gt;</span><span class="s">"</span>
<span class="nv">msgstr</span> <span class="s">""</span>                                                                        
</pre>
<p>The <code class="literal">&lt;value&gt;</code> here is not markup, and is shown verbatim to the user. It is a <span class="emphasis"><em>placeholder</em></span>,
 an indicator to the user that a real argument should be put in its 
place. For this reason, in many languages the placeholders are 
translated, and there is no technical problem with that. You should only
 exercise caution not to misjudge a tag for a placeholder. After little 
experience with the particular markup, the difference usually becomes 
obvious.</p>
<p>There are also non-XML like markups that tend to come up for translation. One could be the wiki markup:</p>
<pre class="programlisting"><span class="nl">#: .txt:191</span>
<span class="nv">msgid</span> <span class="s">"=== Overlay Images ==="</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: poformat.txt:193</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"A special kind of localized image is an ''overlay image'', one which "</span>
<span class="s">"does not simply replace the original, but is combined with it [...]"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>Here <code class="literal">===...===</code> is the approximate of <code class="literal">&lt;h2&gt;...&lt;h2&gt;</code> in HTML, while <code class="literal">''...''</code> is the counterpart of <code class="literal">&lt;i&gt;...&lt;i&gt;</code>. Another markup type is the source language for man pages, troff:</p>
<pre class="programlisting"><span class="c1"># type: Plain text</span>
<span class="nl">#: ../../doc/man/wesnoth.6:55</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"compresses a savefile (B</span><span class="sx">&lt;infile&gt;</span><span class="s">)  that is in text WML format into "</span>
<span class="s">"binary WML format (B</span><span class="sx">&lt;outfile&gt;</span><span class="s">)."</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>where <code class="literal">B&lt;...&gt;</code> is the equivalent of <code class="literal">&lt;b&gt;...&lt;b&gt;</code> in HTML.</p>
<p>When you are faced with a new kind of markup, which you have never 
translated before, you should at least skim through a tutorial or two 
about it. This will enable you both to recognize it in the original 
text, and to modify it in translation if necessary.</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-poescapes" id="sec-poescapes"></a>2.3.3.&nbsp;Escape Sequences</h3>
</div>
</div>
</div>
<p>There are a few special characters which cannot appear verbatim in the <code class="varname">msgid</code> or <code class="varname">msgstr</code> strings. Most obviously, think of the plain double quote (<code class="literal">"</code>):
 since it is used to delimit strings, a raw double quote inside the text
 would terminate the string prematurely, and invalidate the message 
syntax. Such characters are therefore written as <span class="emphasis"><em>escape sequences</em></span>, a combination of the backslash (<code class="literal">\</code>)
 and another character, which is interpreted into the appropriate real 
character when showing the message to the user. The plain double quote 
is written as <code class="literal">\"</code>:</p>
<pre class="programlisting"><span class="nl">#: kstars_i18n.cpp:3591</span>
<span class="nv">msgid</span> <span class="s">"The </span><span class="se">\"</span><span class="s">face</span><span class="se">\"</span><span class="s"> on Mars"</span>
<span class="nv">msgstr</span> <span class="s">"</span><span class="se">\"</span><span class="s">Lice</span><span class="se">\"</span><span class="s"> na Marsu"</span>
</pre>
<p>Another frequent escaped character is the newline, presented as <code class="literal">\n</code>:</p>
<pre class="programlisting"><span class="nl">#: kstarsinit.cpp:699</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="s">"The initial position is below the horizon.</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Would you like to reset to the default position?"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
<span class="s">"Početni položaj je ispod horizonta.</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Želite li da vratite na podrazumevani?"</span>
</pre>
<p>Tools that write out PO files usually unconditionally wrap the text 
at newlines, ignoring the specified wrap column, even when wrapping has 
been turned off. This is to increase readability for translator editing 
the PO file. If the text is not composed of markup (e.g. not Docbook), 
newlines are significant to the program user too, so you should carry 
them over into the translation. In general, unless you are confident 
that you can manipulate newlines in a certain way, you should follow the
 lead of <code class="varname">msgid</code>.</p>
<p>Another two escape sequences, usually of much lower frequency than the double quote and the newline, are the tabulator <code class="literal">\t</code> and the backslash itself <code class="literal">\\</code>
 (because single backslash always starts an escape sequence). While 
other escape sequences are possible, they are extremely rare.</p>
<p>Returning to double quotes, keep in mind that while the English 
original usually uses plain ASCII quotes, translators tend to use 
"fancy" quotes according to the orthography of the language:</p>
<pre class="programlisting"><span class="nl">#: kstars_i18n.cpp:3591</span>
<span class="nv">msgid</span> <span class="s">"The </span><span class="se">\"</span><span class="s">face</span><span class="se">\"</span><span class="s"> on Mars"</span>
<span class="nv">msgstr</span> <span class="s">"„Lice“ na Marsu"</span>
</pre>
<p>This holds both for double and single quotes. Do check if some 
particular quote pairs are prescribed by the ortography of your 
language, and use them if they are.</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-poaccel" id="sec-poaccel"></a>2.3.4.&nbsp;Accelerators</h3>
</div>
</div>
</div>
<p>In user interfaces, short texts on widgets used to perform an action 
or open a dialog, frequently have one letter in them underlined. This 
indicates that when the user presses the <span class="keycap"><strong>Alt</strong></span>
 key (on an IBM PC type keyboard) and the underlined letter together, 
the corresponding action will be triggered. Such letters are called <span class="emphasis"><em>accelerators</em></span>, and in message strings they are usually specified by preceding them with a special character, the <span class="emphasis"><em>accelerator marker</em></span>:</p>
<pre class="programlisting"><span class="nl">#: kstarsinit.cpp:163</span>
<span class="nv">msgid</span> <span class="s">"Set Focus &amp;Manually..."</span>
<span class="nv">msgstr</span> <span class="s">"Zadaj fokus &amp;ručno..."</span>
</pre>
<p>Here the accelerator marker is the ampersand (<code class="literal">&amp;</code>).
 Thus, the accelerator in this message will be the letter 'm' in the 
original text, and the letter 'r' in the translation. Accelerator 
markers differ across environments: ampersand is typical KDE and Qt 
programs, in Gnome programs it is the underscore (<code class="literal">_</code>), in OpenOffice the tilde (<code class="literal">~</code>), etc.</p>
<p>It may be difficult to choose accelerators in the translation (where 
to put the accelerator marker), because you can easily get into 
situations where in the same interface context (e.g. within one menu) 
two items end up having the same accelerator. This will not do anything 
too bad, e.g. the program may automatically reassign conflicting 
accelerators, or the user may have to press <span class="keycap"><strong>Alt</strong></span>
 and the letter several times to go through all such items. 
Nevertheless, it is good to avoid conflicting accelerators, but there is
 no definite way to do that; you can only try to track the message 
context in the PO file, and check the running program. This is not only 
the problem of translation, as not so rarely the original itself 
introduces conflicting accelerators.</p>
<p>CJK languages use input methods different to alphabetical ones 
(keyboard layouts), so instead of assigning an ideogram as the 
accelerator, they add a single Latin letter for that purpose alone:</p>
<pre class="programlisting"><span class="nl">#: kstarsinit.cpp:163</span>
<span class="nv">msgid</span> <span class="s">"Set Focus &amp;Manually..."</span>
<span class="nv">msgstr</span> <span class="s">"フォーカスを手動でセット(&amp;M)..."</span>
</pre>
<p>This letter is usually picked to be the same as in the original text,
 thereby reducing the possibility of accelerator conflicts as much as 
the programmers were able to avoid conflicts themselves.</p>
<p>Accelerator does not have to be positioned at the start of a word, it
 can be put next to any letter or number. A reasonable order of choices 
would be: at the start of the most significant word in the message by 
default, then if it conflicts another message, at the start of another 
word, and if it still conflicts, inside one of the words.</p>
<p>The accelerator marker is usually chosen as one of the rarely used 
characters in normal text, but it may still appear in contexts in which 
it does not mark an accelerator. For example:</p>
<pre class="programlisting"><span class="nl">#: kspopupmenu.cpp:203</span>
<span class="nv">msgid</span> <span class="s">"Center &amp;&amp; Track"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="c1">#. Tag: phrase</span>
<span class="nl">#: config.docbook:137</span>
<span class="nv">msgid</span> <span class="s">"</span><span class="sx">&lt;phrase&gt;</span><span class="s">Configure &amp;kstars; Window</span><span class="sx">&lt;/phrase&gt;</span><span class="s">"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>In the first message, the accelerator marker has been used to escape 
itself, to produce a verbatim ampersand in output (similar as with 
escape sequences where double-backslash was used to represent a verbatim
 backslash). In the second message, the ampersand is used to insert an 
XML <span class="emphasis"><em>entity</em></span> <code class="literal">&amp;kstars;</code>.
 Only by context can it be concluded that the character is not used as 
accelerator marker, but after gaining little experience, the distinction
 will almost always be obvious to you.</p>
</div>
</div>
<div class="sect1">
<div class="titlepage">
<div>
<div>
<h2 class="title" style="clear: both"><a name="sec-poplurals" id="sec-poplurals"></a>2.4.&nbsp;Plural Forms</h2>
</div>
</div>
</div>
<p>Programs frequently need to report to the user the number of objects 
in a given context: "10 files found", "Do you really want to delete 5 
messages?" etc. Of, course, in English such messages should also have 
singular counterparts, like "1 file found", "...delete 1 message?". This
 means that two separate English texts are needed in the PO file, one 
for the singular and another the plural case. You could assume that 
these would then be two messages, like in this hypothetical example:</p>
<pre class="programlisting"><span class="nl">#: hypothetical.cpp:100</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"Time: %1 second"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: hypothetical.cpp:101</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"Time: %1 seconds"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
</pre>
<p>Here the program would use the first message when the number of objects is 1, and the second message for any other number.</p>
<p>However, while this also works for some languages other than English 
(e.g. Spanish, German, French), it does not work for all languages. The 
reason is that, while English needs one text for unity and another text 
for any other number, in many languages it is more complicated than 
that. For example, in some languages the singular form is used for all 
numbers <span class="emphasis"><em>ending</em></span> with the digit 1, 
so it would be wrong to use the singular form only for exactly 1. 
Furthermore, in some languages more than two texts are needed, for 
example three: one for all numbers ending in 1, the second for all 
numbers ending in 2, 3, 4, and the third for all other numbers.</p>
<p>To handle this diversity of plural forms, the PO format implements <span class="emphasis"><em>plural messages</em></span>. The example above in reality looks like this:</p>
<pre class="programlisting"><span class="nl">#: mainwindow.cpp:127</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"Time: %1 second"</span>
<span class="nv">msgid_plural</span> <span class="s">"Time: %1 seconds"</span>
<span class="nv">msgstr[</span><span class="mi">0</span><span class="nv">]</span> <span class="s">""</span>
<span class="nv">msgstr[</span><span class="mi">1</span><span class="nv">]</span> <span class="s">""</span>
</pre>
<p>The English singular form is given by the <code class="varname">msgid</code> string, and the plural form by the <code class="varname">msgid_plural</code> string. There are now several <code class="varname">msgstr</code>
 strings, with zero-based indices in square brackets, so that you can 
write as many translations as there are plural forms in your language. 
By default two <code class="varname">msgstr</code> strings will be 
given, but you may insert the line with the third one (index 2), and so 
on. For example, the Spanish language has same plural forms as English, 
and translation to it looks like this:</p>
<pre class="programlisting"><span class="nl">#: mainwindow.cpp:127</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"Time: %1 second"</span>
<span class="nv">msgid_plural</span> <span class="s">"Time: %1 seconds"</span>
<span class="nv">msgstr[</span><span class="mi">0</span><span class="nv">]</span> <span class="s">"Tiempo: %1 segundo"</span>
<span class="nv">msgstr[</span><span class="mi">1</span><span class="nv">]</span> <span class="s">"Tiempo: %1 segundos"</span>
</pre>
<p>while the Polish translation, which needs three plural forms, is:</p>
<pre class="programlisting"><span class="nl">#: mainwindow.cpp:127</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"Time: %1 second"</span>
<span class="nv">msgid_plural</span> <span class="s">"Time: %1 seconds"</span>
<span class="nv">msgstr[</span><span class="mi">0</span><span class="nv">]</span> <span class="s">"Czas: %1 sekunda"</span>
<span class="nv">msgstr[</span><span class="mi">1</span><span class="nv">]</span> <span class="s">"Czas: %1 sekundy"</span>
<span class="nv">msgstr[</span><span class="mi">2</span><span class="nv">]</span> <span class="s">"Czas: %1 sekund"</span>
</pre>
<p>But, how will the program know which plural form corresponds to which
 numbers? The specification for this is written within the PO file 
itself, in the file <span class="emphasis"><em>header</em></span> (PO headers will be <a class="link" href="http://pology.nedohodnik.net/doc/user/en_US/ch-poformat.html#sec-poheader" title="2.6.&nbsp;PO Header">explained later</a>).
 The specifiction consists of the number of plural forms which every 
plural message in the given PO file should have, and the computable 
logical expression which for any given number computes the index of the 
required plural form. This expression is quite cryptic to untrained eye,
 but you do not have to really understand how it works. Since it is 
constant for a given language, you can just copy it from any other 
translated PO file with plural forms, and by observing the plural 
messages in that other file, you will clearly see which form (by index 
of <code class="varname">msgstr</code>) is used in which situation. Bearing this in mind, just to complete the examples, here is the plural specification for Spanish:</p>
<pre class="programlisting">nplurals=2; plural=n != 1;
</pre>
<p>and for the more complicated Polish plural:</p>
<pre class="programlisting">nplurals=3; plural=(n==1 ? 0 : n%10&gt;=2 &amp;&amp; n%10&lt;=4 &amp;&amp; (n%100&lt;10 || n%100&gt;=20) ? 1 : 2);
</pre>
<p>The <code class="varname">nplurals</code> variable tells how many forms there are, and <code class="varname">plural</code> is the expression which computes the index of the <code class="varname">msgstr</code> string for the given number <code class="varname">n</code>. (If the syntax of the expression is familiar to you, that is because you know some C programming language).</p>
<p>Sometimes you will come upon a message, or a pair of messages, which 
are just like the hypothetical example above: having a number in it, but
 not presented as plural message, when you clearly see it should be. In 
most programming environments today, this simply means that the 
programmer forgot to use the plural message. Since this is considered a 
bug, you should inform the authors to replace the ordinary message with 
the plural message. In some environments, however, programs are not 
capable of using plurals, mostly when the PO format is used as 
intermediate (e.g. for OpenOffice programs). If that is the case, you 
can only try to translate the message in the "least bad" way.</p>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-pononum" id="sec-pononum"></a>2.4.1.&nbsp;Omitting The Number</h3>
</div>
</div>
</div>
<p>Quite frequently English singular form will omit the number, that is,
 only the plural form will contain the format directive for the number:</p>
<pre class="programlisting"><span class="nl">#: modes/typesdialog.cpp:425</span>
<span class="nd">#, kde-format</span>
<span class="nv">msgid</span> <span class="s">"Are you sure you want to delete this type?"</span>
<span class="nv">msgid_plural</span> <span class="s">"Are you sure you want to delete these %1 types?"</span>
<span class="nv">msgstr[</span><span class="mi">0</span><span class="nv">]</span> <span class="s">""</span>
<span class="nv">msgstr[</span><span class="mi">1</span><span class="nv">]</span> <span class="s">""</span>
</pre>
<p>It depends on the programming environment whether it is allowed to omit the number like this. For example, in KDE programs (<code class="literal">kde-format</code> flag) this is always possible, also in Gnome programs (<code class="literal">c-format</code>), but not in pure Qt programs (<code class="literal">qt-format</code>).
 If number omission is supported, in the translation you can either omit
 or retain the number in singular according to what is better for you 
language, and regardless of whether or not the number was omitted in the
 original. More precisely, you can omit the number in any plural form 
that is used for exactly one number. Conversely, if all forms are used 
for more than one number (e.g. the singular form is used for all numbers
 ending in digit 1), you cannot omit the number at all.</p>
<p>On rare occasions the plural message will have no number in the 
original, in either singular or plural. This happens when the programmer
 merely wanted to choose between the forms for "one" and "several", like
 this:</p>
<pre class="programlisting"><span class="nl">#: kgpg.cpp:498</span>
<span class="nv">msgid</span> <span class="s">"Decryption of this file failed:"</span>
<span class="nv">msgid_plural</span> <span class="s">"Decryption of these files failed:"</span>
<span class="nv">msgstr[</span><span class="mi">0</span><span class="nv">]</span> <span class="s">""</span>
<span class="nv">msgstr[</span><span class="mi">1</span><span class="nv">]</span> <span class="s">""</span>
</pre>
<p>In such cases, in translation you should just use the same plural 
text for all forms but the one which is used for unity (if there is any 
such).</p>
</div>
</div>
<div class="sect1">
<div class="titlepage">
<div>
<div>
<h2 class="title" style="clear: both"><a name="sec-pomerge" id="sec-pomerge"></a>2.5.&nbsp;Merging With Templates</h2>
</div>
</div>
</div>
<p>At one point you will have translated the complete PO file, every 
message in it, and sent it back to the source where it is used. As time 
passes, the original text at the source is going to change. Programs 
will get bugs fixed and new features implemented, which will require 
both new strings in the user interface, and modifications to some of the
 existing. Documentation will get new chapters, old chapters expanded, 
old paragraphs modified to better style. At some point, you will want to
 update your translation so that the source is again fully translated 
into your language.</p>
<p>This is done in the following way. On the one side, there is your 
last translated version of the PO file. On the other side, there is the 
latest pristine PO, with non-translated messages corresponding to the 
current state of the source. Pristine PO files are called <span class="emphasis"><em>templates</em></span>, and have the <code class="filename">.pot</code> extension instead of <code class="filename">.po</code>. The translated PO file and the template are then <span class="emphasis"><em>merged</em></span>
 in a special way, producing a new, partially translated PO for you to 
work on. The technicalities of merging are not so important at first, as
 in any established translation project you can just fetch the latest 
merged PO files. More important is what you can expect to see in a 
merged PO file.</p>
<p>In general, merged PO files contain four categories of messages. 
First are those messages which were present in the PO file when you last
 worked on it, in the sense of having unchanged <code class="varname">msgctxt</code> and <code class="varname">msgid</code> strings since then. As expected, their translations (<code class="varname">msgstr</code>
 strings) are as you made them, so there is nothing new for you to do 
about these messages. The second category are entirely new messages, 
added to the source in the meantime, which you should now translate. New
 messages are not added in an arbitrary way, for example simply appended
 to the end of the PO file. Instead they are be interspersed with 
translated messages, following the order of appearance of messages in 
the current source. This allows you to continue to infer contexts by 
preceding and following messages, same as you did when you were 
translating the PO from scratch. For example:</p>
<pre class="programlisting"><span class="nl">#: fitshistogram.cpp:347</span>
<span class="nv">msgid</span> <span class="s">"Auto Scale"</span>
<span class="nv">msgstr</span> <span class="s">""</span>
⁠
<span class="nl">#: fitshistogram.cpp:350</span>
<span class="nv">msgid</span> <span class="s">"Linear Scale"</span>
<span class="nv">msgstr</span> <span class="s">"linearna skala"</span>
⁠
<span class="nl">#: fitshistogram.cpp:353</span>
<span class="nv">msgid</span> <span class="s">"Logarithmic Scale"</span>
<span class="nv">msgstr</span> <span class="s">"logaritamska skala"</span>
</pre>
<p>The first message is a new one, untranslated, and the two other 
messages are old, translated earlier. From the old messages you can see 
that the new message is a new choice of scale (possibly for a diagram 
axis), and not, say, a command or option to change the size of something
 (as in "scale automatically").</p>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-pofuzzy" id="sec-pofuzzy"></a>2.5.1.&nbsp;Fuzzy Messages</h3>
</div>
</div>
</div>
<p>The most interesting is the third category of messages in a merged PO
 file. These are the old messages which were somewhat modified in the 
meantime, i.e. one or both of their <code class="varname">msgctxt</code> and <code class="varname">msgid</code>
 strings have changed. Or, this can also be a new message, but very 
similar to one of the old messages. There is actually no way to tell 
between the two, it is only by similarity to one of the old messages 
that a modified or new message falls into this category. Either way, 
such a message is called <span class="emphasis"><em>fuzzy</em></span>, and looks like this:</p>
<pre class="programlisting"><span class="nl">#: src/somwidget_impl.cpp:120</span>
<span class="nd">#, fuzzy</span>
<span class="c1">#| msgid "Elements with boiling point around this temperature:"</span>
<span class="nv">msgid</span> <span class="s">"Elements with melting point around this temperature:"</span>
<span class="nv">msgstr</span> <span class="s">"Elementi s tačkom ključanja u blizini ove temperature:"</span>
</pre>
<p>The <code class="literal">fuzzy</code> flag indicates that the message is fuzzy. The comment starting with <code class="literal">#|</code> is called the <span class="emphasis"><em>previous-string comment</em></span>. It contains the previous value of the <code class="varname">msgid</code> string, for which the translation in <code class="varname">msgstr</code> was made. This translation is, however, not valid for the <span class="emphasis"><em>current</em></span> (non-commented) <code class="varname">msgid</code> string. By comparing the previous and current <code class="varname">msgid</code>,
 you can see that the word "boiling" was replaced with "melting", and 
you can adjust the translation accordingly. Once you did that, to <span class="emphasis"><em>unfuzzy</em></span> the message you should remove the <code class="literal">fuzzy</code> flag and previous string comments (<code class="literal">#|</code>), so that the final updated message is:</p>
<pre class="programlisting"><span class="nl">#: src/somwidget_impl.cpp:120</span>
<span class="nv">msgid</span> <span class="s">"Elements with melting point around this temperature:"</span>
<span class="nv">msgstr</span> <span class="s">"Elementi s tačkom topljenja u blizini ove temperature:"</span>
</pre>
<p>Previous-string comments are still somewhat fresh addition to the PO 
format, which means that in some translation environments you will not 
have them in merged POs. The fuzzy message is then presented only with 
the <code class="literal">fuzzy</code> flag:</p>
<pre class="programlisting"><span class="nl">#: src/somwidget_impl.cpp:120</span>
<span class="nd">#, fuzzy</span>
<span class="nv">msgid</span> <span class="s">"Elements with melting point around this temperature:"</span>
<span class="nv">msgstr</span> <span class="s">"Elementi s tačkom ključanja u blizini ove temperature:"</span>
</pre>
<p>It may seem that this is no great loss: so long as you are visually 
comparing texts, instead of comparing the previous (here missing) and 
current <code class="varname">msgid</code>, you might as well compare the current <code class="varname">msgid</code> and the old translation in <code class="varname">msgstr</code>,
 and adjust translation based on that. However, there are two 
disadvantages to this. Less importantly, it may not always be easy to 
spot a difference by comparing the new original and the old translation.
 For example, only a typo or some punctuation may have been fixed in the
 original, leaving you to wonder if you are missing something. More 
importantly, a dedicated PO editor can use the previous and current <code class="varname">msgid</code>
 to highlight differences between them, which makes it that much easier 
to see what has changed. Even if you are working with an ordinary text 
editor, there are command-line tools which can embed differences into 
previous <code class="varname">msgid</code>, again making them easier to
 spot. And the bigger the message, the more important to have automatic 
highlighting--think of a long paragraph where only one word has been 
changed. For these reasons, if the merged PO files you work on do not 
have previous-string comments, do inquire with authors if they can 
enable them (they may simply not know about this possibility, as it is 
not the default behavior on merging).</p>
<p>Other than <code class="varname">msgid</code>, the <code class="varname">msgctxt</code> string can also have the corresponding previous-string comment. Regardless of whether one or both of the <code class="varname">msgctxt</code> and <code class="varname">msgid</code> have been changed, both will be given in previous-string comments:</p>
<pre class="programlisting"><span class="nl">#: kstarsinit.cpp:451</span>
<span class="nd">#, fuzzy</span>
<span class="c1">#| msgctxt "Constellation Line"</span>
<span class="c1">#| msgid "Constell. Line"</span>
<span class="nv">msgctxt</span> <span class="s">"Toggle Constellation Lines in the display"</span>
<span class="nv">msgid</span> <span class="s">"Const. Lines"</span>
<span class="nv">msgstr</span> <span class="s">"Linija sazvežđa"</span>
</pre>
<p>In particular, a message will be fuzzied if it previously had no <code class="varname">msgctxt</code> and got one after merging, or had one and lost it. In the first case, the previous-string comments will contain only the <code class="varname">msgid</code>,
 although it may be the same as the current one; by this you will know 
that the change was only the adding of context. In the second case, the 
previous-string comments will contain both the <code class="varname">msgctxt</code> and the <code class="varname">msgid</code> strings, while there will be no current <code class="varname">msgctxt</code>. Here are two examples:</p>
<pre class="programlisting"><span class="nl">#: kstarsinit.cpp:444</span>
<span class="nd">#, fuzzy</span>
<span class="c1">#| msgid "Solar System"</span>
<span class="nv">msgctxt</span> <span class="s">"Toggle Solar System objects in the display"</span>
<span class="nv">msgid</span> <span class="s">"Solar System"</span>
<span class="nv">msgstr</span> <span class="s">"Sunčev sistem"</span>
⁠
<span class="nl">#: finddialog.cpp:102</span>
<span class="nd">#, fuzzy</span>
<span class="c1">#| msgctxt "object name (optional)"</span>
<span class="c1">#| msgid "Andromeda Galaxy"</span>
<span class="nv">msgid</span> <span class="s">"Andromeda Galaxy"</span>
<span class="nv">msgstr</span> <span class="s">"Andromeda, galaksija"</span>
</pre>
<p>It is important for a message to become fuzzy when only the 
disambiguating context is added or removed, because this has been done 
precisely to shed some light on the original text, which may require 
modifying the translation.</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-pofuzztr" id="sec-pofuzztr"></a>2.5.2.&nbsp;Treatment of Fuzzy Messages</h3>
</div>
</div>
</div>
<p>Fuzzy messages are a special category only from translator's 
viewpoint. Consumers of PO files (programs, etc.) will treat them as 
ordinary untranslated messages, i.e. they will use the original instead 
of the old translation. This is necessary, as there is no telling how 
inappropriate the old translation may be for the current original. The 
algorithm that produces fuzzy messages will sometimes turn out rather 
strange pairings, which to you or to the user may not look similar at 
all.</p>
<p>It is important to keep in mind that fuzzy messages are treated as 
untranslated. Fresh translators will sometimes manually add the <code class="literal">fuzzy</code>
 flag to a message to mark they are not entirely sure that the 
translation is proper, not knowing that this will totally exclude the 
translation from being used. Thus, you should manually add the <code class="literal">fuzzy</code>
 flag only when you are so unsure of the meaning of the message, that 
you explicitly want to prevent the translation from being used. This is 
fairly rarely needed. Instead, when you just want to mark the message so
 that you or someone else can check it later, you should write your 
doubts in a <a class="link" href="http://pology.nedohodnik.net/doc/user/en_US/ch-poformat.html#sec-pomancmnt" title="2.2.3.&nbsp;Translator Comments">translator comment</a>.</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-poobsol" id="sec-poobsol"></a>2.5.3.&nbsp;Obsolete Messages</h3>
</div>
</div>
</div>
<p>The last, fourth category are <span class="emphasis"><em>obsolete</em></span>
 messages, the messages which are not present in the source any more. 
All obsolete messages are grouped at the end of the merged PO file, and 
fully commented out by the <code class="literal">#~</code> comment:</p>
<pre class="programlisting"><span class="c1">#~ msgid "Set the telescope longitude and latitude."</span>
<span class="c1">#~ msgstr "Postavi geo. dužinu i širinu teleskopa."</span>
</pre>
<p>Obsolete messages have no extracted comments or source references, as
 they are no longer present in the source. Translator comments and flags
 are retained, as they don't depend on the presence in the source.</p>
<p>It could be said that obsolete messages are in fact no messages at 
all, given that they do not exist from the point of consumers of the PO 
file, and there is nothing for translators to do with them. PO tools in 
general will ignore them, except to preserve them when the PO file is 
modified. Dedicated PO editors will invariably not show obsolete 
messages to the translator, and may provide an option to automatically 
remove them from the file on saving.</p>
<p>What is then the purpose of obsolete messages? It frequently happens 
that a section of the source content, e.g. the code around a certain 
feature of a program, is <span class="emphasis"><em>temporarily</em></span>
 removed. Authors sometimes want to improve a section of the text 
separately, outside of the main content which is being translated, and 
sometimes a section is even briefly omitted by mistake when there are 
moves and renames in the source. When this happens, the affected 
messages will become obsolete in the merged PO; but, when the missing 
section is put back into the source, the merging algorithm will take 
obsolete messages into account, and promote them to real messages 
(either translated or fuzzy) where possible. Thus, some previous 
translation work may be saved.</p>
<p>What you should do with obsolete messages depends on the tools with 
which you work on PO files. For example, if you and other translators 
working on the given PO all use dedicated PO editors with internal 
storage of all previously encountered translations, the <span class="emphasis"><em>translation memory</em></span><a href="#ftn.idp52766080" class="footnote" name="idp52766080" id="idp52766080"><sup class="footnote">[7]</sup></a>,
 there is less need for keeping obsolete messages around, as the editor 
will be able to fill new messages from the memory; but there are some 
difficulties, as the need for translators to share the same memory. In 
practice, many translators choose to keep obsolete messages around for 
some time, and periodically (e.g. months apart) remove them from PO 
files. By this they achieve that accidental removals of source content, 
which are quickly corrected, do not bother them, while avoiding 
accretion of far too much obsolete material.</p>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-ponewfile" id="sec-ponewfile"></a>2.5.4.&nbsp;Starting a New PO file</h3>
</div>
</div>
</div>
<p>In light of the translation maintenance through the process of 
merging with templates, you can think of starting to work on a 
never-before translated PO file as just the "initial merging": you will 
have to take the template and rename it to something with the <code class="varname">.po</code>
 extension, and work from there on. What you rename it to depends on the
 environment, but it is usually one of two things: either the same name 
as that of the template but with the <code class="varname">.po</code> extension (like in KDE), or your language code with the <code class="varname">.po</code> extension (like in Gnome). This basically depends on the organization of the particular translation project.</p>
<p>On the other hand, sometimes for each template in the project an 
empty PO for your language will have been created and put in a proper 
place in the source tree, so that you can just start translating it when
 you get to it.</p>
<p>At any rate, when you start working on a PO file from scratch, the first thing you should do is fill out its <a class="link" href="http://pology.nedohodnik.net/doc/user/en_US/ch-poformat.html#sec-poheader" title="2.6.&nbsp;PO Header">header</a>.</p>
</div>
</div>
<div class="sect1">
<div class="titlepage">
<div>
<div>
<h2 class="title" style="clear: both"><a name="sec-poheader" id="sec-poheader"></a>2.6.&nbsp;PO Header</h2>
</div>
</div>
</div>
<p>The very first message in each PO file is not a real message, but the <span class="emphasis"><em>header</em></span>,
 which provides administrative and technical pieces of information about
 the PO file. Here is one pristine header, before any translation on the
 PO file has been done:</p>
<pre class="programlisting"><span class="c1"># SOME DESCRIPTIVE TITLE.</span>
<span class="c1"># Copyright (C) YEAR This_file_is_part_of_KDE</span>
<span class="c1"># This file is distributed under the same license as the PACKAGE package.</span>
<span class="c1"># FIRST AUTHOR &lt;EMAIL@ADDRESS&gt;, YEAR.</span>
<span class="c1">#</span>
<span class="nd">#, fuzzy</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="nv">msgstr</span> <span class="s">""</span>
<span class="s">"Project-Id-Version: PACKAGE VERSION</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Report-Msgid-Bugs-To: http://bugs.kde.org</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"POT-Creation-Date: 2008-09-03 10:09+0200</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"PO-Revision-Date: YEAR-MO-DA HO:MI+ZONE</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Last-Translator: FULL NAME </span><span class="sx">&lt;EMAIL@ADDRESS&gt;</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Language-Team: LANGUAGE </span><span class="sx">&lt;kde-i18n-doc@kde.org&gt;</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"MIME-Version: 1.0</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Content-Type: text/plain; charset=UTF-8</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Content-Transfer-Encoding: 8bit</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Plural-Forms: nplurals=INTEGER; plural=EXPRESSION;</span><span class="se">\n</span><span class="s">"</span>
</pre>
<p>The header consists of introductory comments, followed by the empty <code class="varname">msgid</code>, and by the <code class="varname">msgstr</code> which contains <span class="emphasis"><em>header fields</em></span>. The header comments, similar to those of normal messages, are not entirely free form, but have some structure to them. The <code class="varname">msgstr</code> is divided by newlines (<code class="literal">\n</code>) into fields of <code class="literal"><em class="replaceable"><code>name</code></em>: <em class="replaceable"><code>value</code></em></code>
 form (the name of the piece of information and the information itself).
 Although the header is pristine, some of the environment-dependent 
values are typically already supplied, e.g. wherever the KDE is 
mentioned in this example. The <code class="literal">fuzzy</code> flag 
indicates that the PO file has not been translated earlier. 
All-uppercase text segments are placeholders which you should replace 
with real values.</p>
<p>The header updated to reflect the translation state could look like this:</p>
<pre class="programlisting"><span class="c1"># Translation of kstars.po into Spanish.</span>
<span class="c1"># This file is distributed under the same license as the kdeedu package.</span>
<span class="c1"># Pablo de Vicente &lt;pablo@foo.com&gt;, 2005, 2006, 2007, 2008.</span>
<span class="c1"># Eloy Cuadra &lt;eloy@bar.net&gt;, 2007, 2008.</span>
<span class="nv">msgid</span> <span class="s">""</span>
<span class="nv">msgstr</span> <span class="s">""</span>
<span class="s">"Project-Id-Version: kstars</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Report-Msgid-Bugs-To: http://bugs.kde.org</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"POT-Creation-Date: 2008-09-01 09:37+0200</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"PO-Revision-Date: 2008-07-22 18:13+0200</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Last-Translator: Eloy Cuadra </span><span class="sx">&lt;eloy@bar.net&gt;</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Language-Team: Spanish </span><span class="sx">&lt;kde-l10n-es@kde.org&gt;</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"MIME-Version: 1.0</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Content-Type: text/plain; charset=UTF-8</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Content-Transfer-Encoding: 8bit</span><span class="se">\n</span><span class="s">"</span>
<span class="s">"Plural-Forms: nplurals=2; plural=n != 1;</span><span class="se">\n</span><span class="s">"</span>
</pre>
<p>Even if this particular header has been slightly abridged for 
clarity, it probably still looks menacing, with a lot of data. Are you 
supposed to manually get <span class="emphasis"><em>all</em></span> that
 correct? Not really. If you are using a dedicated PO editor, it will 
have a comfortable configuration dialog where you can enter data about 
yourself, your language, and so on, and whenever you save a PO file, the
 editor will automatically fill out the header. If you are using a plain
 text editor, there are command line tools to similarly fill out the 
header automatically. But even with such aids, it is useful to give a 
few general directions about header comments and fields.</p>
<p>The first comment line usually has the title role, saying something 
about what is translated and into which language. The second comment 
tells something about licensing. The following comments each list a 
translator who at one time worked on this particular PO file, his name, 
email address, and years of contribution. After that, any freeform 
comments may be added. The <code class="literal">fuzzy</code> flag is removed once the work on the PO file is started.</p>
<p>The <code class="literal">Project-Id-Version</code> header field states the name and possibly version of what is translated, <code class="literal">Report-Msgid-Bugs-To</code> gives address to write to when you discover problems in original text, <code class="literal">POT-Creation-Date</code> the time when the PO template was created, <code class="literal">PO-Revision-Date</code> the time when the PO file was last edited by a translator, <code class="literal">Last-Translator</code> the name and address of last translator who worked on the file, and <code class="literal">Language-Team</code> the name and address of the translation team (if any) which the last translator is part of. The fields <code class="literal">MIME-Version</code>, <code class="literal">Content-Type</code>, and <code class="literal">Content-Transfer-Encoding</code>,
 are pretty much always and for any language as given above, so they are
 not interesting (though you could change encoding to something else 
than UTF-8, in this day and age really think thrice before doing that). 
The final field, <code class="literal">Plural-Forms</code>, is where you write the plural specification for your language (as explained in the section on <a class="link" href="http://pology.nedohodnik.net/doc/user/en_US/ch-poformat.html#sec-poplurals" title="2.4.&nbsp;Plural Forms">plural forms</a>).</p>
<p>Of the presented comments and fields, almost all of them are set when
 the PO file is translated for the first time. When you come back to a 
certain PO to update the translation, if no one else worked on that PO 
in the meantime, you should only update the <code class="literal">PO-Revision-Date</code> field. If someone has worked on it, you will also have to put your data in <code class="literal">Last-Translator</code>
 field. If you get to work on a PO file for the first time after someone
 else has already worked on it, you should add yourself in the 
translator list in comments. If you are using a dedicated PO editor, it 
will perform all these updates for you whenever you save the file.</p>
<p>Note that everything in the header is supposed to be in English, to 
be understandable to people who do not speak your language. Aside from 
comments in English, this also means that the name of the language and 
the language team should be in English, and your own name and names of 
other translators in their romanized equivalents. This is because, for 
example, people speaking other languages may need to contact you or your
 team about any technical problems in the translation (e.g. program 
maintainers). Keep this in mind also when you are setting up your data 
in a dedicated PO editor.</p>
<p>Other than the standard header fields, you may encounter some custom fields, whose names begin with <code class="literal">X-</code>. These fields are added by various PO processing tools. One typical custom field is <code class="literal">X-Generator</code>, where the dedicated PO editor which you use will write its name and version. Another custom field sometimes seen is <code class="literal">X-Accelerator-Marker</code>, which states the character used as the <a class="link" href="http://pology.nedohodnik.net/doc/user/en_US/ch-poformat.html#sec-poaccel" title="2.3.4.&nbsp;Accelerators">accelerator marker</a>
 (recognized by some tools e.g. for searching through PO files, when 
otherwise the accelerator marker could "mask" a word by being in the 
middle of it). Different translation environments may add various 
environment-specific fields for their internal use.</p>
</div>
<div class="sect1">
<div class="titlepage">
<div>
<div>
<h2 class="title" style="clear: both"><a name="sec-poedrepr" id="sec-poedrepr"></a>2.7.&nbsp;Representation in Editors</h2>
</div>
</div>
</div>
<p>When you translate PO files using a plain text editor, all the 
message elements will be displayed in it as we have seen in the examples
 so far. You can edit them at will, including invalidating the syntax if
 you are not careful. Most capable text editors nowdays have syntax 
highlighting for the PO format, albeit with different levels of 
specificity. If you are working with a plain text editor, you should 
definitely use a command line tool to check the basic correctness of the
 PO file. <span class="command"><strong>msgfmt</strong></span> from the Gettext package is one such tool (use it with the <code class="option">-c</code>).</p>
<p>Dedicated PO editors will provide you with much more automation, but 
each will have its own ways of presenting and means of editing different
 elements of a message. As this text has tried to convince you, every 
element of the PO message is potentially important, so you should take 
time to find out how and where the given PO editor shows them. Some 
editors may even not show all elements of the messages, which in the 
opinion of the author of this text reflects poorly on them. At the 
extreme end, immediatelly discard an editor which shows you only the 
original text (the <code class="varname">msgid</code> string), 
regardless of any other qualities it may have (this is typical of 
translation editors not developed around the PO format, but later 
upgraded to "support" it).</p>
<p>Here is the summary of PO message elements, as a checklist of what to look for in a PO editor:</p>
<div class="itemizedlist">
<ul class="itemizedlist" style="list-style-type: disc;">
<li class="listitem">
<p><code class="varname">msgid</code> string (original text)</p>
</li>
<li class="listitem">
<p><code class="varname">msgstr</code> string (translated text)</p>
</li>
<li class="listitem">
<p><code class="varname">msgctxt</code> string (disambiguating context)</p>
</li>
<li class="listitem">
<p>extracted comments (context in comment)</p>
</li>
<li class="listitem">
<p>source references (source file and line of the message)</p>
</li>
<li class="listitem">
<p>flags (<code class="literal">fuzzy</code>, <code class="literal">*-format</code>, etc.)</p>
</li>
<li class="listitem">
<p>fuzzy state (although among flags, requires special attention)</p>
</li>
<li class="listitem">
<p>previous strings (previous <code class="varname">msgctxt</code> and <code class="varname">msgid</code> strings in fuzzy messages)</p>
</li>
<li class="listitem">
<p>translator comments (added by translators, therefore they should be editable as well)</p>
</li>
<li class="listitem">
<p>positional context (good view of preceding and following messages)</p>
</li>
</ul>
</div>
<div class="sect2">
<div class="titlepage">
<div>
<div>
<h3 class="title"><a name="sec-poedlist" id="sec-poedlist"></a>2.7.1.&nbsp;List of PO Editors</h3>
</div>
</div>
</div>
<p>There is a number of dedicated PO editors available. They all have 
the same good basic support for the PO format, but each has some 
specialities and quirks that reflect the background of their authors. 
Namely, dedicated PO editors are normally written and maintained by 
people who are themselves engaged in certain translation projects. You 
should therefore try out the available editors and choose the one which 
is best suited to you, and possibly to the translation project within 
which you translate. Here is the list of some dedicated PO editors:</p>
<div class="variablelist">
<dl class="variablelist">
<dt><span class="term"><a class="ulink" href="http://projects.gnome.org/gtranslator/" target="_top">Gtranslator</a></span></dt>
<dd>
<p>PO editor developed within the Gnome translation project.</p>
</dd>
<dt><span class="term"><a class="ulink" href="http://userbase.kde.org/Lokalize" target="_top">Lokalize</a></span></dt>
<dd>
<p>Computer-aided translation tool developed within the KDE translation project.</p>
</dd>
<dt><span class="term"><a class="ulink" href="http://www.poedit.net/" target="_top">Poedit</a></span></dt>
<dd>
<p>Cross-platform, lightweight PO editor.</p>
</dd>
<dt><span class="term"><a class="ulink" href="http://translate.sourceforge.net/wiki/virtaal/index" target="_top">Virtaal</a></span></dt>
<dd>
<p>Translation editor designed to be visually compact and easy to use, yet powerfull.</p>
</dd>
</dl>
</div>
<p>Some plain text editors can operate in <span class="emphasis"><em>modes</em></span>,
 where additional editing commands became available to the user when a 
file of certain type is opened. Such mode for PO files is available for 
the following text editors: <a class="ulink" href="http://www.gnu.org/software/emacs/" target="_top">Emacs</a>, <a class="ulink" href="http://projects.gnome.org/gedit/" target="_top">Gedit</a>, <a class="ulink" href="http://www.vim.org/" target="_top">Vim</a>.</p>
</div>
</div>
<div class="footnotes"><br>
<hr style="width:100; text-align:left;margin-left: 0">
<div id="ftn.idp54108592" class="footnote">
<p><a href="#idp54108592" class="para"><sup class="para">[3]</sup></a> 
You may want to point to a message when consulting with fellow 
translators, or when reporting a typo or another problem in the original
 text to the authors.</p>
</div>
<div id="ftn.idp52577568" class="footnote">
<p><a href="#idp52577568" class="para"><sup class="para">[4]</sup></a> If the <code class="varname">msgctxt</code> is present but empty, i.e. <code class="literal">msgctxt ""</code>, this is actually different than the <code class="varname">msgctxt</code> not being present at all. Hence the term "null-valued" as opposed to simply "empty".</p>
</div>
<div id="ftn.idp52583712" class="footnote">
<p><a href="#idp52583712" class="para"><sup class="para">[5]</sup></a> 
Programmers of free software are frequently aware of this latent 
necessity, and readily reachable, so you should be able to make the 
request with little communication overhead.</p>
</div>
<div id="ftn.idp52648768" class="footnote">
<p><a href="#idp52648768" class="para"><sup class="para">[6]</sup></a> CJK is the usual acronym for ideographical east-Asian languages, the Chinese, Japanese, and Korean.</p>
</div>
<div id="ftn.idp52766080" class="footnote">
<p><a href="#idp52766080" class="para"><sup class="para">[7]</sup></a> 
Translation memory is an extremely important topic on its own when the 
translation is not done using the PO format. With PO files and the 
concept of merging with templates, translation memories are not of such 
great importance, but can come in handy.</p>
</div>
</div>
</div>
<div class="navfooter">
<hr>
<table summary="Navigation footer" width="100%">
<tbody><tr>
<td width="40%" align="left"><a accesskey="p" href="http://pology.nedohodnik.net/doc/user/en_US/ch-about.html">Prev</a>&nbsp;</td>
<td width="20%" align="center">&nbsp;</td>
<td width="40%" align="right">&nbsp;<a accesskey="n" href="http://pology.nedohodnik.net/doc/user/en_US/ch-sieve.html">Next</a></td>
</tr>
<tr>
<td width="40%" valign="top" align="left">Chapter&nbsp;1.&nbsp;A Study of PO&nbsp;</td>
<td width="20%" align="center"><a accesskey="h" href="http://pology.nedohodnik.net/doc/user/en_US/index.html">Home</a></td>
<td width="40%" valign="top" align="right">&nbsp;Chapter&nbsp;3.&nbsp;Sieving</td>
</tr>
</tbody></table>
</div>


</body></html>

