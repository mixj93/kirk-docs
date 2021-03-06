# 3.3 服务管理

## 3.3.1 添加服务
### 基本配置

**1. 服务名**

?> **要求：**长度为2-32, 可以是小写字母或数字, 首字符必须是小写字母

**2. 服务类型：** 分 **无状态** 和 **有状态** 两种类型
   
?> **无状态：**只支持本地存储临时数据。   
   **有状态：**通过挂载数据盘存储持久化数据，只支持单容器副本。选择有状态类型需要配置存储卷

**3. 镜像地址：**选择完镜像后显示

?> **镜像地址：**仓库地址/namespace/镜像名称:tag号

**4. 镜像仓库**：点击 **选择镜像** 后弹出

> **镜像类型**  

?> **公有镜像：**平台用户均可见  
   **私有镜像：**需要鉴权访问，一个命名空间下的私有镜像对该命名空间下的所有用户可见。

> **镜像信息**

?> **镜像：**namespace/镜像名称  
   **最新版本：**最新更新上传的版本号  
   **版本数：**创建至今累计上传版本数  
   **所选版本：**当前服务需要部署的镜像版本号(默认显示最新更新版本)  
   **操作：**部署镜像


![](_figures/user-guide/app-public-images.png)

**5. 容器规格**：提供四种规格

?> **1U1G：**单个容器配1个CPU和1G内存资源  
   **1U2G：**单个容器配1个CPU和2G内存资源  
   **2U2G：**单个容器配2个CPU和2G内存资源  
   **2U4G：**单个容器配2个CPU和4G内存资源

**6. 容器数量**：当前服务需要配置的容器实例数。服务上线后，可以通过**服务伸缩** [详见3.3.4](#jump4) 进行容器实例数的扩缩容。

**7. 存储卷配置**：服务类型为有状态时才需要配置

> **存储卷类型**

?> **云盘：**使用ceph块存储方案，具备高可靠性和可用性的特色。
　
> **读写方式**

?> **读写：**允许该服务对挂载盘进行读和写两种操作  
   **只读：**只允许该服务对挂载盘进行读操作

> **选择存储卷：**下拉选择 **存储列表** 内的存储卷进行服务挂载  

　
> **新增存储卷：**如果下拉列表内没有目标挂载卷，可以立即新增一个

?> **名称要求：**长度为2-32, 可以是小写字母或数字, 首字符必须是小写字母  
   **大小：**最小为1G，最大为1024G，调整粒度为1G

!> **注意：存储卷一旦创建成功，名称、大小无法修改**

![](_figures/user-guide/app-storage.jpeg)


### 网络配置

**8. 服务在集群内暴露**：配置服务容器在集群内的的端口号和协议类型

?> **如何实现集群内服务的互访：**服务之间如果有网络的访问需求，可以配置**集群内访问**。[详见2.2.1](quick-start/cluster-app.md)  

> **容器端口**

?> **metadata自动配置：**如果该镜像在metadata中约束了端口号，镜像选择之后，自动填写端口号
　
> **协议类型**

?> **metadata自动配置：**如果该镜像在metadata中约束了协议类型，镜像选择之后，自动选择协议类型

**9. 服务在集群外暴露**：添加负载均衡到服务

?> **如何实现集群外服务的访问：**当服务需要在集群外访问，可以 **开启负载均衡** 开关，使用或新增一个负载均衡。[详见2.2.2](quick-start/cluster-app.md)    
   **路径：** 服务的访问路径。

### 高级配置

**10. 配置文件**：将配置文件放入一个目录中供服务调用

?> **配置集名称：**下拉选择 **配置集** 内的名称进行文件配置。配置集[详见3.8](user-guide/configmap.md)  
   **挂载目录：**手动输入路径，配置文件将会放置在镜像内的该路径下。

**11. 环境变量**

> **加载方式**

?> **手动填写：**手动输入变量值  
   **配置中心 [详见3.8](user-guide/configmap.md)：**通过选择配置中心的配置项快捷定义变量值

**12. 运行目录**：镜像内启动程序的路径

**13. 执行命令**：容器启动后执行的命令

**14. 执行参数**：执行命令的参数，多个参数时用空格分隔

***
## 3.3.2 删除服务

![](_figures/user-guide/service-delete.gif)

***
## 3.3.3 启动/停止服务

![](_figures/user-guide/service-start-stop.gif)

***
## <span id="jump4">3.3.4 服务伸缩</span>

服务伸缩允许用户能够手动调整无状态服务的容器实例数，例如将wordpress的web服务2个容器实例扩容为4个.

!> **注意：有状态服务不支持弹性伸缩**

![](_figures/user-guide/service-scale.gif)

***
## 3.3.5 服务升级

允许更新服务配置，生成新的服务版本

> **镜像版本**

?> **基本配置**，包括容器规格和网络配置  
   **高级配置**，包括环境变量、运行目录、执行命令和执行参数

!> **注意：服务升级会导致日志和监控重置**

![](_figures/user-guide/service-upgrade.gif)

***
## 3.3.6 服务回滚

允许在所有服务升级的版本之间做切换。

!> **注意：服务回滚会导致日志和监控重置**

![](_figures/user-guide/service-rollback.gif)

***
## 3.3.7 日志 & 监控
七牛容器云提供服务级别的日志和监控。[详见3.7](user-guide/log-and-monitor.md)








