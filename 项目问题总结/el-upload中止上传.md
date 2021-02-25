# el-upload中止上传

使用el-upload组件上传文件时，首先我们要明确该组件的几个生命周期钩子

| 钩子如下 |
| :--- |


| on-preview | 点击文件列表中已上传的文件时的钩子 | function\(file\) | — | — |
| :--- | :--- | :--- | :--- | :--- |
| on-remove | 文件列表移除文件时的钩子 | function\(file, fileList\) | — | — |
| on-success | 文件上传成功时的钩子 | function\(response, file, fileList\) | — | — |
| on-error | 文件上传失败时的钩子 | function\(err, file, fileList\) | — | — |
| on-progress | 文件上传时的钩子 | function\(event, file, fileList\) | — | — |
| on-change | 文件状态改变时的钩子，添加文件、上传成功和上传失败时都会被调用 | function\(file, fileList\) | — | — |
| before-upload | 上传文件之前的钩子，参数为上传的文件，若返回 false 或者返回 Promise 且被 reject，则停止上传。 | function\(file\) | — | — |
| before-remove | 删除文件之前的钩子，参数为上传的文件和文件列表，若返回 false 或者返回 Promise 且被 reject，则停止删除。 | function\(file, fileList\) | — | — |

#### 我遇到的问题：

前端问题描述：上传文件并进行校验，在该过程中可以点击取消按钮中止上传，但是点击取消按钮中止上传后，请求已取消，但是文件依旧上传成功

#### 遇到问题前的设计思路：

在on-progress钩子中调用相应函数

在el-upload中添加ref=“Upload”，在中止上传的函数中使用this.$refs.Upload.abort\(\);

注：ref的值不可重复

#### 问题点：

此时调用的后端接口没有将数据校验与数据落库分开，虽然前端取消了上传请求但是校验完的文件此时已经落库，故前端虽然取消了上传请求依旧无法阻止上传

#### 解决办法：

后端新增一个落库的接口，在上传完成且校验通过后，调用接口将数据落库



