---
title: Ruby on Rails：控制器纵览
author: gxbsst
layout: post
permalink: /archives/106
post_views_count:
  - 156
views:
  - 46
categories:
  - Ruby/Ruby on Rails
---
　在一个基于MVC的Web应用程序中，应用程序逻辑以及数据的存取是由MVC中的C,也就是控制器来完成的。因此，深刻地理解MVC框架所提供控制器对于开发一个高效、可升级、稳定的应用程序是十分必要的。RoR也不例外。 

　　RoR中所提供的控制器叫动作控制器(ActionController)。本文将主要讨论动作控制器所提供的几种服务，以及如何使用动作控制器。

　　什么是动作控制器

　　在RoR中，动作包(Action Pack)是这个框架的核心。它包括两部分，动作视图和动作控制器。动作包的一个特点是除了Web程序，不能使用在其它类型的程序中。下面让我们看看在我们通过浏览器键入一个URL后，如http://localhost:3000/demo/say/hello，都发生了什么。下面是在RoR中处理动作的步骤：

　　1. RoR首先装载了位于app/controllers目录中的say_controller.rb文件。这个文件只被装载一次。

　　2. 然后 RoR建立了类SayController的实例。

　　3. 一旦SayController类被实例化，RoR就会在app/helpers中查找say_helper.rb文件。如果这个文件存在，它就会被装载，并且这个文件将会和SayController对象混合。这就意味着在SayController对象中可以直接访问SayHelper中的方法。

　　4. 最后在app/models中查找say.rb文件，如果存在，装载它。

　　到现在为止，我们已经对应用程序的初始化过程非常清楚了，接下来让我们继续看看动作控制器所提供的服务。下面是RoR所提供的服务列表：

　　1. URL映射

　　2. 会话跟踪

　　3. 过滤和验证

　　4. 缓冲

　　现在又带来一个问题。这些服务为什么由控制器来提供。当然，答案也很简单，这是因为控制器介于数据和应用程序之间，因此，它可以监视数据的存取，并且可以根据需要对URL进行映射。因此，这些服务理所当然由控制器来提供。下面我们将详细讨论控制器提供的这些服务。

　　1. URL映射

　　当我们在浏览器中输入http://localhost:3000/admin/show时，会显示相应的内容。但你也许会有疑问，RoR是如何将URL链接映射成相应的类或方法呢？事实上，这些映射的代码都被写在了config目录中的routers.rb中。下面是这个文件的部分代码。

ActionController::Routing::Routes.drawdo|map|  
map.connect &#8216;:controller/service.wsdl&#8217;, :action => &#8216;wsdl&#8217;  
map.connect &#8216;:controller/:action/:id&#8217;  
end

　　动作控制器通过它的映射组件将来自外部请求的URL和内部的应用程序连接了起来。上述代码的第3行就是完成这个功能的。在这行语句中，map.connect的连接字符串是&#8221;:controller/:action/:id&#8221;。请求的URL只有匹配这个字符串才能被接受。对于一个URL请求来说，它可以被RoR分成三部分：

　　a. 第一部分是模式字符串中的:controller部分。

　　b. 第二部分是模式字符串中的:action部分。

　　c. 第三部分是模式字符串中的:id部分。

　　根据上面所描述的三部分，URL：http://localhost:3000/demo/admin/show/1/将被映射成以下三部分：

:controller ： &#8216;admin&#8217;,  
:action ：&#8217;show&#8217;,  
:id ：1

　　根据以上的三部分，RoR将调用admin控制器的show方法，并将参数1传到show方法中。因此，我们可以看出，RoR在其中做了很多本应该由我们做的事件。因此，RoR是一项十分强大技术。  
2. 会话跟踪

　　跨应用跟踪用户是大多数Web应用程序都需要的功能。在RoR中，我们可使用由RoR框架提供cookies或session管理来跟踪用户。但在RoR中的cookies和session管理和其它框架所提供的类似的管理不同的，RoR的cookies和session管理无需显式地调用相应的cookies和session对象就可以做到这一切。下面让我们来看看它的实现代码：

