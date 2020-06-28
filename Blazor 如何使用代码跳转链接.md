
可以通过在页面注入 NavigationManager 调用 NavigateTo 方法进行跳转

<!--more-->


<!-- 发布 -->

根据[官方文档](https://docs.microsoft.com/zh-cn/aspnet/core/blazor/fundamentals/routing?view=aspnetcore-3.1) 可以在页面注入 NavigationManager 拿到跳转的功能

```csharp
@page "/todo"
@inject NavigationManager NavigationManager
```

在注入 NavigationManager 之后可以在代码里面调用 `NavigationManager.NavigateTo("链接");` 将链接修改为想要跳转的代码

如下面代码在按钮点击的时候跳转到 counter 页面

```csharp
<button class="btn btn-primary" @onclick="NavigateToCounterComponent">跳转界面</button>

@code
{
	private void NavigateToCounterComponent()
	{
	    NavigationManager.NavigateTo("counter");
	}
}
```

运行上面代码就可以在点击按钮的时候跳转到 counter 页面

特别推荐两个很好用的 Blazor 的 UI 库

- [wzxinchen/Blazui: Element的blazor版本，用 .NET 写前端的 UI 框架，无JS，无TS，非 Silverlight，非 WebForm，开箱即用](https://github.com/wzxinchen/Blazui)

- [ant-design-blazor/ant-design-blazor: 🌈A set of enterprise-class UI components based on Ant Design and Blazor WebAssembly.](https://github.com/ant-design-blazor/ant-design-blazor/)



我搭建了自己的博客 [https://blog.lindexi.com/](https://blog.lindexi.com/) 欢迎大家访问，里面有很多新的博客。只有在我看到博客写成熟之后才会放在csdn或博客园，但是一旦发布了就不再更新

如果在博客看到有任何不懂的，欢迎交流，我搭建了 [dotnet 职业技术学院](https://t.me/dotnet_campus) 欢迎大家加入

如有不方便在博客评论的问题，可以加我 QQ 2844808902 交流

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议</a>进行许可。欢迎转载、使用、重新发布，但务必保留文章署名[林德熙](http://blog.csdn.net/lindexi_gd)(包含链接:http://blog.csdn.net/lindexi_gd )，不得用于商业目的，基于本文修改后的作品务必以相同的许可发布。如有任何疑问，请与我[联系](mailto:lindexi_gd@163.com)。