# thymeleaf的内联表达式
>应用场景：有时，我们可能更喜欢使用这种方式来处理我们的模板，比如在处理邮件发送模板的时候。
`<p>Hello, [[${session.user.name}]]!</p>`
而不是
`<p>Hello, <span th:text="${session.user.name}">Sebastian</span>!</p>`
共有两种内联表达式：`[[${msg}]]`和`[(${msg})]`
区别：当`msg = 'This is <b>great!</b>'`时
`<p>The message is "[(${msg})]"</p>`
的结果为
`<p>The message is "[(${msg})]"</p>`
而
`<p>The message is "[[${msg}]]"</p>`
的结果为
`<p>The message is "This is &lt;b&gt;great!&lt;/b&gt;"</p>`

显然，`[[${msg}]]`的表达式会将msg内容中的p标签进行转义，某些场景下并不合适

当然，在使用内联模板时，与正常的html模板来说，内联表达式中的内容会直接渲染在视图上，这在某些场景下并不适合

当然也可以通过以下方式禁用内联表达式：`th:inline="none"`
`<p th:inline="none">A double array looks like this: [[1, 2, 3], [4, 5]]!</p>`

