# 以运行wordpress容器为例：

以下Docker 命令用于在后台运行一个名为`word-press`的新容器，并将该容器中的`wordpress`应用监听的端口（默认是`80`）映射到宿主机的`80`端口。命令有一个拼写错误，正确的命令如下：

```bash
docker run -d -p 80:80 --name wordpress wordpress
```

解释一下命令中的各个部分：
- `docker run`: 是Docker的命令，用来运行一个新的容器实例。
- `-d`: 表示以“分离模式”（detached mode）运行容器。容器会在后台运行，并输出容器ID。
- `-p 80:80`: 端口映射参数，格式为 `-p <宿主机端口>:<容器端口>`。这告诉Docker将容器内部的端口`80`映射到宿主机的端口`80`。这意味着当在浏览器中访问宿主机的`80`端口时，实际上是访问了容器中的WordPress应用。
- `--name wordpress`: 为运行的容器指定一个名称，方便后续的管理和引用。
- `wordpress`: Docker镜像的名字，这是官方提供的Wordpress镜像。

运行此命令后，如果没有本地 `wordpress` 镜像，Docker 会从 Docker Hub 上拉取最新版本的 `wordpress` 镜像，并根据该镜像启动一个新容器。

如果你已经有一个名为 `wordpress` 的容器，你需要先停止并移除它，或者为新容器选择另一个名字。

```bash
echo $(docker logs wordpress | grep password)
```
该命令是用来从名为 `wordpress` 的 Docker 容器的日志中检索与 `password` 相关的行，并将其输出到控制台的。具体来说：

- `docker logs wordpress`: 这个命令会显示名为 `wordpress` 容器的日志输出。
- `grep password`: 这个命令会从提供的输入中搜索包含单词 "password" 的所有行。
- `$(...)`: 命令替换语法，它会执行括号中的命令，并将结果作为字符串返回。
- `echo`: 这个命令用来在终端中显示参数指定的文本。

因此，整个命令执行的结果就是把 `wordpress` 容器日志中所有包含 "password" 的行输出到控制台。

这个命令通常用于快速检索初次设置 WordPress 网站时生成的管理员密码，因为 WordPress 容器在第一次运行时会在日志中显示一个自动生成的密码。这样用户可以用这个密码登录 WordPress 后台进行配置。

请注意，日志中可能包含多个与 "password" 相关的条目，仅选择相关的信息即可。另外，还应当注意在生产环境中对密码和敏感数据的管理，避免通过日志暴露这些信息。

只需要重复执行上述的命令，换一下映射的端口，就可以再启动一个WordPress，具备良好的扩展能力。
