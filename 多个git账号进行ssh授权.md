多数情况下我们只有一个github账号，此时我们进行ssh授权的步骤如下：
- 打开终端，执行ssh-keygen，就会在/Users/{wangmazi}/.ssh文件下生成id_rsa（公钥）和id_rsa.pub（私钥）这两个文件
- 把id_rsa公钥信息粘贴到github上

那么如果我们有多个github账号，如果再执行ssh-keygen会把原来的秘钥信息覆盖，正常操作姿势如下：
- 打开终端，执行ssh-keygen，**输入秘钥名称，如account2**，此时会生成account2和account2.pub，这样就不会覆盖原来的秘钥了
- 在/Users/{wangmazi}/.ssh文件下新建config文件，配置当前使用的git秘钥信息
```
Host github.com
    HostName github.com
    User {你的用户名}
    IdentityFile /Users/zyb/.ssh/{秘钥名称}
    IdentitiesOnly yes
```
逐行解释：
- Host github.com 用于指定该密钥的主机名，这里必须使用代码库的主机名 github.com。
- HostName github.com 指定主机对应的具体域名，与 Host 保持一致。Host 和 HostName 可以不同，但是 Host 必须与代码库的主机名匹配，也就是 Git 在需要时会使用代码库的主机名来在 SSH 配置文件中查找匹配的 Host，找到后就使用该配置，访问的具体域名将采用 HostName。
- User git 说明该配置的用户必须是 git。
- IdentityFile /root/.ssh/xxx 这一行非常关键，需要指定要使用那个 SSH 密钥文件，这里的密钥文件一定是私钥文件，不是有 pub 后缀的那个。
- IdentitiesOnly yes 请配置为 yes。


