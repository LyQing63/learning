# Thymeleaf 布局(Layout)

---

> 使用```th:include + th:replace```方案完成开发

* 在```Layout.html```中
```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>布局</title>
    <style>
        .header {background-color: #f5f5f5;padding: 20px;}
        .header a {padding: 0 20px;}
        .container {padding: 20px;margin:20px auto;}
        .footer {height: 40px;background-color: #f5f5f5;border-top: 1px solid #ddd;padding: 20px;}
    </style>
</head>
<body>
<header class="header">
    <div>
        <a href="/book/list.html">图书管理</a>
        <a href="/user/list.html">用户管理</a>
    </div>
</header>
<div class="container" th:include="::content">页面正文内容</div>
<footer class="footer">
    <div>
        <p style="float: left">&copy; youkeda.com 2017</p>
        <p style="float: right">
            Powered by 优课达
        </p>
    </div>
</footer>

</body>
```
*  th:include="::content" : ```::content```指的是选择器，这个选择器是加载页面```th:fragment```的值

* user/list.html
```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org"
      th:replace="layout">
<div th:fragment="content">
    <h2>用户列表</h2>
    <div>
        <a href="/user/add.html">添加用户</a>
    </div>
    <table>
        <thead>
        <tr>
            <th>
                用户名称
            </th>
            <th>
                用户年龄
            </th>
            <th>
                用户邮箱
            </th>
        </tr>
        </thead>
        <tbody>
        <tr th:each="user : ${users}">
            <td th:text="${user.name}"></td>
            <td th:text="${user.age}"></td>
            <td th:text="${user.email}"></td>
        </tr>
        </tbody>
    </table>
</div>

</html>

```

* th:replace="layout" : 指定布局名称，layout指"templates/layout.html"
* th:fragment="content" : 指定选择器