---
layout: post
title: SPARK Ada programming language
date: 2014-04-10 10:35:38.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Ada
- SPARK
meta:
  _edit_last: '1'
  layout: default
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  _syntaxhighlighter_encoded: '1'
  dsq_thread_id: '2601598704'
  feature_size: blank
  builder_switch_frontend: '0'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/spark-ada-programming-language/"
---
<p>Before I joined <a href="http://santoslab.org">SAnToS Lab</a>, I heard about Ada programming language only a few times. I thought it is an ancient language, that nobody is using anymore. I assumed, that only reason why somebody may bother are some legacy applications written 30 years ago. I thought that safety-critical and high-assurance systems are developed in C/C++ or even Assembly language.</p>
<p>I was wrong.</p>
<h3>Ada programming language</h3>
<p>First version of Ada programming language - Ada 83 - was designed to meet the US Department of Defence Requirements formalized in <a href="http://www.adahome.com/History/Steelman/steelman.htm">"Steelman" document</a>. Since that time, Ada evolved. There were Ada 95, Ada 2005 and <a href="http://www.ada2012.org">Ada 2012</a> (released in December 10, 2012). Ada is activelly used in many <a href="http://www.seas.gwu.edu/~mfeldman/ada-project-summary.html">Real-World projects</a>, e.g. Aviation (<a href="http://archive.adaic.com/projects/atwork/boeing.html">Boeing 777's Software is written in Ada</a>), Railway Transportation, Commercial Rockets, Satellites and even Banking. One of the main goals of Ada is to ensure software correctness and safety. The picture below, shows what is the goal of Ada: prevent the Developer from introducing bugs into system by rich tooling and language properties.</p>
<p><img class="aligncenter size-large wp-image-1199" src="{{ site.baseurl }}/assets/2014/04/developer_responsibility_in_ada-785x541.png" alt="Ada responsibilities" width="785" height="541" /></p>
<p>Ada does not use curly braces. The code listing below shows "Hello, World" in Ada:</p>
{% highlight ada %}
with Ada.Text_IO; 
use Ada.Text_IO;

procedure Hello is 
begin   
  Put_Line ("Hello, world!"); 
end Hello;
{% endhighlight %}
<h4>Basic constructs</h4>
<p>The table below, shows C# code, and equivalent Ada code.</p>
<table class="code_cmp" style="margin-bottom: 20px;">
<tbody>
<tr>
<th>C#</th>
<th>Ada</th>
</tr>
<tr>
<td>
{% highlight csharp %}
x = 5;
{% endhighlight %}
</td>
<td>
{% highlight ada %}
x := 5;
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
x == 5
{% endhighlight %}
</td>
<td>
{% highlight ada %}
x = 5
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
x != 5
{% endhighlight %}
</td>
<td>
{% highlight ada %}
x /= 5
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
// comment
{% endhighlight %}
</td>
<td>
{% highlight ada %}
-- comment
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
int i = 2;
Console.WriteLine(i);
{% endhighlight %}
</td>
<td>
{% highlight ada %}
i : Integer := 2;
Put_Line(Integer'Image(i));
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
if (a &gt; b)  
{
  Console.WriteLine("Condition met");  
}  
else  
{
  Console.WriteLine("Condition not met");
}
{% endhighlight %}
</td>
<td>
{% highlight ada %}
if a &gt; b then   
 Put_Line("Condition met");
else   
 Put_Line("Condition not met"); 
end if;
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
switch(i) 
{
  case 0:     
    Console.WriteLine("zero");     
    break;   
  case 1:
    Console.WriteLine("one");     
    break;
  case 2:     
    Console.WriteLine("two");     
    break;   
  default:     
    Console.WriteLine("none");     
}{% endhighlight %}
</td>
<td>
{% highlight ada %}
case i is   
  when 0 =&gt; Put_Line("zero");   
  when 1 =&gt; Put_Line("one");   
  when 2 =&gt; Put_Line("two");   
  when others =&gt; Put_Line("none");
end case;
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
for (int i=1; i&lt;=10; ++i)  
{
  Console.WriteLine("Iteration: ");   
  Console.WriteLine(i);   
  Console.WriteLine("");  
}
{% endhighlight %}
</td>
<td>
{% highlight ada %}
for i in 1 .. 10 loop
  Put_Line("Iteration: ");   
  Put_Line(Integer'Image(i));
  Put_Line("");
end loop;
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
while(a != b)  
{
  Console.WriteLine("Waiting"); 
}
{% endhighlight %}
</td>
<td>
{% highlight ada %}
while a /= b loop   
  Put_Line("Waiting"); 
end loop;
{% endhighlight %}
</td>
</tr>
<tr>
<td>
{% highlight csharp %}
do 
{
  a++;    
} 
while(a!=10);{% endhighlight %}
</td>
<td>
{% highlight csharp %}
loop   
  a := a + 1;   
  exit when a = 10; 
end loop;
{% endhighlight %}
</td>
</tr>
</tbody>
</table>
<h4>Packages</h4>
<p>The equivalent for C# class - in Ada - is package. It has two files: specification (.ads file) and body (.adb file). It is like header (.h) and implementation (.cpp) files for class definition in C++. Additionally:</p>
<ul>
<li>class variables in C# conforms to 'global' variables in Ada package (the name 'global' in Ada package means that variable is visible for entire package, not entire application like in C/C++)</li>
<li>C# class have methods, which returns value or not (<code>void</code>). In Ada, methods are called subprograms. There are two distinguished types of them: functions (returns something) and procedures (does not return anything).</li>
</ul>
<p>Here is sample C# class:</p>
{% highlight csharp %}
class Person  
{
  public int publicVar;

  private int privateVar;

  void MyMethod(int param)
  {
    // do stuff
  }

  public int MultiplyBy(int param) 	
  {
    return param * 2
  }
}
{% endhighlight %}
<p>And its equivalent package in Ada:</p>
{% highlight ada %}
-- person.ads
package Person is
  publicVar : Integer; 	

  procedure MyMethod(Param : Integer);   
   
  function MultiplyBy(Param : Integer) return Integer; 
end Person;
{% endhighlight %}

{% highlight ada %}
-- person.adb
package body Person is 	
  privateVar : Integer;

  procedure MyMethod(Param : Integer)
  is
  begin
    -- do stuff
  end;

  function MultiplyBy(Param : Integer)
  is
    Result : Integer;
  begin
    Result := Param * 2;
    return Result;
  end;
end Person;
{% endhighlight %}
<h3>SPARK Ada</h3>
<p><a href="http://en.wikipedia.org/wiki/SPARK_(programming_language)">SPARK programming language</a> is based on Ada. Thus, it is usually referred as "SPARK Ada".</p>
<p>SPARK is a programming language and static verification technology designed specifically for the development of high integrity software. First version was designed over 20 years ago. SPARK excludes some Ada constructs (i.e. pointers, dynamic memory allocation or recursion) to make static analysis feasible. Additionally SPARK contains tool-set for Software Verification:</p>
<ul>
<li>Examiner - analyze code and ensures that it conforms to the SPARK language; also verify program to some extent using Verification Conditions (e.g. array index out of range, type range violation, division by zero, numerical overflow etc.)</li>
<li>Simplifier - simplify Verification Conditions generated by Examiner</li>
<li>Proof Checker - prove the Verification Conditions</li>
</ul>
<p>Using SPARK, a developer takes a <a href="http://en.wikipedia.org/wiki/Z_notation">Z specification</a> and performs a stepwise refinement from the specification to SPARK code. For each refinement step a tool is used to produce verification conditions (VC's), which are mathematical theorems. If the VC's can be proved then the refinement step will be known to be valid. However if the VC's cannot be proved then the refinement step may be erroneous.</p>
<p>First version of SPARK (SPARK 83) was based on Ada 83. The second version (SPARK 95) - on Ada 95. Current version - SPARK 2005 - is based on Ada 2005. It is a subset of Ada 2005 with annotations. The annotation language support flow analysis and formal verification. Annotations are encoded in Ada comments (via the prefix <code>--#</code>). It makes every SPARK 2005 program, valid Ada 2005 program. Code listing below shows example SPARK 2005 package specification.</p>
{% highlight ada %}
package Odometer
--# own Trip, Total : Integer;
is
	procedure Zero_Trip;
	--# global out Trip;
	--# derives Trip from ;
	--# post Trip = 0;

	function Read_Trip return Integer;
	--# global in Trip;

	function Read_Total return Integer;
	--# global in Total;

	procedure Inc;
	--# global in out Trip, Total;
	--# derives Trip from Trip &amp; Total from Total;
	--# post Trip = Trip~ + 1 and Total = Total~ + 1;

end Odometer;{% endhighlight %}
<p>It is an interface for simple Odometer. There are 4 subprograms (2 procedures and 2 functions):</p>
<ul>
<li><code>Zero_Trip</code> procedure - reset Odometer to 0</li>
<li><code>Read_Trip</code> function - returns current distance</li>
<li><code>Read_Total</code> function - returns total distance traveled</li>
<li><code>Inc</code> procedure- increment total and current distance by 1</li>
</ul>
<p>Annotation <code>global</code> means that subprogram uses some global variable. Postfix <code>in</code>, <code>out</code> or <code>in out</code> means that particular variable is read, write or read and write respectively. Annotation <code>derives</code> says that some variable value depends on other variables. E.g. in procedure <code>Inc</code> variable <code>Trip</code> is dependent on its current value (before procedure call). Annotations <code>pre</code> and <code>post</code> define pre- and postconditions of procedure (only <code>post</code> is present in above example). We can see, that in <code>Zero_Trip</code> procedure postcondition requires that variable <code>Trip</code> is equal to 0. In procedure <code>Inc</code>, postconditions requires that variables <code>Trip</code> and <code>Total</code> are incremented by 1 ('<code>~</code>' is the value of variable before procedure call). Annotation <code>own</code> expose private variables for use in public methods specification.</p>
<p>We can see, that SPARK contracts describe the functionality of particular subprograms. It is like documentation. You can find more about SPARK contracts in <a href="http://www.adacore.com/sparkpro/tokeneer/discovery/">Tokeneer Discovery tutorial</a> and <a href="http://docs.adacore.com/spark2014-docs/html/lrm/mapping-spec.html">SPARK 2005 to SPARK 2014 Mapping Specification</a>.</p>
<p>The most popular IDE for SPARK Ada development is <a href="http://libre.adacore.com/tools/gps/">GNAT Programming Studio</a>. There is also Eclipse plugin <a href="http://libre.adacore.com/tools/gnatbench/">GNATbench</a>.</p>
<p>The next version, SPARK 2014 (based on Ada 2012) is under development. There is partial tool support (in GNAT Programming Studio), but some language features are still not supported. It is worth to mention, that Ada 2012 contains code contracts. Thus SPARK 2014 is just subset of Ada 2012. There are no additional constructs like annotations in SPARK 2005, because now, contracts are part of the language.</p>
<p>In real-world applications, the embedded critical components are written in SPARK while the non-critical components are written in Ada.</p>
<h3>Summary</h3>
<p>I am working with SPARK Ada for more than 1 year. My (beginner) thoughts are as follows:</p>
<ul>
<li>I don't like the syntax. It is not developer friendly. You need to do a lot of repetitions, of the same code (e.g. subprograms declaration/definition). Syntax is very verbose, e.g. code blocks starts with <code>begin</code> and ends with <code>end</code> keywords. It means more writing than in case when you use 'curly braces' for that.</li>
<li>It is very hard to create valid and working SPARK program. There are many rules and limitations (e.g. no dynamic allocation).</li>
<li>Quite steep learning curve. Additionally, it is not easy to find some resources like tutorials, books, videos.</li>
<li>SPARK Ada IDE - GNAT Programming Studio - is very specific, and different than the most popular IDEs (e.g. Visual Studio or Eclipse). It is also less powerful, in case of e.g. intellisense, key shortcuts or project manipulations.</li>
</ul>
<p>From my perspective, SPARK is a temporary subset of Ada, chosen for software verification. Once, verification techniques evolves, more features of Ada are getting included in SPARK. Maybe, in some day, there will be no SPARK, but just Ada, and tools will be able to verify (reason about) all its features.</p>
<p>More about Ada you can find at <a href="http://en.wikibooks.org/wiki/Ada_Programming">Ada Programming</a> at Wikibooks, <a href="http://university.adacore.com/">AdaCore University</a> (video tutorials) and at <a href="http://www.ada2012.org/">ada2012.org</a> website. Good place to start getting familiar with SPARK is <a href="http://www.adacore.com/sparkpro/tokeneer/discovery/">Tokeneer Discovery tutorial</a> (SPARK 2005) and <a href="http://docs.adacore.com/spark2014-docs/html/ug/tutorial.html">SPARK 2014 tutorial</a>. <a href="http://www.cs.swan.ac.uk/~csetzer/lectures/critsys/09/critsysfinal2.pdf">This lecture</a> gives SPARK overview in nutshell. More about SPARK 2014 can be found in <a href="http://spark-2014.org/">SPARK 2014 website</a>, <a href="http://docs.adacore.com/spark2014-docs/html/ug/spark_2014.html">SPARK 2014 Toolset User's Guide</a> and <a href="http://docs.adacore.com/spark2014-docs/html/lrm/">SPARK 2014 Reference Manual</a>. To go deeper, there is a book <a href="http://intelligent-systems.altran.com/technologies/software-engineering/spark/new-spark-book.html">SPARK: THE PROVEN APPROACH TO HIGH INTEGRITY SOFTWARE</a> by John Barnes.</p>
