1. **创建 Dockerfile：** 首先，创建一个名为 Dockerfile 的文本文件，用于描述构建 Docker 镜像的步骤。Dockerfile 是一种包含一系列指令的脚本，指令定义了镜像的构建过程。

2. **选择基础镜像：** 在 Dockerfile 中，选择一个合适的基础镜像，该镜像包含了你的 RPM 软件包所需的操作系统环境。通常情况下，你可以选择官方提供的 CentOS 或 Fedora 镜像作为基础镜像。

   ```
   FROM centos:7
   ```

3. **安装 RPM 软件包：** 将你的 RPM 软件包复制到 Docker 镜像中，并在镜像中安装它。在 Dockerfile 中添加以下指令：

   ```
   COPY your-software.rpm /tmp/
   RUN rpm -ivh /tmp/your-software.rpm
   ```

   这将复制你的 RPM 软件包到镜像中的临时目录，并使用 `rpm` 命令来安装它。

4. **配置运行环境：** 根据你的软件包的需要，进行任何必要的配置。这可能包括设置环境变量、创建目录、设置系统服务等。根据你的具体情况进行相应的配置。

   ```
   ENV YOUR_ENV_VARIABLE=value
   RUN mkdir /app/data
   ```

5. **暴露端口（如果需要）：** 如果你的软件需要监听某个网络端口，确保在 Dockerfile 中暴露该端口，以便外部可以访问。

   ```
   EXPOSE 8080
   ```

6. **构建 Docker 镜像：** 在包含 Dockerfile 的目录中打开终端，并执行以下命令来构建 Docker 镜像。

   ```
   docker build -t your-image-name:tag .
   ```

   这会根据 Dockerfile 中的指令构建一个名为 "your-image-name" 的镜像，"tag" 是你给镜像的版本标签，可以是任何你喜欢的标签，例如 "latest" 或者是软件版本号。

7. **运行容器：** 现在，你可以使用创建的 Docker 镜像来运行容器。

   ```
   docker run -d -p 8080:8080 your-image-name:tag
   ```

   这将在后台运行一个容器，并将容器的 8080 端口映射到宿主机的 8080 端口上。根据你的软件配置的端口，进行相应的映射。



具体事例:将功夫.rpm软件放入基于centos7系统运行