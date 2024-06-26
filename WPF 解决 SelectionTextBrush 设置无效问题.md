
本文告诉大家在 WPF 里面设置 SelectionTextBrush 无效的问题，可以通过 AppContext 的开关开启其行为

<!--more-->


<!-- CreateTime:2024/04/02 07:07:45 -->

<!-- 发布 -->
<!-- 博客 -->

如以下的代码，设置被选择的文本的字符颜色为红色

```xml
    <Grid>
        <TextBox Text="Test" FontSize="100" SelectionTextBrush="Red"/>
    </Grid>
```

运行项目，你将发现 SelectionTextBrush 属性设置是完全没有效果的，被选择的文本依然是黑色的

可以在 App 构造函数添加开关让 SelectionTextBrush 属性生效，代码如下

```csharp
    public App()
    {
        AppContext.SetSwitch("Switch.System.Windows.Controls.Text.UseAdornerForTextboxSelectionRendering", false);
    }
```

加上如上代码之后，再次运行项目，选择文本，你将发现选择的文本的颜色变为红色

根据微软的官方文档，这是因为在 .NET Framework 4.7.1 以及更早的版本里面，在 `System.Windows.Controls.TextBox` 和 `System.Windows.Controls.PasswordBox` 底层将在 Adorner 层绘制文本选择范围。这将会在某些系统主题下，导致文本蒙层的颜色影响文本的阅读。为了 WPF 提出新的 `Switch.System.Windows.Controls.Text.UseAdornerForTextboxSelectionRendering` 开关，用于控制 WPF 的文本选择是否采用 Adorner 层实现。当采用在 .NET Framework 4.7.2 引入的禁用 Adorner 层绘制文本选择范围时，由于底层机制的变更，能够支持在 .NET Framework 4.8 引入的 SelectionTextBrush 属性。这就是为什么设置开关能够让此属性工作的原因，一旦没有设置开关，则因为 WPF 保持兼容性，依然走 Adorner 层绘制文本选择范围而不能支持 SelectionTextBrush 属性，导致设置无效

相关文档：

- [WPF TextBox/PasswordBox Text Selection Does Not Follow System Colors](https://github.com/Microsoft/dotnet/blob/main/Documentation/compatibility/wpf-TextBox-PasswordBox-text-selection-does-not-follow-system-colors.md )
- [Add SelectionTextBrush public property to TextBox/PasswordBox non-adorner selection](https://github.com/microsoft/dotnet/blob/main/Documentation/compatibility/wpf-SelectionTextBrush-property-for-non-adorner-selection.md)

以上代码放在 [github](https://github.com/lindexi/lindexi_gd/tree/15ab047a99f4327e21ce406430651bc79a950a7a/BikallnawyeWhereluwecunu) 和 [gitee](https://gitee.com/lindexi/lindexi_gd/tree/15ab047a99f4327e21ce406430651bc79a950a7a/BikallnawyeWhereluwecunu) 上，可以使用如下命令行拉取代码

先创建一个空文件夹，接着使用命令行 cd 命令进入此空文件夹，在命令行里面输入以下代码，即可获取到本文的代码

```
git init
git remote add origin https://gitee.com/lindexi/lindexi_gd.git
git pull origin 15ab047a99f4327e21ce406430651bc79a950a7a
```

以上使用的是 gitee 的源，如果 gitee 不能访问，请替换为 github 的源。请在命令行继续输入以下代码，将 gitee 源换成 github 源进行拉取代码

```
git remote remove origin
git remote add origin https://github.com/lindexi/lindexi_gd.git
git pull origin 15ab047a99f4327e21ce406430651bc79a950a7a
```

获取代码之后，进入 BikallnawyeWhereluwecunu 文件夹，即可获取到源代码


我搭建了自己的博客 [https://blog.lindexi.com/](https://blog.lindexi.com/) 欢迎大家访问，里面有很多新的博客。只有在我看到博客写成熟之后才会放在csdn或博客园，但是一旦发布了就不再更新

如果在博客看到有任何不懂的，欢迎交流，我搭建了 [dotnet 职业技术学院](https://t.me/dotnet_campus) 欢迎大家加入

如有不方便在博客评论的问题，可以加我 QQ 2844808902 交流

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享署名-非商业性使用-相同方式共享 4.0 国际许可协议</a>进行许可。欢迎转载、使用、重新发布，但务必保留文章署名[林德熙](http://blog.csdn.net/lindexi_gd)(包含链接:http://blog.csdn.net/lindexi_gd )，不得用于商业目的，基于本文修改后的作品务必以相同的许可发布。如有任何疑问，请与我[联系](mailto:lindexi_gd@163.com)。