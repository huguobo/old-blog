---
layout: post
title: Node初学者教程
date: 2016-03-23 20:25:00
type: Nodejs
comment: y
---

###什么是Node.js?

很多初学者并没有真正地理解Node.js到底是什么。nodejs.org网站中的描述也没有多大帮助。

首先要清楚Node不是一个Web服务器，这十分重要。它本身并不能做任何事情。它无法像Apache那样工作。如果你希望它成为一个HTTP服务器，你必须借助它内置库自己编写。Node.js只是计算机上执行代码的另一种方式，它是一个简单的JavaScript Runtime.





###安装Node.js

Node.js的安装十分容易。只需在[这里](https://nodejs.org/download/ "这里")下载满足你需要的安装程序即可。

###已安装好Node.js，下一步做什么？

安装结束后，你可以输入一个新命令“node”。使用该“node”命令有两种不同的方法。第一种不带任何参数，将打开一个交互式Shell“>”（REPL： read-eval-print-loop），你可以在这里执行JavaScript代码。

{% highlight javascript %}
$ node  
> console.log('Hello World');  
Hello World  
undefined  
{% endhighlight %}

![](http://cms.csdnimg.cn/article/201308/28/521d9e4f51ad7.jpg)

上面案例中，我在Shell中键入了“console.log('Hello World')”，并敲回车。Node便开始执行该代码，并显示刚才记录的信息，同时打印出“undefined”。这是因为每条命令都会返回一个值，而console.log没有任何返回，故输出“undefined”。

Node命令的另一种用法是执行一个JavaScript文件。这是我们平时最常用的方法。

**hello.js**</br>


{% highlight javascript%}
console.log('Hello World');  

$ node hello.js  
Hello World
{%endhighlight%}

![](http://cms.csdnimg.cn/article/201308/28/521d9e6f77456.jpg)

该案例中，我将“console.log('Hello World');”命令存入一个文件中，并将该文件作为node命令的参数。Node运行文件中JavaScript代码，并输出“Hello World”。

###案例一：文件的输入与输出

Node.js包含一组[强大的库](https://nodejs.org/api/)（模块），可以帮助我们做很多事。第一个案例中，我将打开一个Log文件，并对它进行解析。

**example_log.txt**


{% highlight javascript%}
2013-08-09T13:50:33.166Z A 2  
2013-08-09T13:51:33.166Z B 1  
2013-08-09T13:52:33.166Z C 6  
2013-08-09T13:53:33.166Z B 8  
2013-08-09T13:54:33.166Z B 5
{% endhighlight%}
  
该Log数据什么意思并不重要，基本可以确定每条信息都包含一条数据、一个字母和一个值。我希望将每个字母后面的值进行累加。

我们要做的第一件事是读出文件的内容。

**my_parser.js**


{% highlight javascript%}
// Load the fs (filesystem) module  
var fs = require('fs');  
  
// Read the contents of the file into memory.  
fs.readFile('example_log.txt', function (err, logData) {  
  
  // If an error occurred, throwing it will  
  // display the exception and end our app.  
  if (err) throw err;  
  
  // logData is a Buffer, convert to string.  
  var text = logData.toString();  
}); 
{% endhighlight%}
通过内置的文件（fs）模块，我们可以很容易进行文件的输入/输出操作。fs模块有一个readFile方法，该方法以文件路径、回调函数为参数。该回调函数在完成文件读取后调用。文件数据读取后存储在Buffer类型中，为基本的字节数组。我们可以通过toString（）方法将它转化为字符串。

现在我们对它进行解析。

my_parser.js


{% highlight javascript%}
// Load the fs (filesystem) module.  
var fs = require('fs');  
  
// Read the contents of the file into memory.  
fs.readFile('example_log.txt', function (err, logData) {  
  
  // If an error occurred, throwing it will  
  // display the exception and kill our app.  
  if (err) throw err;  
  
  // logData is a Buffer, convert to string.  
  var text = logData.toString();  
  
  var results = {};  
  
  // Break up the file into lines.  
  var lines = text.split('\n');  
  
  lines.forEach(function(line) {  
    var parts = line.split(' ');  
    var letter = parts[1];  
    var count = parseInt(parts[2]);  
  
    if(!results[letter]) {  
      results[letter] = 0;  
    }  
  
    results[letter] += parseInt(count);  
  });  
  
  console.log(results);  
  // { A: 2, B: 14, C: 6 }  
});  
{% endhighlight%}
现在，当你将该文件作为node命令的参数时，执行该命令将打印出如下结果，执行完毕后退出。

{% highlight javascript%}
$ node my_parser.js  
{ A: 2, B: 14, C: 6 }  
{% endhighlight %}

![](http://cms.csdnimg.cn/article/201308/28/521d9e87af1e3.jpg)

我大部时候将Node.js作为脚本使用，正如上面所展示的那样。它更易于使用，是脚本程序有力的替代者。

###异步回调

正如在上例中看到的那样，Node.js典型的模式是使用异步回调。基本上，你告诉Node.js要做的事，它执行完后便会调用你的函数（回调函数）。这是因为Node是单线程的。在你等待回调函数执行过程中，Node可继续执行其他事务，不必被阻塞直到该请求完毕。

这对于Web服务器尤其重要。在现代Web应用访问数据库的过程中特别普遍。当你等待数据库返回结果的过程中，Node可以处理更多请求。与每次连接仅处理一个线程相比，它使你以很小的开销来处理成千上万个并行连接。

###案例二：HTTP服务器

Node内建有一个模块，利用它可以很容易创建基本的[HTTP服务器](https://nodejs.org/api/http.html#http_http_createserver_requestlistener)。请看下面案例。

**my_web_server.js**


{% highlight javascript%}
var http = require('http');  
  
http.createServer(function (req, res) {  
  res.writeHead(200, {'Content-Type': 'text/plain'});  
  res.end('Hello World\n');  
}).listen(8080);  
  
console.log('Server running on port 8080.');  
{%endhighlight%}
在上面，我说是的基本HTTP服务器。该例中所创建的并不是一个功能全面的HTTP服务器，它并不能处理任何HTML文件、图片。事实上，无论你请求什么，它都将返回“Hello World”。你运行该代码，并在浏览器中输入“http://localhost:8080”，你将看见该文本。

`$ node my_web_server.js  `

现在你可能已经注意到一些不一样的东西。你的Node.js应用并没有退出。这是因为你创建了一个服务器，你的Node.js应用将继续运行，并响应请求，直到你关闭它。

如果你希望它成为一个全功能的Web服务器，你必须检查所收到的请求，读取合适的文件，并返回所请求的内容。值得高兴的是，有人已经帮你做了这个艰难的工作。

###案例三：Express框架

[Express](http://expressjs.com/)为一个框架，可使创建网站的过程十分简单。你首先需要安装它。除了node命令，你还需要访问“npm”命令。利用该工具，你可以访问社区所创建的庞大模块集。其中之一就是Express。

{%highlight javascript%}
$ cd /my/app/location  
$ npm install express  
{%endhighlight%}
当你安装了一个模块，它将出现在应用程序所在目录的“node_modules”文件夹中。现在我们可以利用Express来创建一个基本的静态文件服务器。

**my_static_file_server.js**


{%highlight javascript%}
var express = require('express'),  
    app = express();  
  
app.use(express.static(__dirname + '/public'));  
  
app.listen(8080);</b>  
{%endhighlight%}

{%highlight javascript%}
$ node my_static_file_server.js  
{%endhighlight%}
现在你已创建了一个强大的静态文件服务器。你可以通过浏览器请求访问你放在public文件夹中任何文件，并进行展示，包括HTML、图片等任何东西。比如，把一个名为“my_image.png”的图片放在public文件夹中，你可以在浏览器中输入“http://localhost:8080/my_image.png”来访问该图片。当然，Express还有很多特性，你可以在以后的开发中继续探索。

###NPM

上面我们已经接触到了npm，但我仍想强调一下在Node.js开发过程中该工具的重要性。它有成千上万个模块可帮我们解决遇到的大部分典型问题。在重新发明轮子之前，记得检查一下npm中是否有相应功能。 

上一例中，我们手动安装了Express。如果你的程序包含很多“依赖”（Dependency），那再利用该方法安装它们就不合适了。为此npm提供了一个package.json文件。

**package.json**
{%highlight javascript%}
{  
  "name" : "MyStaticServer",  
  "version" : "0.0.1",  
  "dependencies" : {  
    "express" : "3.3.x"  
  }  
} 
{%endhighlight%}
package.json文件包含了应用程序的基本信息。其中“dependencies”部分描述了你想安装模块的名称和版本。该案例，接受Express 3.3的任何版本。你可以在该部分列出你想要的所有依赖。

代替之前一个个安装每个依赖，现在我们可以运行一个命令，即可将它们全部安装完成。

{%highlight javascript%}
$ npm install  
{%endhighlight%}
运行该命令，npm将在当下文件夹中查找“package.json”文件。一旦找到，即可安装所列出的所有依赖。

###代码的组织

在大部分应用程序中，你的代码往往被分割到几个文件中。现在让我们把最开始案例中的Log分析脚本分离出来。这样该程序将更易于测试与维护。

**parser.js**


{%highlight javascript%}
// Parser constructor.  
var Parser = function() {  
  
};  
  
// Parses the specified text.  
Parser.prototype.parse = function(text) {  
  
  var results = {};  
  
  // Break up the file into lines.  
  var lines = text.split('\n');  
  
  lines.forEach(function(line) {  
    var parts = line.split(' ');  
    var letter = parts[1];  
    var count = parseInt(parts[2]);  
  
    if(!results[letter]) {  
      results[letter] = 0;  
    }  
  
    results[letter] += parseInt(count);  
  });  
  
  return results;  
};  
  
// Export the Parser constructor from this module.  
module.exports = Parser;
{%endhighlight%}
在此创建了一个新文件，来存放Log分析脚本。这仅仅是一种标准JavaScript，还有很多方法可用来封装该代码。我选择重新定义一个JavaScript对象，这样更容易进行单元测试。

该程序中最重要的部分是“module.exports = Parser;”这一行代码。它告诉Node从该文件中要输出的内容。在该例中，我输出了构造函数，用户可以用Parser对象来创建实例。你可以输出任何你想要的。

现在我们看一下，如何导入该文件，来使用Parser对象。

**my_parser.js**


{%highlight javascript%}
// Require my new parser.js file.  
var Parser = require('./parser');  
  
// Load the fs (filesystem) module.  
var fs = require('fs');  
  
// Read the contents of the file into memory.  
fs.readFile('example_log.txt', function (err, logData) {  
  
  // If an error occurred, throwing it will  
  // display the exception and kill our app.  
  if (err) throw err;  
  
  // logData is a Buffer, convert to string.  
  var text = logData.toString();  
  
  // Create an instance of the Parser object.  
  var parser = new Parser();  
  
  // Call the parse function.  
  console.log(parser.parse(text));  
  // { A: 2, B: 14, C: 6 }  
}); 
{%endhighlight%}

如模块一样，文件被引入其中，你需要输入路径，而非名称。

###总结

希望该教程可以帮助到你。Node.js是一个强大、灵活的技术，可以帮助解决各种各样的问题。它已经超出了我们的想像。