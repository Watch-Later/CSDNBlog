
本文告诉大家如何在 GTK Sharp 里面设置窗口背景透明

<!--more-->


<!-- CreateTime:2024/03/28 07:23:22 -->

<!-- 发布 -->
<!-- 博客 -->

在 GTK 里面设置窗口背景透明十分简单，只需使用如下代码即可

```csharp
        this.AppPaintable = true;
        var screen = this.Screen;
        var visual = screen.RgbaVisual;
        if (visual is not null && screen.IsComposited)
        {
            this.Visual = visual;
        }
```

感谢 [walterlv](https://github.com/walterlv) 大佬提供此方法，我只是代为记录的工具人

上面代码一般是放在窗口的构造函数里面，如以下示例

```csharp
internal sealed class DemoWindow : global::Gtk.Window
{
    public DemoWindow() : base(global::Gtk.WindowType.Toplevel)
    {
        Title = "Walterlv Blank Gtk App";
        SetDefaultSize(800, 600);
        Add(new Area());

        this.AppPaintable = true;
        var screen = this.Screen;
        var visual = screen.RgbaVisual;
        if (visual is not null && screen.IsComposited)
        {
            this.Visual = visual;
        }
    }

    protected override bool OnDeleteEvent(Event evnt)
    {
        global::Gtk.Application.Quit();
        return base.OnDeleteEvent(evnt);
    }
}
```

如果你运行代码没有看到窗口背景透明，那可能是你的系统里面的桌面窗口合成管理不正确或没安装，请自行解决，如安装 [compiz](https://en.wikipedia.org/wiki/Compiz) 窗口合成管理器。详细请看 [dotnet C# 设置 X11 应用窗口背景透明](https://blog.lindexi.com/post/dotnet-C-%E8%AE%BE%E7%BD%AE-X11-%E5%BA%94%E7%94%A8%E7%AA%97%E5%8F%A3%E8%83%8C%E6%99%AF%E9%80%8F%E6%98%8E.html ) 这篇博客的窗口合成管理器处理部分

本文代码放在 <https://github.com/walterlv/Walterlv.BlankUnoApp> 仓库里，欢迎大家拉取代码运行


我搭建了自己的博客 [https://blog.lindexi.com/](https://blog.lindexi.com/) 欢迎大家访问，里面有很多新的博客。只有在我看到博客写成熟之后才会放在csdn或博客园，但是一旦发布了就不再更新

如果在博客看到有任何不懂的，欢迎交流，我搭建了 [dotnet 职业技术学院](https://t.me/dotnet_campus) 欢迎大家加入

如有不方便在博客评论的问题，可以加我 QQ 2844808902 交流

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议</a>进行许可。欢迎转载、使用、重新发布，但务必保留文章署名[林德熙](http://blog.csdn.net/lindexi_gd)(包含链接:http://blog.csdn.net/lindexi_gd )，不得用于商业目的，基于本文修改后的作品务必以相同的许可发布。如有任何疑问，请与我[联系](mailto:lindexi_gd@163.com)。