class CookiesController < ApplicationController  
def create_cookie  
cookies[:the\_time] = Time.now.to\_s  
redirect\_to :action =>&#8220;action\_two&#8221;  
end

def get_cookie  
cookie\_value = cookies[:the\_time]  
render(:text =>&#8221; #{cookie_value}&#8221;)  
end  
end

　　在以上代码中，在控制器中有两个动作方法，一个是设置cookie的，另一个是读取和显示cookie值的。在这里cookies[]是一个cookies对象数组，我们不需要声明它，只需要将它看成一个普通数组即可。

　　接下来使用redirect\_to方法通过参数:action将请新进行重定向。在get\_cookie动作中，cookies的值被取出来，然后使用render()方法显示这些值。

　　上面讨论cookie的使用方法。但如果有一种方法可以透明使用cookie，那不是更好吗？这个技术就是session。就象cookie一样，session数组也无需声明。它的用法类似于cookie对象。下面的代码描述了session的使用。

class SessionController < ApplicationController  
def login  
user = User.find\_by\_name\_and\_password(params[:user], params[:password])  
if user  
session[:user_id] = user.id  
redirect_to :action =>&#8220;index&#8221;  
else  
reset_session  
flash[:note] =&#8221;有户名或密码不正确!&#8221;  
end  
end

　　上面代码对user\_id和password进行核对。如果用户存在，将这个用户的user-id保存在session中。其中session[:user\_id] = user.id的形式和保存cookie的形式完全一样。接下来重定向到index页上。如果用户不存在，使用reset_session将session设为无效，并通过RoR返回简单的提示信息。

　　3. 过滤和验证

　　在一此情况下，在请求被处理之前，要进行一系列处理。这个过程就叫做过滤。过滤器所包含代码需要在许多动作执行前或执行后被调用。因此，过滤器分为两种，before过滤器和after过滤器。Before过滤器的代码在请求被处理前被执行，而after过滤器恰恰相反，是在请求被处理之后执行过滤代码。例如，验证用户身份代码必须要在调用一个动作之前被调用，代码如下示：

def authorize  
unless session[:user_id]  
flash[:notice] =&#8221;请登录&#8221;  
redirect_to(:controller =>&#8221;login&#8221;, :action =>&#8221;login&#8221;)  
end  
end

class AdminController < ApplicationController  
before_filter :authorize  
… …

　　以上代码在AdminController中的任何动作被执行之前调用，而在控制器中要想调用authorize函数，必须在其中加上before\_filter。after\_filter的使用方法和before_filter类似。

　　过滤器虽然可以执行验证代码，但有时对请求需要更进一步的验证，如此一来，过滤器就显得捉襟见肘了。为了完成这些功能，我们就需要使用更为强大的验证机制。在控制器中，可以通过verify实现更强大的验证功能。如下面的代码验证了用户提交方式。即用户只能用post进行提交。

class BlogController < ApplicationController  
verify :only => :post_comment,  
:session => :user_id,  
:add_flash => { :note =>&#8221;You must log in to comment&#8221;},  
:redirect_to => :index

… …

　　4. 缓冲

　　从以上代码可看出，服务器总是一遍一遍调用同样的动作，如果调用这些动作很费时间的话，将会严重影响服务器的性能。因此，RoR为了解决这一问题，为我们提供了缓冲的功能。如果某一个动作经常被调用，将这个动作进行缓冲将是一个好主意。

　　在RoR中，可以通过caches_page来实现缓冲功能。缓冲可分为不同的层次，如对整个网页进行缓冲，对动作缓冲，或是同时对网页和动作进行缓冲。如在一个blog管理应用程序，将大家经常访问的内容进行缓冲的代码如下：

class ContentController < ApplicationController  
before\_filter :verify\_premium\_user, :except => :public\_content  
caches\_page :public\_content

转载请注明：[韦旭红的点点滴滴][1] &raquo; [Ruby on Rails：控制器纵览][2]

 [1]: http://www.weixuhong.com
 [2]: http://www.weixuhong.com/archives/106