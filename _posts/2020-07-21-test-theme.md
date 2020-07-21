---
title: Test Theme
author: Jan Marek
layout: post
---
Tak zkouším nový theme.
Pokud dva.

{% highlight powershell %}
[string]$Path = 'TestFolder'
Get-Process -Name notepad
Invoke-Command -ComputerName test -ScriptBlock {
	param($Path)
	Test-Path ('C:\{0}' -f $Path)
} -ArgumentList $Path
{% endhighlight %}

{% highlight javascript %}
function sayHello(name) {
  if (!name) {
    console.log('Hello World');
  } else {
    console.log(`Hello ${name}`);
  }  
}  
{% endhighlight %}