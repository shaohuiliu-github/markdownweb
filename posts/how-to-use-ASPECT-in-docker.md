**Shaohui Liu**

**[Home](../index.html)    [Posts](../posts.html)    [Timeline](../timeline.html)    [Research](../research.html)**

---

### 如何在docker里使用ASPECT

使用docker的逻辑如下。

1. 先在docker中下载别人打包好的image，然后根据这个image创建container。

2. 将本地文件传递到container中，并在container中完成运算任务，再将计算后到文件传递到本地。

### 1 安装并运行docker Desktop

Mac, Windows, Linux都可：https://www.docker.com/products/docker-desktop/

### 2 下载镜像并运行ASPECT

打开本地终端并执行：

```bash
$docker pull geodynamics/aspect #下载名为geodynamic/aspect的镜像
$docker images #查询目前已有的镜像信息
$docker run -it geodynamics/aspect #创建，并用终端交互的形式打开container
$docker ps -a #查看容器名
```

即可在docker的container中提交，用aspect计算任务

### 3 在本地和container之间传递文件

打开本地终端并执行：

`$docker cp local_path/filename container_id:container_path`

`$docker cp container_id:container_path local_path/filename`

以上命令可将文件位置1传送到文件位置2

### 4 运行案例

1. 选择cookbook中的案例如convection-box.prm，将其传递到docker中（例如home/dealii/aspect路径）

2. 进入docker终端（在docker客户端运行container之后的exec页面中）；也可使用`$docker start -i container_id`命令进入 （container_id可以通过`$docker ps -a`查询）
3. 在docker终端（home/dealii/aspect路径下），运行命令`$aspect convection.prm`。此为用可执行文件aspect执行参数文件.prm。
4. 将计算得到的文件夹传到本地，用Paraview打开即可。