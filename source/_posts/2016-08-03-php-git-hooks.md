---
layout: post
title: 如何简单的在 php 下运行 git hook，实现自动部署
date: 2016-08-03 10:25:04
comments: true
categories: [Ubuntu, Git, PHP]
---

由于 php 是运行在 nginx 账户下的，直接使用 `shell_exec` 会出现权限问题，所以我们首先需要解决权限问题。

1. 登录到 `www-data` 用户
```bash
usermod -s /bin/bash www-data
su www-data
```

2. 创建 `id_rsa` 并将内容复制到目标 git 中
```bash
ssh-keygen -t rsa -C "wenzhixin2010@gmail.com"

cat ~/.ssh/id_rsa.pub
```

3. 测试并 `clone` 所需要的仓库
```bash
ssh -T git@github.com
git clone git@github.com:wenzhixin/php-blog
```

4. 添加 `api.php` 文件
```php
<?php
if ($_GET['key'] == 'xxx') {
    shell_exec('git pull > logs/git.log');
}
```

5. 在 git 仓库中设置 WebHooks 即可
```
URL: api.php?key=xxx
```
