# dialog关闭时内容闪动

#### 我遇到的问题：

dialog组件调用一次，不同的提示框内容靠通过code值的改变来负责切换，当点击确定按钮关闭dialog时提示框内容会瞬间切换一下。

#### 遇到问题前的设计思路：

通过code值的改变来负责切换dialog提示的内容，当点击确认按钮关闭dialog时会将code置空，但是当code为空时会显示默认的提示信息，造成了提示框内容会瞬间切换的问题。

#### 解决方法：

将code置空命令切换到上传文件成功之后执行，因为在文件上传成功之后下一步才会调用接口返回code，所以在此处将code置空既能保证每次从接口取code值之前code为空，又不会影响dialog提示内容的显示。



